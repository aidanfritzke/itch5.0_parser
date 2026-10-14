# 1.0 Functional Requirements

- **F-001** - The module shall implement an ITCH5.0 parser that decodes all message types, simulation only, 10Gb/s throughput, ultra low latency.
- **F-002** - The module shall run on 322.265625 MHz clock.
- **F-003** - The module shall implement 32 bit AXI-Stream for input data path. 
- **F-004** - The module shall accept bare ITCH messages as input.
- **F-005** - The module shall always accept input and never apply backpressure. Messages are packed back to back and can start at any of the 4 byte positions in a 32-bit word.
- **F-006** - The module shall output a stream of normalized, fixed-width book-update commands. It shall emit one, roughly 260 bit long, command per order-affecting ITCH message (Add, Execute, Cancel, Delete and Replace), and drop all other message types.
- **F-007** - The module shall output one registered command with no backpressure. It carries the command type, stock locate, timestamp, order reference, new order reference, buy/sell, shares, price, and valid signal
- **F-008** - The module shall take 1 clock cycles to output after the cycle carrying the input messages last byte.
- **F-009** - The module shall never be stalled on an error, but will count them.

## 1.1 Non-Functional Requirements

- **NF-001** - Comments-by-humans shall gate any output from the LLM: RTL, TBs, constraints, TCL, Python, .md's, etc, every file, including docs, CI YAML, the VSG config and constraints, all written through comments-by-humans:build, unless the file extension is in the comments-by-humans exempt list.
- **NF-002** - The FPGA repository shall implement CI/CD. See Section 1.2 for CI/CD, Testbench, and Functional Coverage guidelines.
- **NF-003** - The repo shall use VUnit as the test runner, NVC as the simulator. OSVVM for verification libraries. GTKWave for waveform viewing. VSG for linting. VSG shall enforce coding, naming, and formatting conventions.
- **NF-004** - The test data and reference model can be found XXXXXXX.

## 1.2 CI/CD, Testbenches, and Functional Coverage Guidelines

### 1.2.1 CI/CD

- Lint on every push.
- Unit sims on a pull request merged into master.

### 1.2.2 Testbenches

- One testbench per module.
- Directed cases include but not limited to: corrupted message
- Constrained random on frame length, message count, error inject.
- Trace each functional requirement to a test case tagged with its ID, including latency & determinism checks.

### 1.2.3 Functional Coverage

- Statement & branch: 100% (reviewed exclusions).
- FSM: every state & transition.
- Functional: every bin defined from directed case list.

## 1.3 VSG Standards

VHDL-2008, numeric_std only.
Lowercase keywords, 2-space indent.
One entity per file, with the file named after the entity.
snake_case: file name, packages
Architecture names should mirror file name.
Testbench names should mirror the file name it is testing, with _tb at the end.
UPPER_SNAKE_CASE: constant
camelCase: signal, generic, type, variable, process, enumeration literals, ports, instance labels and record fields
camelCase name suffixes: In/Out on ports (last suffix if multiple apply), Var on variables, Proc on processes, R on signals that are registered
Synchronous, active-high resets for control registers, data registers have no reset.
Always declare components.

## 1.4 Tool/Build Environment

### 1.4.1 Tool Versions



### 1.4.2 Environment Paths
