
* 📅 **Day** – Day number
* 📘 **Topic** – Focus area for the day
* 📝 **Description** – What will be covered
* 🎯 **Outcome** – What you will be able to do after completing the day

---

### 📚 **30-Day Rust Learning Plan for IoT and Embedded Systems**

| 📅 Day | 📘 Topic                                   | 📝 Description                                                   | 🎯 Outcome                                                     |
| ------ | ------------------------------------------ | ---------------------------------------------------------------- | -------------------------------------------------------------- |
| 1      | Introduction to Rust                       | Install Rust, understand `cargo`, setup VS Code or preferred IDE | Able to compile and run a basic Rust program                   |
| 2      | Variables, Data Types & Mutability         | Learn about scalar & compound types, mutability                  | Use different types and control mutability effectively         |
| 3      | Functions and Control Flow                 | Define and use functions, conditionals, loops                    | Write clean, modular Rust code                                 |
| 4      | Ownership & Borrowing                      | Core Rust concept to manage memory                               | Avoid common bugs, understand lifetimes                        |
| 5      | References and Slices                      | Work with references, string & array slices                      | Prevent copying and manage memory safely                       |
| 6      | Structs and Methods                        | Define `struct`s and implement methods                           | Model sensor/device data with Rust structs                     |
| 7      | Enums and Pattern Matching                 | Use `enum` and `match` for logic control                         | Represent device states or input actions clearly               |
| 8      | Collections: Vectors and HashMaps          | Use dynamic collections to store data                            | Efficiently manage sensor readings or logs                     |
| 9      | Error Handling                             | Learn `Result`, `Option`, `unwrap`, `?` operator                 | Write robust and safe device logic                             |
| 10     | Modules & Crate Structure                  | Organize code into modules and use external crates               | Build scalable and reusable components                         |
| 11     | Traits and Generics                        | Implement polymorphism and abstraction                           | Design reusable sensor/actuator interfaces                     |
| 12     | Smart Pointers & Lifetimes                 | Dive into `Box`, `Rc`, and lifetimes                             | Understand heap allocation and ownership rules                 |
| 13     | File and Serial I/O                        | Read/write files and handle UART via serial port                 | Communicate with peripheral devices                            |
| 14     | Working with `no_std`                      | Learn about embedded constraints (`no_std` use)                  | Write Rust for bare-metal environments                         |
| 15     | Embedded HAL (Hardware Abstraction Layer)  | Use `embedded-hal` traits for hardware interaction               | Abstract over GPIO, PWM, SPI, I2C                              |
| 16     | Blinking LED on Microcontroller            | Run Rust on a board (e.g., STM32, RP2040, ESP32)                 | Successfully toggle GPIO pins                                  |
| 17     | Timers and Interrupts                      | Configure timers, handle basic interrupts                        | Perform non-blocking hardware tasks                            |
| 18     | GPIO Input (e.g., Button)                  | Read input from GPIO                                             | Implement simple user interfaces                               |
| 19     | UART Communication                         | Setup serial communication using embedded Rust                   | Send/receive data from sensors/modules                         |
| 20     | I2C Sensor Interface                       | Interact with temperature/acceleration sensor over I2C           | Collect real-world data from peripherals                       |
| 21     | SPI Interface                              | Communicate with SPI-based displays or memory                    | Master another bus protocol for peripherals                    |
| 22     | RTIC Framework Intro                       | Learn Real-Time Interrupt-driven Concurrency (RTIC)              | Build multitasking embedded applications                       |
| 23     | Logging and Debugging                      | Use `defmt`, `probe-rs`, semihosting                             | Debug and trace embedded programs                              |
| 24     | Power Management                           | Explore low-power modes, sleep, wake                             | Make devices battery-friendly                                  |
| 25     | Embedded Networking (e.g., Wi-Fi on ESP32) | Use embedded Rust with Wi-Fi capable boards                      | Enable device to connect to network                            |
| 26     | MQTT Communication                         | Connect IoT device to MQTT broker                                | Send sensor data to cloud services                             |
| 27     | Over-the-Air Updates (OTA) Concept         | Understand firmware updates over network                         | Enable remote update capabilities (theory + partial practical) |
| 28     | End-to-End Mini Project (Sensor Node)      | Build complete sensor system with data publishing                | Deploy working IoT prototype                                   |
| 29     | Rust on Raspberry Pi Pico (RP2040)         | Flash and interact with RP2040 in Rust                           | Expand board support & portability                             |
| 30     | Recap, Optimization & Next Steps           | Summarize learning, profile code, explore next libraries         | Be confident in using Rust for embedded/IoT projects           |

