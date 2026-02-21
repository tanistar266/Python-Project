# Python-Project
import time
import random

levels = {
    1: ["Typing is a useful skill that helps students and professionals complete their work faster.",
        "In the digital world, typing efficiently is more important than ever before. Speed and accuracy both matter."],
    2: ["In the digital world, typing efficiently is more important than ever before. Speed and accuracy both matter.",
        "Through this project, we understood how unfiltered corporation water affects health and quality of life."],
    3: ["In 2026, digital literacy requires speed, precision, and the ability to type complex symbols like @, #, %, &, *, and parentheses under pressure.",
        "Water is an essential part of life, but the water supplied by municipal corporations is often unfiltered and unsafe for direct consumption."]
}
level_accuracies = {}
level_speeds = {}

level = 1
print("..................... TYPING ACCURACY AND SPEED....................")
while level <= 3:

    print("\nLevel:", level)

    refer_text = random.choice(levels[level])
    print(refer_text)

    time_limit = None
    if level == 2:
        time_limit = 90
    elif level == 3:
        time_limit = 120

    start_time = time.time()
    typed_text = input("Start Typing...\n")
    end_time = time.time()

    time_taken = end_time - start_time

    minutes = int(time_taken // 60)
    seconds = int(time_taken % 60)
    print(f"Time: {minutes} min {seconds} sec")

    if time_limit is not None and time_taken > time_limit:
        print("Time limit exceeded! Retry this level.")
        continue

    correct_chars = 0
    for i in range(min(len(typed_text), len(refer_text))):
        if typed_text[i] == refer_text[i]:
            correct_chars += 1

    accuracy = (correct_chars / len(refer_text)) * 100

    time_minutes = time_taken / 60
    if time_minutes > 0:
        speed_cpm = len(refer_text) / time_minutes
    else:
        speed_cpm = 0

    print("Accuracy:", round(accuracy, 2))
    print("Speed (CPM):", round(speed_cpm, 2))
    level_accuracies[level] = accuracy
    level_speeds[level] = speed_cpm

    if accuracy >= 75:
        if level == 1:
            choice = input("Do you want to proceed to level 2? (y/n): ").lower()
            if choice == "y":
                level += 1
            else:
                print("Thank you for visiting.....")
                break
        else :
            level += 1
    else:
        print("Retry this level")

print("Congratulations! You completed all levels.")
print("Level-wise Accuracy: ")
for lvl in level_accuracies:
    print("level",lvl,": (Accuracy,Speed)",
round(level_accuracies[lvl],2),
round(level_speeds[lvl],2))


avg_accuracy = sum(level_accuracies.values()) / len(level_accuracies)
avg_speeds = sum(level_speeds.values()) / len(level_speeds)
print("Average Accuracy :" , sum(level_accuracies.values())/3)
print("Average Speeds :" , sum(level_speeds.values())/3)
