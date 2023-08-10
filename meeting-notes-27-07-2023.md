## Agenda

- **Adoption into other runtimes**
- **Governance, any ideas**?
  - Ideally, everything should happen in the open.
  - Stability
  - Do not reinvent the wheel
- Technical discussion
  - Current implementation of WASIX
  - It’s growth
  - It’s further implementation in various runtimes

### Meeting Attendees:

- Syrus Akbary - Founder of Wasmer (Meeting head)
  - Email: [syrus@wasmer.io](mailto:syrus@wasmer.io)
- Christoph Herzog - Software Engineer working at Wasmer Edge and WASIX
- Rudra - Engineer at Wasmer
- Frank Denis - Software Engineer/photographer & maintainer of Zig and their implementation of WASI - also working on WASI crypto
- Eduardo - (Full name @Syrus Akbary ) - Maintainer of Wazero runtime (Go)

## Governance Decisions:

| Question                                                                             | Decision                                                                               |
| ------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------- |
| Can the meeting sessions be recorded from the next meeting?                          | ✅ (Can record the video)                                                              |
| Focus of WASIX Meetings ?                                                            | ℹ️ Technical discussions , fast pace, keeping WASIX stable and no politics/bureaucracy |
| Decision making for issues/features                                                  | ℹ️ In the Open/publicly on GitHub                                                      |
| Should other runtime implementors be added to http://WASIX.org’s GitHub organization | ✅ (from both Frank and Eduardo)                                                       |
| Meeting Schedule                                                                     | 🚨 Once per month                                                                      |

## Technical statements and questions about WASIX

- 100% compatible with WASI Preview 1
- Right now there's an implicit implementation of WASIX
- Partition for WASIX on different functionality such as `threading`, `forking`, `networking` ?
- `@wasmer/wasix` needs development
- WASM has linear memory so it doesn’t implement any memory security
- `mmap` is required as it is missing from wasm
  - it is required for better memory management
  - never being able to shrink wasm's memory
  - Fully properly implementing mmap for `wasm`
  - `mmap` is currently implemented using `asyncify`
- No test suite in WASI so that's why wazero implemented their own test suite
- Wazero doesn't wants to go through c-go
- `longjmp`/`setjmp` depends on `asyncify` belong in processing plugin
- `Zig` implementation of WASIX can really fast forward the development of C programs/applications for WASIX
- Wasmer will **help** Zig and Wazero implementors with WASIX implementation if they require any **help**
- Discussion on how [wasmer.sh](http://wasmer.sh) works:
  - Networking using Virtual-network
  - File system using Virtual-FS
  - multiplexed I/O using Virtual-mio
- WASIX works for both browser and system level so virtual crates can be considered by Zig and Wazero if they want to keep a consistency
- wasi-crypto proposal is from Frank Denis and that only works in WasmEdge which would now also be removed.
- Pain points about wasi-preview-2 and WASI:
  - The new component architecture discards everything that has been worked on.
  - WASI already took 3 years for it’s implementation in Node.
- Our roadmap should support end users (supporting them regardless of the use cases)
  - WASI Preview 2
  - Waste too much time on supporting both
  - WASIX is trying to embrace a lot of different concerns (partition). Should we partition?
  - WASIX is a lot of work (couple months). Partition (sockets). Base WASIX (thread spawning).
    - Sockets
    - Threads
    - Signals
    - Process stack (fork, process management) - depends on `asyncify`
  - Inherited the small mmap emulated layer (mmap emulation layer)
  - WASI Preview 1 is not available in every single runtime
  - Bias towards Rust
  - Proc done (protected memory) - malloc (linear memory)
  - Need more wide adoption - How to make it easy to people to use WASIX / implement WASIX. More support (more runtimes) ?

## Technical Actions:

- `@wasmer/wasix` npm package needs to be published
- `mmap` needs a go through in WASIX and needs a better implementation
- Do we need a test suite for WASIX on the Rust(wasmer) side ?
- Wasmer will help Zig/wazero with their implementation of WASIX
- Another discussion on the plugin system
- Need more wide adoption - How to make it easy to people to use WASIX / implement WASIX
