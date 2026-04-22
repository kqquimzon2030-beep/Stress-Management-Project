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
# import tkinter as tk
from tkinter import messagebox

def sleep_tip(hours_slept):
    if hours_slept < 0:
        return "That's not a valid number of hours!"
    elif hours_slept < 5:
        return "You slept very little! Take a short nap and rest. Lack of sleep can increase stress levels and reduce focus."
    elif 5 <= hours_slept < 8:
        return "You got some sleep, but try to sleep more tonight for full recovery. Consistent sleep improves mood and energy."
    else:
        return "Great! You got enough sleep. Keep it up for a healthy routine and better stress control."


def stress_tip(level):
    tips = [
        "You're feeling relaxed. Maintain this by keeping a balanced routine and taking short breaks.",
        "Moderate stress detected. Try organizing your tasks and take breaks to avoid burnout.",
        "High stress detected! Consider deep breathing, short walks, or talking to someone you trust."
    ]

    if level < 0 or level >= len(tips):
        return "Invalid stress level selected."
    return tips[level]


def hydration_tip(cups):
    if cups < 3:
        return "You need more water. Dehydration can increase fatigue and stress. Aim for at least 6–8 cups daily."
    elif 3 <= cups < 6:
        return "You're doing okay, but drinking more water can improve focus and energy levels."
    else:
        return "Great hydration! Staying hydrated helps regulate mood and body functions."


def mood_tip(mood):
    mood = mood.lower()
    if mood == "happy":
        return "Nice! Keep doing what makes you feel good and maintain your positive habits."
    elif mood == "neutral":
        return "You're feeling okay. Try doing something enjoyable like listening to music or relaxing."
    elif mood == "stressed":
        return "You're feeling stressed. Try deep breathing, journaling, or taking a short break."
    else:
        return "Mood not recognized, but remember to take care of yourself and rest when needed."


def calculate_score(hours, stress, water):
    score = 0

    if hours >= 8:
        score += 4
    elif hours >= 5:
        score += 2

    score += (2 - stress)

    if water >= 6:
        score += 3
    elif water >= 3:
        score += 1

    return score


def wellness_feedback(score):
    if score >= 8:
        return "Excellent wellness! You're taking great care of yourself."
    elif 5 <= score < 8:
        return "Good job! There are a few areas you can still improve."
    else:
        return "You might need to focus more on your health and stress management."


def get_results():
    try:
        hours = float(entry_sleep.get())
        stress_level = int(stress_var.get())
        water = int(entry_water.get())
        mood = entry_mood.get()

        sleep_message = sleep_tip(hours)
        stress_message = stress_tip(stress_level)
        water_message = hydration_tip(water)
        mood_message = mood_tip(mood)

        score = calculate_score(hours, stress_level, water)
        feedback = wellness_feedback(score)

        result_label.config(
            text=(
                f"--- RESULTS ---\n\n"
                f"Sleep Tip:\n{sleep_message}\n\n"
                f"Stress Tip:\n{stress_message}\n\n"
                f"Hydration Tip:\n{water_message}\n\n"
                f"Mood Tip:\n{mood_message}\n\n"
                f"Wellness Score: {score}/10\n"
                f"Feedback: {feedback}"
            )
        )

    except ValueError:
        messagebox.showerror("Input Error", "Please enter valid inputs.")


root = tk.Tk()
root.title("Advanced Stress & Sleep Helper")
root.geometry("500x550")
root.resizable(False, False)

title_label = tk.Label(root, text="Stress & Sleep Wellness Checker", font=("Arial", 16, "bold"))
title_label.pack(pady=10)

tk.Label(root, text="Hours of sleep:").pack()
entry_sleep = tk.Entry(root)
entry_sleep.pack(pady=5)

tk.Label(root, text="Stress Level:").pack()
stress_var = tk.StringVar(value="0")

frame = tk.Frame(root)
frame.pack()

tk.Radiobutton(frame, text="Low (0)", variable=stress_var, value="0").pack(anchor='w')
tk.Radiobutton(frame, text="Medium (1)", variable=stress_var, value="1").pack(anchor='w')
tk.Radiobutton(frame, text="High (2)", variable=stress_var, value="2").pack(anchor='w')

tk.Label(root, text="Cups of water today:").pack()
entry_water = tk.Entry(root)
entry_water.pack(pady=5)

tk.Label(root, text="Mood (happy / neutral / stressed):").pack()
entry_mood = tk.Entry(root)
entry_mood.pack(pady=5)

btn = tk.Button(root, text="Get Advice", command=get_results)
btn.pack(pady=10)

result_label = tk.Label(root, text="", wraplength=450, justify="left")
result_label.pack(pady=10)

footer = tk.Label(root, text="Tip: Small daily habits lead to big improvements!", font=("Arial", 9, "italic"))
footer.pack(side="bottom", pady=10)

root.mainloop()
