# Universal Git Project Continuity Bootstrap

You are establishing a durable Git-based project environment designed so that different AI models, human operators, local agents, or cloud agents can work on the project at different times without relying on previous chat history.

The repository must become the authoritative project memory.

The system must work for software development, infrastructure, research, automation, hardware modification, reverse engineering, device hacking, electronics projects, media projects, documentation projects, or other complex work that can be decomposed into tasks.

Do not assume this is a software-only project.

## Core principle

A new model entering this repository should be able to determine, with minimal reading:

1. What the project is trying to accomplish.
2. What currently exists.
3. How the major components fit together.
4. What dependencies, software, hardware, services, environments, and resources are involved.
5. What has already been attempted.
6. What succeeded or failed.
7. What task is currently active.
8. What the next executable task is.
9. How that task will be proven complete.
10. What information or access is still missing.

Chat history must never be required to continue the project.

Anything important enough that another model may need it later must be recorded in the repository.

---

# 1. Inspect Before Changing Anything

Before creating or modifying project files:

- Inspect the repository structure.
- Read existing documentation.
- Inspect Git status.
- Determine the current branch and remote state.
- Inspect recent commit history.
- Preserve existing work.
- Do not overwrite existing documentation simply because it does not match this structure.
- Integrate useful existing documentation into the structure when appropriate.
- Do not discard uncommitted changes.
- Do not invent project goals that have not been supplied by the owner.

If this is an existing project, learn from what is already present before reorganizing anything.

If this is a new or nearly empty repository, establish the framework below.

---

# 2. Required Project Memory Structure

Use the following structure unless the existing repository has a strong reason to place an equivalent document elsewhere.

## README.md

This is the front door to the project.

Keep it concise.

It should explain:

- what the project is,
- its current broad status,
- where the authoritative project records are,
- how a new model should begin.

It should point a new model to `AGENTS.md` and `TASKS.md` first.

---

## AGENTS.md

This contains the permanent operating instructions for any model working in the repository.

It must explain:

- what files must be read at startup,
- how to inspect current Git state,
- how tasks are selected,
- how scope is controlled,
- how blockers are recorded,
- how evidence is recorded,
- how scripts and important code are preserved,
- how configuration changes are documented,
- how secrets are handled,
- how work is handed off,
- what must be updated before ending a session.

A model starting work should normally read:

1. `AGENTS.md`
2. the Current Handoff section of `TASKS.md`
3. the relevant portion of `TASKS.md`
4. `PROJECT_CONTEXT.md`
5. `RESOURCES.md`
6. the recent entries in `JOURNAL.md`
7. Git status and recent Git history

Do not require a model to read the entire historical journal before beginning work.

---

## TASKS.md

`TASKS.md` is the single authoritative project plan and task status file.

Do not maintain competing task lists in chat, GitHub Issues, miscellaneous notes, or other documents unless the owner explicitly requests another system.

Other documents may explain a task, but `TASKS.md` determines its state.

### Current Handoff

The top of `TASKS.md` must contain a compact `Current Handoff` section.

It should contain enough information for a newly started model to resume quickly, including:

- project goal summary,
- current task ID,
- exact next action,
- most recently completed work,
- active blockers,
- relevant current environment or system state,
- important failed attempts that should not be blindly repeated,
- branch or Git state when relevant,
- last important validation result,
- any unsaved, uncommitted, unpushed, external, or owner-held work.

This section should describe the present, not the full history.

### Hierarchical task tree

Tasks must form a numbered tree.

Example:

- `1`
- `1.1`
- `1.1.1`
- `1.1.2`
- `1.2`
- `2`
- `2.1`

Top-level numbers represent broad project goals.

Children break those goals into increasingly focused work.

Continue decomposing work until the leaves are small enough for a model to complete as one focused unit without losing the parent goal.

Task IDs are permanent.

Never renumber completed tasks because priorities change.

Never reuse an old task ID for unrelated work.

### Task statuses

Use:

- `todo`
- `in_progress`
- `blocked`
- `done`
- `cancelled`

