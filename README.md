# to-do-list-
TaskFlow is a modern, responsive web application engineered to streamline daily productivity and task management. Built as a core project during my software development certification, this application solves a universal user problem: the need for a distraction-free, highly intuitive interface to track daily objectives. 
import os

FILE_NAME = "tasks.txt"

def load_tasks():
    """Loads tasks from a text file."""
    if not os.path.exists(FILE_NAME):
        return []
    with open(FILE_NAME, "r") as file:
        return [line.strip() for line in file.readlines()]

def save_tasks(tasks):
    """Saves tasks to a text file."""
    with open(FILE_NAME, "w") as file:
        for task in tasks:
            file.write(f"{task}\n")

def show_tasks(tasks):
    """Displays the current to-do list."""
    print("\n--- 📋 YOUR TO-DO LIST ---")
    if not tasks:
        print("Your list is empty!")
    for index, task in enumerate(tasks, start=1):
        print(f"{index}. {task}")
    print("-------------------------\n")

def main():
    tasks = load_tasks()
    
    while True:
        show_tasks(tasks)
        print("Options: [1] Add Task  [2] Delete Task  [3] Exit")
        choice = input("Choose an option (1-3): ").strip()
        
        if choice == "1":
            new_task = input("Enter the new task: ").strip()
            if new_task:
                tasks.append(new_task)
                save_tasks(tasks)
                print(f"✅ Added: '{new_task}'")
        elif choice == "2":
            if not tasks:
                print("❌ No tasks to delete.")
                continue
            try:
                task_num = int(input("Enter the task number to delete: "))
                if 1 <= task_num <= len(tasks):
                    removed = tasks.pop(task_num - 1)
                    save_tasks(tasks)
                    print(f"🗑️ Deleted: '{removed}'")
                else:
                    print("❌ Invalid task number.")
            except ValueError:
                print("❌ Please enter a valid number.")
        elif choice == "3":
            print("👋 Goodbye! Your tasks are saved.")
            break
        else:
            print("❌ Invalid choice. Please pick 1, 2, or 3.")

if __name__ == "__main__":
    main()