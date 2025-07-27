### 📚 30-Day Rust Fundamentals Learning Plan – Practical Software Development Approach

| 📅 Day | 📘 Topic                          | 📝 Description                                                  | 🎯 Outcome                                           |
| -----: | --------------------------------- | --------------------------------------------------------------- | ---------------------------------------------------- |
|      1 | Rust Setup & Tooling              | Install Rust, setup `cargo`, configure IDE (VS Code, IntelliJ)  | Able to compile & run a Rust program                 |
|      2 | Hello Rust!                       | Write your first program, understand `main()` and basic syntax  | Comfortable writing and running simple Rust programs |
|      3 | Variables & Data Types            | Learn `let`, `mut`, scalar and compound types                   | Confidently declare and use typed variables          |
|      4 | Functions and Comments            | Define functions, understand scopes, and use comments           | Modularize code with clear documentation             |
|      5 | Control Flow                      | Use `if`, `else`, `match`, loops                                | Build logic using branching and repetition           |
|      6 | Ownership Basics                  | Understand move semantics, ownership, and scope                 | Prevent memory errors using ownership rules          |
|      7 | Borrowing and References          | Learn `&`, `&mut`, and reference rules                          | Pass variables safely without transferring ownership |
|      8 | Slices and String Handling        | Work with string slices, indexing, and string operations        | Manipulate text data efficiently                     |
|      9 | Structs                           | Define and use `struct`s with associated data                   | Model real-world entities                            |
|     10 | Enums and Pattern Matching        | Use `enum`, `Option`, `Result`, and `match`                     | Handle multiple data states and errors               |
|     11 | Collections: Vectors and HashMaps | Work with dynamic arrays and key-value pairs                    | Store and retrieve runtime data effectively          |
|     12 | Error Handling                    | Practice using `Result`, `unwrap`, `expect`, and `?`            | Write safe and resilient code                        |
|     13 | Modules and Visibility            | Organize code into modules, control visibility with `pub`       | Structure projects into reusable parts               |
|     14 | Cargo & Crates                    | Use external libraries with `cargo`, explore `crates.io`        | Integrate open-source libraries                      |
|     15 | Traits and Interfaces             | Understand `trait`, `impl`, and polymorphism                    | Implement generic, flexible code                     |
|     16 | Generics                          | Use generics for type abstraction                               | Build reusable and type-safe components              |
|     17 | Lifetimes Basics                  | Understand lifetime annotations and borrowing rules             | Prevent dangling references in larger codebases      |
|     18 | Smart Pointers: Box, Rc           | Learn `Box<T>`, `Rc<T>`, and their use cases                    | Manage heap data and shared ownership                |
|     19 | File I/O Basics                   | Read/write text and binary files                                | Build CLI tools that persist data                    |
|     20 | Command Line Interface (CLI) Apps | Use `clap` or `structopt` to build CLI apps                     | Create real-world tools with argument parsing        |
|     21 | Testing in Rust                   | Write unit tests with `#[test]`, `assert_eq!`, and test modules | Ensure code correctness with automated testing       |
|     22 | Iterators and Closures            | Work with iterators, adaptors, closures                         | Write concise, expressive transformations on data    |
|     23 | Error Propagation & Logging       | Implement layered error handling, use `log` crate               | Track errors and program flow                        |
|     24 | Concurrency & Threads             | Spawn threads, use `Mutex`, `Arc`                               | Write basic multithreaded applications               |
|     25 | Working with JSON                 | Use `serde` for JSON serialization/deserialization              | Build APIs and data-driven software                  |
|     26 | Building a Mini Project (Part 1)  | Plan and start a small CLI or server-side project               | Apply your learning in real code                     |
|     27 | Building a Mini Project (Part 2)  | Continue implementation and add real features                   | Handle input, storage, error flow                    |
|     28 | Project Finalization              | Test, optimize, refactor, and document                          | Deliver production-quality code                      |
|     29 | Performance Tips                  | Benchmarking with `criterion`, profiling tips                   | Improve speed and memory usage                       |
|     30 | Next Steps & Rust Ecosystem       | Explore WebAssembly, IOT-embedded, async, actix, and Leptos         | Path forward for domain-specific deep dive           |

---

> 🧑‍🏫 **Goal**: Build solid Rust foundation to develop reliable, maintainable, and safe software.
> ✅ Includes hands-on activities, daily exercises, and weekly challenges.
> 📁 All code can be version-controlled via Git and shared on GitHub.

---

## 🧪 Final Project: Build a Command-Line Task Manager

**Title**: `rusty-tasker`

**Overview**: Build a CLI-based task management application in Rust where users can add, view, edit, and delete tasks. Store the data in a JSON file.

### ✨ Features
- Add new tasks with title, priority, and due date
- View task list sorted by due date or priority
- Mark tasks as completed
- Save/load tasks from a JSON file using `serde`
- Clean, modular code structure using `modules`, `traits`, and `error handling`

### 🛠️ Technologies & Concepts Used
- `serde`, `serde_json` for data serialization
- `chrono` crate for date/time management
- CLI argument parsing with `clap` or `structopt`
- `Result`, `Option`, error handling
- File I/O, lifetimes, enums, structs

### ✅ Final Outcome
A fully functional, user-friendly CLI app that reinforces your entire Rust learning—ready to extend into a web app or a TUI interface using `tui-rs` or `egui`.

---

Note:  
✅ Students must bring their own laptop/desktop.  
✅ Duration: 30 days × 6 hours/day = 180 hours.  
✅ Mode: Offline  
✅ Commercials: ₹600/hour × 180 hours = ₹108,000/-
✅ Contact : anirudhagaikwad@hotmail.com
