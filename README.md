# Managing Stress for Students

## Group Members
Dave  
Qodi  
Aaron  

## Project Description
This project helps students manage their stress from school in simple ways. We created a poster that shows stress tips like taking breaks, sleeping well, and organizing tasks. The poster is easy to understand and visually friendly, so students can quickly learn how to handle stress.

## Goal
To help students stay healthy and do better in school by controlling stress. The project aims to make stress management simple and practical, so students can apply the tips in their daily life.

## Updated Features
- Time management tips for students  
- Stress-relief exercises  
- Poster draft with illustrations  
- Updated code for interactive tips  

## Methodology
- Tips displayed on the frontend for students to read  
- Poster created in Canva, uploaded as PDF  
- Backend handles tip selection based on user input  
- Code tested locally for functionality and errors  

## Code Examples
```python
import tkinter as tk
from tkinter import messagebox

BG = "#0f172a"
CARD = "#1e293b"
TEXT = "#e2e8f0"
ACCENT = "#22c55e"
WARN = "#f59e0b"
DANGER = "#ef4444"

def sleep_tip(hours):
    if hours < 0 or hours > 12:
        return "Invalid sleep input.\nRange: 0–12 hours."
    elif hours < 5:
        return "Low sleep.\nScience: Increases cortisol and reduces focus."
    elif hours < 8:
        return "Moderate sleep.\nScience: Improves memory and learning."
    else:
        return "Good sleep.\nScience: Boosts brain recovery and mood."

def stress_tip(level):
    if level == 0:
        return "Low stress.\nScience: Stable cortisol improves clarity."
    elif level == 1:
        return "Moderate stress.\nScience: Can improve short-term alertness."
    else:
        return "High stress.\nScience: Long-term stress harms health."

def hydration_tip(water):
    if water < 0 or water > 20:
        return "Invalid water input.\nRange: 0–20 cups."
    elif water < 3:
        return "Low hydration.\nScience: Causes fatigue and poor focus."
    elif water < 6:
        return "Moderate hydration.\nScience: Supports brain function."
    else:
        return "Good hydration.\nScience: Improves energy and cognition."

def mood_tip(mood):
    mood = mood.lower().strip()
    if mood == "happy":
        return "Happy.\nScience: Increases dopamine."
    elif mood == "neutral":
        return "Neutral.\nScience: Balanced emotional state."
    elif mood == "stressed":
        return "Stressed.\nScience: Raises cortisol levels."
    return "Mood not recognized."

def score(hours, stress, water):
    s = 0
    if hours >= 8:
        s += 4
    elif hours >= 5:
        s += 2
    else:
        s += 1

    if stress == 0:
        s += 3
    elif stress == 1:
        s += 2
    else:
        s += 1

    if water >= 6:
        s += 3
    elif water >= 3:
        s += 1

    return s

def feedback(s):
    if s >= 9:
        return "Excellent wellness"
    elif s >= 6:
        return "Good wellness"
    return "Needs improvement"

def validate(h, w):
    if h > 12:
        return False, "Sleep cannot exceed 12 hours"
    if w > 20:
        return False, "Water cannot exceed 20 cups"
    return True, ""

def run():
    try:
        h = float(sleep_entry.get())
        w = int(water_entry.get())
        m = mood_entry.get()
        s = int(stress_var.get())

        ok, msg = validate(h, w)
        if not ok:
            messagebox.showwarning("Invalid Input", msg)
            return

        result = (
            "WELLNESS REPORT\n\n"
            f"{sleep_tip(h)}\n\n"
            f"{stress_tip(s)}\n\n"
            f"{hydration_tip(w)}\n\n"
            f"{mood_tip(m)}\n\n"
        )

        sc = score(h, s, w)
        result += f"Score: {sc}/10\n{feedback(sc)}"

        result_label.config(text=result)
        history.insert(tk.END, f"{sc}/10 | Sleep:{h}h | Water:{w}")

    except:
        messagebox.showerror("Error", "Invalid input")

def clear():
    sleep_entry.delete(0, tk.END)
    water_entry.delete(0, tk.END)
    mood_entry.delete(0, tk.END)
    stress_var.set("0")
    result_label.config(text="")

def remove():
    try:
        history.delete(history.curselection())
    except:
        pass

root = tk.Tk()
root.title("Stress Management Program")
root.geometry("550x700")
root.configure(bg=BG)

title = tk.Label(
    root,
    text="Stress Management Program",
    bg=BG,
    fg=TEXT,
    font=("Arial", 16, "bold")
)
title.pack(pady=10)

input_card = tk.Frame(root, bg=CARD, padx=15, pady=15)
input_card.pack(padx=15, pady=10, fill="x")

tk.Label(input_card, text="Sleep Hours (0–12)", bg=CARD, fg=TEXT).pack(anchor="w")
sleep_entry = tk.Entry(input_card)
sleep_entry.pack(fill="x", pady=5)

tk.Label(input_card, text="Stress Level", bg=CARD, fg=TEXT).pack(anchor="w")
stress_var = tk.StringVar(value="0")

stress_frame = tk.Frame(input_card, bg=CARD)
stress_frame.pack()

tk.Radiobutton(stress_frame, text="Low", variable=stress_var, value="0", bg=CARD, fg=TEXT, selectcolor=BG).pack(side="left")
tk.Radiobutton(stress_frame, text="Medium", variable=stress_var, value="1", bg=CARD, fg=TEXT, selectcolor=BG).pack(side="left")
tk.Radiobutton(stress_frame, text="High", variable=stress_var, value="2", bg=CARD, fg=TEXT, selectcolor=BG).pack(side="left")

tk.Label(input_card, text="Water Intake (cups 0–20)", bg=CARD, fg=TEXT).pack(anchor="w")
water_entry = tk.Entry(input_card)
water_entry.pack(fill="x", pady=5)

tk.Label(input_card, text="Mood (happy / neutral / stressed)", bg=CARD, fg=TEXT).pack(anchor="w")
mood_entry = tk.Entry(input_card)
mood_entry.pack(fill="x", pady=5)

btn_frame = tk.Frame(root, bg=BG)
btn_frame.pack(pady=10)

tk.Button(btn_frame, text="Analyze", command=run, bg=ACCENT, fg="black", width=12).grid(row=0, column=0, padx=5)
tk.Button(btn_frame, text="Clear", command=clear, bg=WARN, fg="black", width=10).grid(row=0, column=1, padx=5)
tk.Button(btn_frame, text="Remove", command=remove, bg=DANGER, fg="white", width=10).grid(row=0, column=2, padx=5)

result_card = tk.Frame(root, bg=CARD, padx=15, pady=15)
result_card.pack(padx=15, pady=10, fill="both", expand=True)

result_label = tk.Label(
    result_card,
    text="",
    bg=CARD,
    fg=TEXT,
    justify="left",
    wraplength=480
)
result_label.pack()

tk.Label(root, text="History", bg=BG, fg=TEXT).pack()
history = tk.Listbox(root, height=6, bg=CARD, fg=TEXT)
history.pack(padx=15, pady=10, fill="both")

root.mainloop()
