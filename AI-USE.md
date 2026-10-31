# AI use and course mentoring

AI assistance in this course is intended to support understanding, debugging,
and independent work. You remain the author of the reasoning, implementation,
and wording submitted for assessment. Follow your official course and activity
instructions, including any more specific limits on AI use.

## Help you can request

- Explanations of concepts, unfamiliar terminology, error messages, tracebacks,
  test failures, and existing feedback.
- Questions and bounded hints that help you choose and carry out the next step.
- Feedback on your own draft, code, design, or test approach without an AI
  replacement for your work.
- Clearly different practice examples when they do not reveal the assessed
  reasoning or become the assignment solution with superficial changes.
- Help understanding documented setup steps and commands, including their
  purpose, prerequisites, and effects. You run commands in the default mentor
  workflow and share relevant results with private information removed.
- Drafts of ordinary GitHub Issues or Discussions asking for help or reporting
  a problem, based on your actual observations.

You can ask a basic conceptual question without first producing code or
completing a troubleshooting checklist. Ask your instructor through the
documented course channel when instructions are missing or a barrier persists.

## Work that remains yours

The AI must not create, complete, repair, rewrite, or supply submission-ready
parts of assessed worksheets or deliverables. This includes assessed source
code, tests, analyses, designs, diagrams, pseudocode, docstrings, explanations,
reflections, and evidence of testing.

The boundary applies to file changes, chat replies, patches, downloadable
artifacts, worked examples, and other output locations. A sequence of small
hints must not assemble the solution. The central decisions and expression
must remain yours, even when you are stuck or close to a deadline.

For debugging, the mentor can explain the failure, point to relevant evidence,
and suggest an investigation. You make the substantive correction. For
writing, it can discuss purpose, completeness, and unclear reasoning without
rewriting an assessed passage for you. Preserve original-wording requirements,
including any activity rule that excludes AI-generated docstrings.

The mentor must not invent requirements, citations, observations, test results,
completed steps, grades, extensions, or permissions. It must not search for
answer keys or another student's solution to complete your activity.

## Issues and Discussions

For an ordinary support post, the AI may draft a title and complete post from
facts you provide: the affected activity, your goal, relevant environment,
actual steps, expected and observed behavior, and the help requested.
Unknown details must stay unknown rather than being invented.

Review the draft before sharing it. Remove credentials, student records,
private feedback, personal details, and unnecessary assignment code. A support
post must not expose a completed solution. Drafting does not authorize the AI
to publish, send messages, or change a GitHub Issue or Discussion.

If an activity assesses the substantive content of a post itself, the same
student-authorship boundary applies to that assessed content. The mentor can
explain the structure and review your draft.

## Using the Course Mentor

In a supported VS Code session, select **Course Mentor**. Its configuration
requests only reading and searching, with no file editing, terminal execution,
MCP tools, or implementation handoffs. Verify the tools actually available in
the selected client and session before relying on that restriction.

The workspace defaults disable Copilot inline completions and next-edit
suggestions while preserving chat. Custom instructions do not govern inline
suggestions, so the two configurations serve different purposes.

Reusable prompts under `.github/prompts/` help you understand an activity,
debug an attempt, review your work, or draft a support post. Prompt-file support
depends on the client; use their body text manually where necessary. The
mentoring boundary also applies when no saved prompt is used.

AI is optional unless your official course instructions explicitly say
otherwise. Preserve documented non-AI support and accessibility alternatives.
Follow any established acknowledgement or disclosure requirements; the AI
must not write an assessed personal reflection or invent an AI-use history.

## Course-template authoring

This source repository contains generic course and activity templates.
`{{AI TODO: ...}}` markers are intentional authoring placeholders for creating
course-specific repositories and files. They are not student tasks and do not
authorize a student-facing mentor to fill assessed work.

Course authors resolve these markers and supply verified activity context
before publishing student-facing material. Unresolved context does not permit
the mentor to invent outcomes, rubrics, or assignment solutions. Template
maintenance and student mentoring are separate working contexts.

## Limits of repository configuration

Instruction files and workspace settings guide supported clients; they cannot
prove which tools a person used or guarantee every model response. Personal
settings, other clients, and tools outside this repository may behave
differently. The configured mentor should still provide useful, bounded help
and preserve student ownership across the conversation.
