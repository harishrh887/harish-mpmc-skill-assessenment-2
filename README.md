Write an assembly language program in 8051 to generate a 100 ms delay using Timer 1 in Mode 2 and toggle Port 2.5 continuously.
## AIM
To Write an assembly language program in 8051 to generate a 100 ms delay using Timer 1 in Mode 2 and toggle Port 2.5 continuously.

---

## APPARATUS REQUIRED
- Personal computer with dosbox software

---

## ALGORITHM
1 Start the program.

2 Initialize the timer:

Set Timer 1 in Mode 2 (8-bit auto-reload mode)
→ MOV TMOD, #20H

Load TH1 = 00H (auto-reload value for the timer).

Clear the Timer 1 overflow flag (TF1).

Start Timer 1 by setting the TR1 bit.

3 Enter the main loop (MAIN_LOOP):

Load registers R2 and R3 with initial count values (R2 = 87H, R3 = 01H).
These registers control how many timer overflows are used to create the total delay.

4 Delay generation loop (WAIT_OVF):

5 Wait for Timer 1 to overflow:

Continuously check the TF1 flag using JNB TF1, $
(this instruction keeps checking until TF1 = 1).

6 Once overflow occurs:

Clear the TF1 flag.

Decrement R2.

If R2 ≠ 0, repeat the overflow waiting loop.

When R2 = 0, decrement R3 and repeat until R3 = 0.

This double-loop structure extends the delay time.

7 After the delay:

Toggle the output pin P2.5 using CPL P2.5
(if it was 0, it becomes 1, and vice versa).

---



## PROGRAM
```asm
ORG 0000H
LJMP START

START:
    MOV TMOD, #20H
    MOV TH1, #00H
    CLR TF1
    SETB TR1

MAIN_LOOP:
    MOV R2, #087H
    MOV R3, #01H

WAIT_OVF:
    JNB TF1, $
    CLR TF1
    DJNZ R2, WAIT_OVF
    DJNZ R3, WAIT_OVF

    CPL P2.5
    SJMP MAIN_LOOP

END

```
OUTPUT

![WhatsApp Image 2025-10-27 at 22 54 00_f4bcc196](https://github.com/user-attachments/assets/3c6689ff-f5cf-4e47-96b3-6376fcc45a9f)



---


RESULT

Thus the program continuously toggles **Port 2.5** every ~37 milliseconds using **Timer 1 in Mode 2**.


---


