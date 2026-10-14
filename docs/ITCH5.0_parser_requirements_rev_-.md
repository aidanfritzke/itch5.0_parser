# 1.0 Requirements

- **001** - The module shall implement an ITCH5.0 parser that decodes all message types.
- **002** - The FPGA RTL shall be written in VHDL.
- **003** - Comments-by-humans shall gate any output from the LLM: RTL, TBs, constraints, TCL, Python, .md's, etc, every file, including docs, CI YAML, the VSG config and constraints, all written through comments-by-humans:build
- **004** - The FPGA repository shall implement CI/CD. See Section 1.2 for CI/CD, Testbench, and Functional Coverage guidelines.
- **005** - The repo shall use VUnit as the test runner, NVC as the simulator. OSVVM for verification libraries. GTKWave for waveform viewing. VSG for linting. Vivado in batch mode for builds. VSG shall enforce coding, naming, and formatting conventions.

## 1.1 Tool/Build Environment

## 1.2 CI/CD, Testbenches, and Functional Coverage Guidelines

### 1.2.1 CI/CD

- Lint on every push.
- Unit sims on every push.
- Full-chain sim on every merge.
- Vivado syn & par on every merge.
- Bitstreams & reports archived & tagged on release.

### 1.2.2 Testbenches

- One tb per module.
- Directed cases include but not limited to: bad CRC, runts, padding, minimum inter-frame gap.
- Constrained random on frame length, message count, error inject.
- Encode each req as an assertion for each functional requirement tagged with its ID, including latency & determinism checks.

### 1.2.3 Functional Coverage

- Statement & branch: 100% (reviewed exclusions).
- FSM: every state & transition.
- Functional: every bin defined from directed case list.

## 1.3 VSG Standards

VHDL-2008, numeric_std only.
Lowercase keywords, 2-space indent.
One entity per file, with the file named after the entity.
File names should be lowercase, underscores as spaces.
Architecture names should mirror file name.
Testbench names should mirror the file name it is testing, with _tb at the end.
UPPER_SNAKE_CASE: constant
camelCase: signal, generic, type, variable, process, component, etc
camelCase name suffixes: In/Out on ports (last suffix if multiple apply), Var on variables, Proc on processes, R on signals that are registered
Synchronous, active-high resets.

