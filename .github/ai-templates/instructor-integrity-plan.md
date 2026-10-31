# Instructor integrity-check design

**Status: planned; not implemented or deployed.** Course AI files are being added to the GC-STEM `crs000` template. This document adds a maintainer-facing design only. Deployment of an external checker is separate, explicit work; this change creates no workflow, App installation, credentials, account connection, or scheduled check.

## Purpose and limits

Provide reproducible evidence that designated files at a recorded repository commit match an approved course release, plus a review list of missing, changed, or newly added instruction-related files. A difference is a fact for human review, not an accusation, grade, or finding of misconduct.

Repository verification cannot establish which AI tool someone used, what instructions it loaded, or whether it followed them. Personal instructions, client settings, uncommitted files, external tools, and instructions outside the repository are out of scope. Matching one snapshot does not establish that files were unchanged between checks, in other branches, or during earlier sessions.

## Trust boundary

Keep the approved baseline, verifier, target registry, credentials, and results outside learner-controlled repositories, in an instructor-controlled location. A repository owner can change files, hashes, workflows, and branches within their repository. A copied checksum or workflow therefore cannot be the authoritative evidence of its own integrity.

In a private personal-account repository, the owner retains full control and collaborators receive write access; GitHub does not offer read-only collaborator access there. Instructor collaboration enables access without transferring ownership or enforcing course policy. The checker should deliberately use a separate read-only credential. [GitHub: personal-repository permissions](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/repository-access-and-collaboration/permission-levels-for-a-personal-account-repository)

## Approved baseline

Use **exact SHA-256 equality after narrowly defined text normalization** for the match decision. Fuzzy similarity cannot establish unchanged instructions: deleting “not” can reverse a rule while leaving a document highly similar. Similarity may order human review, but must not convert a difference into a match.

Maintain an instructor-controlled manifest for each approved release containing:

- Release identifier and full authoritative source commit ID, rather than a movable branch or tag alone.
- Manifest, normalization, and supported file-discovery profile versions.
- Required paths, expected Git entry types/modes, and raw and normalized SHA-256 digests.
- Approved additional instruction paths, permitted variants, effective dates, migration periods, and documented exceptions.

For declared UTF-8 text, convert CRLF to LF and preserve everything else: spaces, comments, case, Unicode, byte-order marks, and final newlines. Do not trim or rewrite text. Invalid UTF-8 needs review; compare binary files as raw bytes. Retain raw hashes so accepted line-ending differences remain visible. SHA-256 digests are distinct from Git object IDs.

Generate baselines from approved course releases, never automatically from learner repositories. Retain earlier approved versions. Authorized policy updates produce a new baseline or exception; they are not automatically violations.

## Complete instruction inventory

Compare required files, then enumerate the entire tree at the same commit for additions, removals, renames, and files that could supplement or shadow unchanged guidance. Review the discovery profile when supported clients change. Candidate families include:

- Root/nested `AGENTS.md`, override files, and configured fallback names.
- Repository-wide/path-specific instructions, prompts, custom agents, and repository skills.
- AI/MCP configuration, editor/workspace settings affecting instruction loading, hook definitions, and referenced hook scripts.

These are candidates, not a claim that every client loads every file. New candidates require review without implying misconduct. Read them as data; never execute learner workflows, scripts, hooks, commands, or package installation.

Record symlinks, submodules, large-file pointers, unsupported encodings, size limits, and ambiguous path/case collisions. Do not silently follow links outside the inspected tree or call an incomplete inspection a match. The profile must specify supported handling.

## Proposed external checker

A private instructor-controlled repository could hold the baseline and verifier, with manual execution and optional scheduled GitHub Actions. Learners would have no write access there. Review verifier/manifest changes, pin reusable dependencies to reviewed revisions, and keep credentials under instructor control.

Prefer an instructor-maintained GitHub App installed by each participating repository owner, limited to **Only select repositories**, **Contents: read**, and necessary metadata. Request no repository writes, administration, issue/comment/check posting, or unrelated repository access. Instructor collaborator membership does not install an App on someone else's account. Owners can withdraw access. [GitHub: App installation](https://docs.github.com/en/apps/using-github-apps/installing-a-github-app-from-a-third-party), [GitHub: changing/blocking access](https://docs.github.com/en/apps/using-github-apps/reviewing-and-modifying-installed-github-apps)

The central workflow's `GITHUB_TOKEN` accesses its own repository; a properly installed App supplies installation tokens for the separate private repositories. Limit tokens to required repositories and read permissions. [GitHub: App authentication in Actions](https://docs.github.com/en/apps/creating-github-apps/authenticating-with-a-github-app/making-authenticated-api-requests-with-a-github-app-in-a-github-actions-workflow)

Choose cadence and freshness limits during deployment. Scheduled Actions run from the verifier's default branch and can be delayed or dropped; stale or absent runs remain unavailable evidence. [GitHub: schedule behavior](https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows#schedule)

## Reproducible read sequence

1. Load the approved release and assigned repository/ref or submitted commit from instructor-controlled records.
2. Resolve a branch once to a full commit ID, or use the recorded submission commit. Record repository identity, ref, commit, observation time, baseline, and verifier versions. Obtain that commit's tree; avoid separate reads through a moving branch. [GitHub: commit objects](https://docs.github.com/en/rest/git/commits#get-a-commit-object)
3. Enumerate the tree. If recursive output is truncated, traverse subtrees until complete or report an incomplete inspection. [GitHub: trees](https://docs.github.com/en/rest/git/trees#get-a-tree)
4. Retrieve relevant blobs by object ID as raw bytes or decoded Base64, without checkout or execution. [GitHub: blobs](https://docs.github.com/en/rest/git/blobs#get-a-blob)
5. Compare hashes, paths, entry types, and the inventory. Produce a report tied to that exact snapshot. Later branch changes require another observation.

Treat downloaded filenames and contents as untrusted data; do not derive commands from them.

## Results and review

| Result | Meaning |
| --- | --- |
| Matches approved snapshot | Required files match the assigned baseline, inventory has no unresolved candidates, and inspection is complete. State commit/time without runtime or conduct claims. |
| Difference for review | Missing, changed, moved, differently typed, or newly discovered relevant files. Check approved versions/exceptions and show limited relevant diffs. |
| Unverifiable | Access loss, unavailable repository/commit, authentication/API failure, rate limits, incomplete tree, unsupported entry, or stale observation. Never count this as a current match; retain earlier observations separately. |
| Not assigned | No applicable approved baseline; infer neither compliance nor noncompliance. |

Restrict results to instructors and retain only necessary repository identifiers, commits, timestamps, versions, path statuses, hashes, and relevant diffs. Define access and retention during deployment. Do not collect chat logs or unrelated learner work, grade learners, monitor general activity, or post messages or repository writes.

Before deployment, validate synthetic examples covering a one-word edit, deletion, nested override, authorized release update, revoked access, and truncated inventory. This design does not activate those checks.
