# ============================================
#         TO-DO LIST APP  📝
#  A beginner Python project to manage tasks
# ============================================

# A list to store all our tasks
# Each task is a dictionary with 'title' and 'done' status
tasks = []


def show_menu():
    """Display the main menu options to the user."""
    print("\n" + "=" * 35)
    print("        📝 MY TO-DO LIST APP")
    print("=" * 35)
    print("  1. View all tasks")
    print("  2. Add a new task")
    print("  3. Mark a task as done ✅")
    print("  4. Delete a task")
    print("  5. Quit")
    print("=" * 35)


def view_tasks():
    """Show all tasks with their status."""
    print("\n📋 YOUR TASKS:")
    print("-" * 30)

    # Check if the list is empty
    if len(tasks) == 0:
        print("  No tasks yet! Add one to get started.")
    else:
        # Loop through tasks and display each one
        for index, task in enumerate(tasks):
            task_number = index + 1          # Start numbering from 1
            title = task["title"]
            is_done = task["done"]

            # Show a checkmark if done, or a bullet point if not
            if is_done:
                status = "✅"
            else:
                status = "⬜"

            print(f"  {task_number}. {status} {title}")

    print("-" * 30)


def add_task():
    """Ask the user for a task name and add it to the list."""
    print("\n➕ ADD A NEW TASK")
    title = input("  Enter task name: ").strip()  # .strip() removes extra spaces

    # Don't add empty tasks
    if title == "":
        print("  ⚠️  Task name cannot be empty!")
        return  # Exit the function early

    # Create a new task dictionary and add it to the list
    new_task = {
        "title": title,
        "done": False       # New tasks always start as not done
    }
    tasks.append(new_task)

    print(f"  ✅ Task '{title}' added successfully!")


def mark_done():
    """Mark a task as completed."""
    view_tasks()  # Show tasks first so user can pick one

    if len(tasks) == 0:
        return  # Nothing to mark if list is empty

    print("\n✅ MARK TASK AS DONE")
    choice = input("  Enter task number to mark as done: ")

    # Make sure the user typed a valid number
    if not choice.isdigit():
        print("  ⚠️  Please enter a valid number!")
        return

    task_index = int(choice) - 1  # Convert to 0-based index

    # Check if the number is within range
    if task_index < 0 or task_index >= len(tasks):
        print("  ⚠️  That task number doesn't exist!")
        return

    # Check if it's already done
    if tasks[task_index]["done"]:
        print(f"  ℹ️  '{tasks[task_index]['title']}' is already marked as done!")
    else:
        tasks[task_index]["done"] = True
        print(f"  ✅ '{tasks[task_index]['title']}' marked as done!")


def delete_task():
    """Remove a task from the list."""
    view_tasks()  # Show tasks first so user can pick one

    if len(tasks) == 0:
        return  # Nothing to delete if list is empty

    print("\n🗑️  DELETE A TASK")
    choice = input("  Enter task number to delete: ")

    # Make sure the user typed a valid number
    if not choice.isdigit():
        print("  ⚠️  Please enter a valid number!")
        return

    task_index = int(choice) - 1  # Convert to 0-based index

    # Check if the number is within range
    if task_index < 0 or task_index >= len(tasks):
        print("  ⚠️  That task number doesn't exist!")
        return

    # Remove the task and confirm to the user
    removed_task = tasks.pop(task_index)  # .pop() removes and returns the item
    print(f"  🗑️  '{removed_task['title']}' deleted successfully!")


# ============================================
#         MAIN PROGRAM STARTS HERE
# ============================================

print("\n👋 Welcome to your To-Do List App!")
print("   Let's help you stay organized.")

# Keep the app running until user chooses to quit
while True:
    show_menu()
    user_choice = input("\n  Enter your choice (1-5): ").strip()

    if user_choice == "1":
        view_tasks()

    elif user_choice == "2":
        add_task()

    elif user_choice == "3":
        mark_done()

    elif user_choice == "4":
        delete_task()

    elif user_choice == "5":
        print("\n👋 Goodbye! Stay productive! 🚀\n")
        break  # Exit the while loop, ending the program

    else:
        print("  ⚠️  Invalid choice! Please enter a number between 1 and 5.")
