# IoT Health Monitoring System Proposal

## Project Overview
This proposal outlines the development of an IoT-based Health Monitoring System using Rust, designed to monitor patient vital signs (heart rate, body temperature) and send real-time alerts (email/SMS) when readings exceed critical thresholds. A panic button allows patients to trigger emergency notifications. Data is stored on a cloud server (e.g., ThingSpeak) and visualized via a web dashboard. The system leverages Rust’s memory safety and performance for reliable device and server code, targeting completion of a minimum viable product (MVP) within 30 days.

### Objectives
- Develop a Rust-based IoT device to collect heart rate and temperature data.
- Implement a backend server for data processing and storage.
- Enable real-time alerts via email/SMS for critical readings.
- Provide a web dashboard for data visualization.
- Ensure system reliability, security, and scalability using Rust.

### Scope
- **Hardware**: Raspberry Pi Pico (or ESP32), pulse sensor, DS18B20 temperature sensor, panic button.
- **Software**: Rust firmware for device, Rust backend server, MQTT for communication, web dashboard (HTML/CSS/JS or Leptos).
- **Features**:
  - Real-time vital sign monitoring.
  - Threshold-based alerts (email/SMS).
  - Panic button for emergency notifications.
  - Cloud storage and historical data access.
  - Web dashboard for visualization.
- **Constraints**: 30-day timeline, single developer or small team, focus on MVP.

