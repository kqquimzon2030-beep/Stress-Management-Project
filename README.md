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
