
# STM32 Task Scheduler Using PendSV and PSP

This project demonstrates a basic task scheduler on STM32, using the PendSV exception and Process Stack Pointer (PSP) for context switching between two tasks.

## 📌 Features

- Two tasks running on STM32.
- Manual context switching using PendSV.
- Stack management using Process Stack Pointer (PSP).
- Demonstrates how CPU and software share context saving:
  - **CPU automatically saves**: R0–R3, R12, LR, PC, xPSR.
  - **PendSV handler saves/restores**: R4–R11.

## 🧠 How It Works

1. **SysTick interrupt** triggers at a fixed interval.
2. In the SysTick handler, PendSV is **pended manually**.
3. When PendSV runs:
   - It **saves R4–R11** of the current task to its stack (PSP).
   - It **switches the PSP** to the next task.
   - It **restores R4–R11** of the next task from its PSP stack.
   - On exiting PendSV, the CPU restores the remaining registers and resumes the next task.