---
## ✅ **Final Project: Smart Environmental Monitoring IoT Node**

### 🔧 Project Description:

Create an **IoT device** that:

* **Reads temperature, humidity, and light intensity**
* **Displays values on an OLED screen**
* **Publishes data over Wi-Fi using MQTT**
* **Supports power-saving modes**
* Optional: Enable **firmware updates (OTA)** or **store data to SD card**

---

### 🏗️ **Project Architecture Overview:**

```
Sensor (I2C) → Microcontroller (Rust) → OLED Display (SPI/I2C)
                            ↓
                   Wi-Fi MQTT Publisher
                            ↓
                Cloud Dashboard or MQTT Broker
```

---

### 📋 **Prerequisites:**

#### 📌 Hardware:

| Component                     | Purpose                                   |
| ----------------------------- | ----------------------------------------- |
| ESP32 / RP2040 + Wi-Fi module | Core MCU with Wi-Fi capability            |
| DHT11 / DHT22                 | Temperature and Humidity Sensor (Digital) |
| BH1750 / LDR + ADC            | Light Intensity Sensor (I2C or analog)    |
| SSD1306 OLED Display          | Display readings (SPI/I2C)                |
| Push button                   | Manual trigger or mode switch             |
| USB to UART                   | Flash/debug firmware                      |
| Power Supply / Li-Ion Battery | Portable operation                        |
| Optional: SD Card Module      | Data logging                              |

#### 📌 Software:

| Tool                                                     | Description                           |
| -------------------------------------------------------- | ------------------------------------- |
| Rust with `cargo-generate`                               | Project scaffolding                   |
| `probe-rs`, `cargo-embed`                                | Flash and debug firmware              |
| `espflash` (for ESP32) or `rp2040-hal` (for RP2040)      | MCU-specific tooling                  |
| `mqtt-rs` or `rumqttc`                                   | MQTT client crates                    |
| `embedded-hal`, `dht-sensor`, `ssd1306`, `bh1750` crates | Hardware interfacing                  |
| MQTT Broker (Mosquitto or Cloud: Adafruit IO, HiveMQ)    | MQTT testing & dashboard              |
| Optional: Node-RED / Grafana                             | Dashboard for visualizing sensor data |

---

### 📈 **Project Timeline Mapping with TOC:**

| TOC Day   | Learning Outcome        | Project Contribution                |
| --------- | ----------------------- | ----------------------------------- |
| Day 6–7   | Structs, Enums, Match   | Sensor state & modes                |
| Day 13    | Serial I/O              | Debugging and sensor testing        |
| Day 15–17 | GPIO, Timer, Interrupts | LED/Buzzer indicator, sleep wake-up |
| Day 20–21 | I2C, SPI                | Sensor and display communication    |
| Day 25–26 | Networking & MQTT       | Data publishing to cloud            |
| Day 28    | Mini Project            | Start implementation                |
| Day 30    | Optimization            | Power saving, OTA, polish code      |

---

### 🎯 **Final Project Outcomes:**

* 📶 Embedded Rust application that interacts with multiple peripherals
* 🌐 Cloud-enabled smart sensor node using MQTT
* 💡 Understanding of `embedded-hal`, real-time constraints, and `no_std`
* 🔌 Low-power operation and modular code design
* 📈 Potential for scaling into a larger Smart Home or Industrial IoT solution

---

Note:

✅ All hardware and peripherals will be provided by the vendor.  
✅ Students must bring their own laptop/desktop.  
✅ Duration: 30 days × 6 hours/day = 180 hours.  
✅ Mode: Offline  
✅ Commercials: ₹900/hour × 180 hours = ₹1,62,000/-
✅ Contact : anirudhagaikwad@hotmail.com