Only leaf tasks are directly executable.

### Leaf task format

Each executable leaf should contain:

```text
- N.N [status] Short action-oriented task name.
  - Goal: Why this task exists and what parent objective it advances.
  - Depends on: Required task IDs, or none.
  - Scope: What is included and what boundaries matter.
  - Inputs: Files, hardware, services, information, or resources required.
  - Done when: An observable test, result, artifact, or condition proving completion.
  - Evidence: Actual validation results, commands, measurements, artifact references, or pending.
  - Artifacts: Important files, scripts, code, diagrams, logs, or outputs created by this task.
  - Blocker: None, or the exact missing prerequisite and next action.
```

### Task sizing

A leaf task should have one primary goal.

If a task contains several independently meaningful outcomes, split it.

If a task cannot reasonably be completed in one focused model session, split it.

If unexpected complexity appears during implementation, create child tasks rather than allowing the current task to expand without limit.

A task is not complete because code was written or an action was attempted.

A task is complete only when its `Done when` condition has been satisfied and evidence has been recorded.

Failed or unperformed validation is not completion.

### Choosing the next task

Resume an eligible `in_progress` task first.

Otherwise choose the lowest-numbered executable leaf whose dependencies are complete.

Dependencies override numeric ordering.

If an earlier task is blocked, clearly record the blocker and continue with the next independent eligible leaf when useful work is available.

If no task is executable, identify the exact information, authorization, hardware, resource, or dependency preventing progress.

When the owner asks:

"What is the next task?"

Do not automatically begin implementation.

Report:

- task ID,
- task goal,
- prerequisites,
- exact completion check.

Then wait for the owner to direct execution unless the surrounding request clearly asks you to proceed.

---

# 3. PROJECT_CONTEXT.md

Create `PROJECT_CONTEXT.md` as the high-level technical and operational map of the project.

This is intended to prevent future models from having to rediscover how the project works.

It must be useful for both software and non-software projects.

Include applicable sections for:

## Project environment

Record relevant environments such as:

- operating systems,
- development environments,
- runtime environments,
- physical locations,
- servers,
- workstations,
- embedded devices,
- test benches,
- virtual machines,
- containers,
- cloud services,
- networks,
- repositories.

## Core components

Identify major components involved in the project.

These may be:

- applications,
- libraries,
- databases,
- services,
- APIs,
- containers,
- operating systems,
- firmware,
- hardware modules,
- boards,
- adapters,
- radios,
- storage devices,
- test equipment,
- mechanical components,
- external services,
- datasets.

## Dependencies

Record important dependencies and relationships.

Where relevant include:

- software package and version,
- firmware version,
- hardware revision,
- runtime,
- compiler,
- database,
- library,
- driver,
- API,
- protocol,
- electrical interface,
- communications interface,
- network dependency,
- upstream repository,
- external service.

Pin exact versions, revisions, commits, or firmware when reproducibility requires it.

Clearly distinguish verified versions from assumptions or planned versions.

## Connection map

Explain how the major pieces interact.

Describe important:

- data flow,
- network flow,
- control flow,
- physical connections,
- ports,
- protocols,
- buses,
- APIs,
- mounts,
- shares,
- file movement,
- build relationships,
- dependencies between machines,
- dependencies between hardware components.

Use a simple Mermaid diagram when it significantly improves understanding and the repository supports Markdown rendering.

The purpose is not decoration. It is to allow a new model to understand the system without rediscovering its structure.

## Configuration summary

Record important high-level configuration.

Include configuration that another model would need to reproduce, troubleshoot, modify, or understand the environment.

Do not store secrets.

Record secret binding names or required credential types instead of their values.

Examples include:

- important paths,
- ports,
- service names,
- container names,
- database names,
- environment variable names,
- device addresses,
- VLAN or network roles,
- build options,
- enabled modules,
- feature flags,
- firmware modes,
- jumper settings,
- interface settings,
- compile-time choices.

Avoid dumping enormous generated configuration files into this document.

Document the configuration that explains how the project works and point to authoritative configuration files where appropriate.

