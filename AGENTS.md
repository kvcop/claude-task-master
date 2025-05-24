# Agent Instructions

## Overview
This repository uses the Task Master development process. `tasks/tasks.json` is the source of truth for all work items and each task also has a matching file under `tasks/`.
For a detailed explanation of how to manually reproduce Task Master's behavior with an AI assistant, see `INNER_WORKINGS.md`.

## Bootstrapping a Project
1. If no `tasks/` directory is present:
   - Create `scripts/prd.txt` and place the product requirements there.
   - Manually read the PRD and produce `tasks/tasks.json` using the structure in `docs/task-structure.md` (fields: id, title, description, status, dependencies, priority, details, testStrategy, subtasks).
   - Make a `tasks/` directory and create one file per task (`task_001.txt`, etc.) following the Task File Format from the same document.

## Daily Workflow
1. **Task discovery** – open `tasks/tasks.json` to see all tasks and review their dependencies and priorities. The next task is the highest priority item whose dependencies are done.
2. **Implementation** – follow the instructions in the task's `details` section and write tests as described in `testStrategy`.
3. **Verification** – run tests or perform manual checks as specified. Only mark a task complete when verification succeeds.
4. **Completion** – update the task status in both `tasks/tasks.json` and its task file.
5. **Handling drift** – if current implementation changes the plan, edit tasks from the affected ID onward so future tasks stay aligned.
6. **Breaking down work** – for complex tasks, add `subtasks` entries in `tasks/tasks.json` and regenerate the corresponding task file sections.

## Best Practices
- Keep tasks in sequential order and avoid circular dependencies.
- When editing tasks, maintain synchronization between `tasks/tasks.json` and the individual files.
- Use the examples in `assets/scripts_README.md` and `docs/tutorial.md` for guidance on structuring tasks and subtasks.
- Revisit the PRD when major changes occur to ensure tasks still reflect requirements.

## Important
- Do not use the `task-master` CLI. All operations—parsing the PRD, generating task files, updating statuses—must be performed manually by modifying the repository files.
- Review the documentation under `docs/` whenever uncertain about field meanings or recommended workflow.
