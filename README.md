# mBot2 Parallel Logic Optimization
**Project Focus:** Decoupling Hardware Outputs & Multi-threaded Logic

## 📖 Description
This project was born from a refusal to accept a "Standard Hardware Limitation." During the execution of a high-complexity navigation task, I identified a **Sequential Blocking Bug**: the mBot2 would pause all motor movement while executing audio signals (`click`) or LED transitions.

While this behavior is considered "standard" for basic block coding, I found it unacceptable for high-performance robotics. I re-engineered the system architecture to allow for **simultaneous movement and feedback.**

---

## 📈 The Evolution of the Logic

### 1. The Legacy Hierarchy (Sequential)
Initially, the code followed a linear path. 
* **The Problem:** The processor would "hang" on the sound block.
* **Status:** Failed Performance Audit.

### 2. Parallel Alpha (Broadcasting)
I implemented the `Message` block system to trigger the sound and movement in two separate threads. 
* **The Result:** The bot began moving while making sound, but the logic felt "heavy" and required too many custom blocks.

### 3. Final Form: The State Machine (Variable Listener)
The final optimization uses a **Global State Variable** (`leds`). 
* **Logic:** The main thread only changes a number. A background "Listener" loop (running in parallel) watches that number and triggers the hardware instantly.
* **Efficiency:** This is the cleanest, most responsive version of the code.

---

## 🖼️ Visual Logic Breakdown

| Version | Logic Type | Description |
| :--- | :--- | :--- |
| **Alpha** | Sequential | [<img width="1061" height="1205" alt="Screenshot 2026-05-09 233657" src="https://github.com/user-attachments/assets/8cbc0f56-95bc-4d0d-9daa-6f38f559c0e3" />
] |
| **Beta** | Message-Based | [<img width="961" height="1088" alt="Screenshot 2026-05-09 234051" src="https://github.com/user-attachments/assets/8d7bfc9d-bd27-404f-a0ea-d014e2c2eab7" />
] |
| **Final** | State Variable | [<img width="983" height="1130" alt="Screenshot 2026-05-09 234248" src="https://github.com/user-attachments/assets/b203652d-5cf1-4285-a712-b90d75417f7a" />
] |

---

## 🛠️ Technical Implementation
* **Hardware:** CyberPi + mBot2 Shield
* **Concepts:** Multithreading, State Management, Asynchronous Execution.
* **Optimization:** 100% Latency Reduction in Motor-to-Audio sync.
