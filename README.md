# Managing Stress for Students

## Group Members
- Dave
- Qodi
- Aaron

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
- Backend handles tip selection based on user input (if applicable)
- Code tested locally for functionality and errors

## Code Examples

```python
# Mini Stress-Helper Program

# Function to give a tip based on hours of sleep
def sleep_tip(hours_slept):
    if hours_slept < 0:
        return "That's not a valid number of hours!"
    elif hours_slept < 5:
        return "You slept very little! Take a short nap and rest."
    elif 5 <= hours_slept < 8:
        return "You got some sleep, but try to sleep more tonight for full recovery."
    else:  # 8 or more hours
        return "Great! You got enough sleep. Keep it up for a healthy routine."

# Function to give a stress tip based on stress level (0=low, 1=medium, 2=high)
def stress_tip(level):
    tips = [
        "Take a short break and breathe deeply.",
        "Make sure to sleep at least 8 hours.",
        "Do 15–30 minutes of light exercise."
    ]

    if level < 0 or level >= len(tips):
        return "Invalid stress level selected."
    return tips[level]

# --- Main Program ---

print("=== Welcome to the Mini Stress-Helper ===")

# Get user input for sleep (safe input)
while True:
    try:
        hours = float(input("How many hours did you sleep yesterday? "))
        break
    except ValueError:
        print("Please enter a valid number (e.g., 6 or 7.5).")

print(sleep_tip(hours))

# Get user input for stress level (safe input)
print("\nStress Levels: 0=Low, 1=Medium, 2=High")

while True:
    try:
        stress_level = int(input("Enter your stress level: "))
        if 0 <= stress_level <= 2:
            break
        else:
            print("Please enter 0, 1, or 2 only.")
    except ValueError:
        print("Please enter a valid integer (0, 1, or 2).")

print(stress_tip(stress_level))

print("\nStay healthy and take care of yourself! 😊")