## Constraints and assumptions

Record important project limitations such as:

- storage limits,
- cost limits,
- hardware limitations,
- safety constraints,
- compatibility requirements,
- licensing restrictions,
- network restrictions,
- owner preferences,
- destructive operations requiring approval.

## Known unknowns

Maintain a small section for important information that has not yet been established.

Once resolved, move the information into its proper section rather than allowing this section to become a permanent backlog.

Tasks still belong in `TASKS.md`.

---

# 4. RESOURCES.md

Use `RESOURCES.md` as the resource inventory.

Record resources such as:

- repositories,
- computers,
- servers,
- devices,
- storage locations,
- shares,
- external services,
- test equipment,
- source repositories,
- documentation sources,
- APIs,
- accounts or access methods,
- local paths,
- remote paths,
- network endpoints.

For each resource distinguish between:

- supplied information,
- verified information,
- planned information,
- unknown information.

Record when and how important facts were last verified.

Never store:

- passwords,
- API keys,
- tokens,
- private keys,
- credential-bearing URLs,
- recovery codes.

Record only the non-secret name or binding needed to locate those credentials securely.

---

# 5. JOURNAL.md

`JOURNAL.md` is an append-only project action history.

Do not use it as the task list.

Each meaningful work session should append a concise entry containing:

- timestamp with timezone,
- task ID,
- action performed,
- relevant result,
- validation result,
- important failure or discovery,
- Git commit when useful.

Do not rewrite previous journal entries to make history look cleaner.

If an earlier entry is incorrect, append a correction referencing the affected task or entry.

Record results, not merely intentions.

The journal exists so later models can investigate history when troubleshooting without bloating the Current Handoff.

---

# 6. Preserve Important Scripts and Code in Git

Do not allow valuable project logic to exist only in:

- chat messages,
- temporary shell commands,
- terminal history,
- scratch files,
- a model's temporary workspace.

If a script, code fragment, query, configuration generator, conversion tool, deployment helper, repair tool, diagnostic utility, data transformation, firmware tool, or repeatable command sequence materially contributed to the project, preserve it in Git when appropriate.

Use a `scripts/` or similarly appropriate source directory.

Create `scripts/README.md` when enough scripts exist to require an index.

The index should identify:

- script name,
- purpose,
- associated task IDs,
- expected environment,
- whether it modifies state,
- important prerequisites,
- current or retired status.

Use clear filenames.

Prefer reusable scripts over repeatedly reconstructing complicated command sequences in chat.

### Historical code

Git history itself is the primary version archive.

Do not create a duplicate file for every revision.

However, when an older standalone implementation, diagnostic tool, migration script, firmware extraction tool, recovery routine, or other historically important piece of code may be valuable for future debugging, comparison, optimization, cleanup, or restoration, preserve it intentionally.

If it is no longer active but deserves to remain directly accessible, place it under an appropriate archive location such as:

`scripts/archive/`

Document:

- why it was retained,
- which task produced it,
- what replaced it,
- whether it is safe to run.

Never silently delete a historically important troubleshooting or recovery tool merely because a newer solution exists.

---

# 7. External and Large Artifacts

Git should contain project knowledge, source, scripts, small configuration, and reasonable documentation artifacts.

Large binary assets, disk images, firmware dumps, backups, database dumps, VM images, generated builds, media files, installation archives, or other large artifacts may belong in external storage.

When external artifacts are important to reproducing the project, maintain:

`assets/MANIFEST.tsv`

Recommended fields:

```text
asset_id
project_relative_path_or_location
bytes
sha256
purpose
task_id
verified_at
```

Use checksums for artifacts where exact identity matters.

Do not assume that a file exists merely because its name is documented.

Differentiate planned, supplied, and verified assets.

---

# 8. docs/WORKFLOW.md

Create a concise workflow describing how work moves between models, computers, and locations.

It should explain:

- how a model starts a session,
- how it finds the current task,
- how it marks work in progress,
- how it records evidence,
- where scripts belong,
- where configuration knowledge belongs,
- how large artifacts are handled,
- how blockers are recorded,
- how a session is handed off,
- how another model resumes.