### Justification
Health monitoring is critical due to increasing healthcare demands and busy lifestyles, making regular checkups challenging (). IoT enables continuous monitoring, reducing hospital visits and enabling remote patient tracking. Rust ensures safe, high-performance code for IoT devices and servers, minimizing bugs and crashes in critical applications.[](https://web.iitd.ac.in/~bmz198302/template/project/project_proposal.html)

## 30-Day Table of Contents (ToC)

| **Day** | **WBS** | **Task Name** | **Duration** | **Start** | **Finish** | **Deliverable** |
|---------|---------|---------------|--------------|-----------|------------|-----------------|
| 1-3     | 1.0     | **Project Setup** | 3 days | Day 1 | Day 3 | Project plan, tools installed |
|         | 1.1     | Define requirements and scope | 1 day | Day 1 | Day 1 | Requirements document |
|         | 1.2     | Research Rust IoT libraries (`embedded-hal`, `rumqttc`, `reqwest`) | 1 day | Day 2 | Day 2 | Library selection report |
|         | 1.3     | Set up development environment (Rust, `cargo`, cross-compilation) | 1 day | Day 3 | Day 3 | Dev environment configured |
| 4-7     | 2.0     | **Hardware Selection and Setup** | 4 days | Day 4 | Day 7 | Functional hardware prototype |
|         | 2.1     | Select microcontroller (Raspberry Pi Pico/ESP32) | 1 day | Day 4 | Day 4 | Hardware spec document |
|         | 2.2     | Configure sensors (pulse, DS18B20, panic button) | 2 days | Day 5 | Day 6 | Sensor wiring complete |
|         | 2.3     | Test hardware connectivity | 1 day | Day 7 | Day 7 | Hardware test report |
| 8-10    | 3.0     | **Software Framework Design** | 3 days | Day 8 | Day 10 | Software architecture |
|         | 3.1     | Design device firmware architecture (Rust, `embedded-hal`) | 1 day | Day 8 | Day 8 | Firmware design doc |
|         | 3.2     | Design backend server (Rust, `tokio`, `axum`) | 1 day | Day 9 | Day 9 | Backend design doc |
|         | 3.3     | Select cloud service (AWS IoT Core or custom MQTT server) | 1 day | Day 10 | Day 10 | Cloud setup complete |
| 11-18   | 4.0     | **Rapid Prototyping** | 8 days | Day 11 | Day 18 | Functional prototype |
|         | 4.1     | Implement device firmware (sensor reading, MQTT publish) | 3 days | Day 11 | Day 13 | Firmware code |
|         | 4.2     | Develop backend server (MQTT subscribe, data storage) | 3 days | Day 14 | Day 16 | Backend server code |
|         | 4.3     | Integrate panic button and alert system (email/SMS via `reqwest`) | 2 days | Day 17 | Day 18 | Alert system functional |
| 19-25   | 5.0     | **MVP Refinement and Testing** | 7 days | Day 19 | Day 25 | Refined MVP |
|         | 5.1     | Develop web dashboard (HTML/CSS/JS or Leptos) | 3 days | Day 19 | Day 21 | Dashboard prototype |
|         | 5.2     | Test sensor accuracy and alert reliability | 2 days | Day 22 | Day 23 | Test results |
|         | 5.3     | Optimize user experience (dashboard UI, alert timing) | 2 days | Day 24 | Day 25 | Optimized MVP |
| 26-30   | 6.0     | **Final Integration and Documentation** | 5 days | Day 26 | Day 30 | Final deliverable |
|         | 6.1     | Integrate hardware, firmware, and backend | 2 days | Day 26 | Day 27 | Integrated system |
|         | 6.2     | Perform end-to-end testing | 1 day | Day 28 | Day 28 | Test report |
|         | 6.3     | Document system (user manual, code docs) | 1 day | Day 29 | Day 29 | Documentation |
|         | 6.4     | Prepare for deployment and submit | 1 day | Day 30 | Day 30 | Deployed MVP |

## Technical Details
- **Hardware**:
  - **Microcontroller**: Raspberry Pi Pico (Rust-supported via `rp-hal`).
  - **Sensors**: Pulse sensor (e.g., SEN-11574), DS18B20 temperature sensor, push-button for panic.
  - **Connectivity**: Wi-Fi module (ESP32) or external USB Wi-Fi for Pico.
- **Software**:
  - **Firmware**: Rust with `embedded-hal` for sensor reading, `rumqttc` for MQTT.
  - **Backend**: Rust with `axum` for HTTP server, `tokio` for async, `sqlx` for database (e.g., SQLite).
  - **Cloud**: AWS IoT Core or Mosquitto MQTT broker.
  - **Dashboard**: Simple HTML/CSS/JS or Leptos (Rust web framework) for visualization.
  - **Alerts**: Email/SMS via `reqwest` (HTTP) or third-party APIs (e.g., Twilio).
- **Rust Libraries**:
  - `embedded-hal`: Hardware abstraction.
  - `rumqttc`: MQTT communication.
  - `serde`: Data serialization for cloud storage.
  - `reqwest`: HTTP requests for alerts.
  - `tokio`: Async runtime for backend.
  - `axum`: Web server framework.
- **Security**:
  - Encrypt MQTT communication with TLS.
  - Validate sensor data to prevent injection attacks.
  - Secure API endpoints with authentication (e.g., JWT).

## Milestones
- **Day 3**: Project setup and requirements defined.
- **Day 7**: Hardware prototype functional.
- **Day 10**: Software architecture designed.
- **Day 18**: Functional prototype with firmware, backend, and alerts.
- **Day 25**: Refined MVP with dashboard and tested features.
- **Day 30**: Fully integrated system, documented, and deployed.

## Risks and Mitigation
- **Risk**: Hardware compatibility issues with Rust.
  - **Mitigation**: Use well-documented boards (Pico/ESP32) and `embedded-hal`.
- **Risk**: Sensor data inaccuracies.
  - **Mitigation**: Calibrate sensors and implement error handling in firmware.
- **Risk**: Cloud service integration delays.
  - **Mitigation**: Start with a local MQTT broker, switch to AWS IoT Core later.
- **Risk**: Tight 30-day timeline.
  - **Mitigation**: Prioritize core features (sensor reading, alerts) for MVP.

## References
- Health monitoring system inspiration:[](https://web.iitd.ac.in/~bmz198302/template/project/project_proposal.html)
- IoT project ideas and hardware:[](https://www.projectpro.io/article/top-20-iot-project-ideas-for-beginners-in-2021/428)
- 30-day MVP development structure:[](https://sdh.global/blog/development/how-to-build-your-iot-mvp-in-30-days-a-practical-guide-for-2025/)
- Project timeline and Gantt chart:[](https://desklib.com/study-documents/iot-based-home-automation/)

## Next Steps
- Finalize hardware selection (Pico vs. ESP32).
- Set up Rust development environment with cross-compilation.
- Begin firmware development and sensor integration.
- Test MQTT connectivity and cloud storage early.