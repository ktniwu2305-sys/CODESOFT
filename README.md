# CODESOFT

import os

TODO_FILE="todo.text"

def load_task():
 if not os.path.isfile(TODO_FILE):
        return []
    with open(TODO_FILE, "r") as f:
        tasks = [line.strip() for line in f.readlines() if line.strip()]
    return tasks

def save_tasks(tasks):
    with open(TODO_FILE, "w") as f:
        for task in tasks:
            f.write(task + "\n")

def add_task(task):
    tasks = load_tasks()
    tasks.append(task)
    save_tasks(tasks)
    print(f"Added: {task}")

def list_tasks():
    tasks = load_tasks()
    if not tasks:
        print("No tasks found.")
        return
    print("To Do List:")
    for i, task in enumerate(tasks, start=1):
        print(f"{i}. {task}")

def complete_task(task_number):
    tasks = load_tasks()
    if 1 <= task_number <= len(tasks):
        completed = tasks.pop(task_number - 1)
        save_tasks(tasks)
        print(f"Completed: {completed}")
    else:
        print("Invalid task number.")

def main():
    while True:
        print("\nMenu:")
        print("1. Add Task")
        print("2. View Tasks")
        print("3. Complete Task")
        print("4. Exit")
        choice = input("Choose an option: ")
        if choice == "1":
            task = input("Enter task: ")
            add_task(task)
        elif choice == "2":
            list_tasks()
        elif choice == "3":
            list_tasks()
            try:
                task_number = int(input("Enter task number to complete: "))
                complete_task(task_number)
            except ValueError:
                print("Please enter a valid number.")
        elif choice == "4":
            print("Goodbye!")
            break
        else:
            print("Invalid choice.")

if __name__ == "__main__":
    main()
