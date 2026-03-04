---
name: bullet3-index
description: This skill should be used when users ask how to use bullet3 and the correct generated documentation skill must be selected before going deeper into source code.
---

# bullet3 Skills Index

## Route the request
- Classify the request into one of the generated topic skills listed below.
- Prefer abstract, workflow-level guidance for large scientific packages; do not attempt full function-by-function coverage unless explicitly requested.

## Generated topic skills
- `bullet3-examples-and-tutorials`: Examples and Tutorials (worked examples, tutorials, and cookbook usage)
- `bullet3-build-and-install`: Build and Install (build, installation, compilation, and environment setup)
- `bullet3-simulation-workflows`: Simulation Workflows (simulation setup, execution flow, and runtime controls)
- `bullet3-api-and-scripting`: API and Scripting (language bindings, APIs, and programmatic interfaces)
- `bullet3-inputs-and-modeling`: Inputs and Modeling (inputs, system setup, models, and physical parameterization)
- `bullet3-test`: Test (documentation grouped under the 'test' theme)

## Documentation-first inputs
- `docs`
- `examples/pybullet/gym/pybullet_envs/deep_mimic/mocap`
- `examples/pybullet/gym/pybullet_envs/minitaur/envs`

## Tutorials and examples roots
- `examples`

## Test roots for behavior checks
- `test`
- `Extras/VHACD/test`
- `examples/pybullet/unittests`

## Escalate only when needed
- Start from topic skill primary references.
- If those references are insufficient, open the topic doc map directly:
- `skills/bullet3-build-and-install/references/doc_map.md`
- `skills/bullet3-api-and-scripting/references/doc_map.md`
- `skills/bullet3-inputs-and-modeling/references/doc_map.md`
- `skills/bullet3-simulation-workflows/references/doc_map.md`
- `skills/bullet3-examples-and-tutorials/references/doc_map.md`
- `skills/bullet3-test/references/doc_map.md`
- If documentation still leaves ambiguity, open the matching topic source map:
- `skills/bullet3-build-and-install/references/source_map.md`
- `skills/bullet3-api-and-scripting/references/source_map.md`
- `skills/bullet3-inputs-and-modeling/references/source_map.md`
- `skills/bullet3-simulation-workflows/references/source_map.md`
- `skills/bullet3-examples-and-tutorials/references/source_map.md`
- `skills/bullet3-test/references/source_map.md`
- Use targeted symbol search while inspecting source (e.g., `rg -n "<symbol_or_keyword>" Extras src examples/pybullet`).

## Source directories for deeper inspection
- `Extras`
- `src`
- `examples/pybullet`