The repository, not a chat transcript, is the continuity mechanism.

---

# 9. Git Working Method

Respect any established repository workflow.

If no workflow exists, prefer the simplest workflow that minimizes fragmented state.

Use concise commits that reference task IDs when practical.

Examples:

```text
2.3: add device communication test
4.1: record dependency versions
5.2: fix configuration generator
```

Commit task-state and journal updates with the associated work when practical.

Do not claim work is available to another model until it is actually saved in the shared Git repository or another explicitly documented shared location.

Clearly distinguish:

- modified locally,
- committed locally,
- pushed remotely.

Before completing a work session:

1. Update task status and evidence.
2. Update Current Handoff.
3. Update `PROJECT_CONTEXT.md` or `RESOURCES.md` if the known system changed.
4. Preserve important scripts or code.
5. Append the meaningful outcome to `JOURNAL.md`.
6. Inspect the diff for unintended files or secrets.
7. Commit with the relevant task ID when appropriate.
8. Push when repository access allows it.
9. Clearly record anything that remains local or external.

Never force-push, discard another worker's changes, or reset unknown work simply to make the repository appear clean.

---

# 10. Avoid Scope Drift

Every implementation action should trace back to a task.

When useful unrelated work is discovered:

- record it as a new task,
- record it as a blocker,
- or record it as a future child of the appropriate goal.

Do not silently expand the active task.

Do not invent detailed owner goals merely because they appear technically reasonable.

The model may recommend improvements, but recommendations are not automatically accepted project requirements.

---

# 11. Build the Task Tree From the Goal, Not From Technology

Do not begin by creating tasks simply because a technology normally requires them.

First understand the desired outcome.

Then work backward from observable success.

Break the project into major goals that collectively satisfy the owner's definition of done.

Break each goal into smaller dependent outcomes.

Continue decomposition until the executable leaf tasks are appropriately sized.

Every required outcome should map to at least one task.

Every task should map back to a project goal.

Include research, access verification, environment discovery, backup/recovery, testing, validation, documentation, migration, cleanup, and handoff tasks when they are genuinely required by the project.

Do not add ceremony that provides no practical value.

---

# 12. Initial Bootstrap Behavior

For a new project, first establish the durable project framework and inspect any existing material.

Do not fabricate a detailed implementation `TASKS.md` from assumptions.

You may create the task structure, task conventions, Current Handoff template, and project-foundation entries needed to establish the system.

Before constructing the actual implementation task tree, gather the project information required to do it accurately.

Review anything already known first so you do not ask the owner to repeat information that is already available.

Then ask the owner a focused project intake covering whatever remains unknown, including:

1. What is the ultimate project goal, in plain language?
2. What would make the owner consider the project successfully finished?
3. What currently exists, works, partially works, or has already been attempted?
4. What outcomes are required, optional, or explicitly outside the project scope?
5. What hardware, software, services, repositories, environments, tools, data, or other components are already involved?
6. What versions, models, revisions, firmware, operating systems, or dependency information is known?
7. How do the known components currently connect or interact?
8. Where will the work actually run, and what machines, devices, storage, networks, or remote-access methods are relevant?
9. What important configuration is already known?
10. What resources, source material, external files, credentials, subscriptions, licenses, or equipment may be required? Ask only for credential binding information, never secret values.
11. What constraints apply, including safety, cost, time, storage, compatibility, destructive actions, production systems, or operations requiring explicit approval?
12. What tests, measurements, demonstrations, outputs, or other evidence should prove that the final project works?
13. What known blockers, unresolved decisions, previous failures, or owner preferences should influence the plan?
14. What additional questions are necessary based specifically on what you discovered in the repository?

Ask only questions whose answers materially affect the project environment, dependencies, success criteria, or task plan. Do not interrogate the owner about information already established. Once the answers are received, record the durable facts in the appropriate project files and build `TASKS.md` into a complete hierarchical goal tree with stable IDs, dependencies, small executable leaves, observable completion checks, and an accurate Current Handoff.
