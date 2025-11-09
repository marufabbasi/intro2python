# 🪶 Python Project: Personal Diary App

### 🎯 Goal
You will create a **Personal Diary App** where the user can:
- Add new diary entries  
- View all saved entries  
- Search entries for specific words  
- Exit the program  

This project combines everything you’ve learned so far:  
**variables, input, conditions, loops, functions, and file handling.**

---

## 🧩 Step 0 — Setup

Create a folder and a Python file for your project:

```bash
mkdir diary_app && cd diary_app
touch diary.py
```

---

## 🪜 Step 1 — Create the Menu Only

Start by making a menu that shows the options and repeats until the user chooses Exit.

```python
# diary.py — Step 1
def show_menu():
    print("\n===== Personal Diary =====")
    print("1) Add Entry")
    print("2) View Entries")
    print("3) Search Entries")
    print("4) Exit")

def main():
    while True:
        show_menu()
        choice = input("Choose an option (1-4): ").strip()
        if choice == "4":
            print("You chose: Exit — Goodbye!")
            break
        elif choice in {"1", "2", "3"}:
            print(f"You chose option {choice}.")
        else:
            print("Please choose a valid option (1-4).")

if __name__ == "__main__":
    main()
```

✅ **Try it:** Run `python diary.py` and see the menu appear.

---

## 🪜 Step 2 — Add Dummy Functions

Let’s turn each menu option into a function, but for now they just print messages.

```python
# diary.py — Step 2
def show_menu():
    print("\n===== Personal Diary =====")
    print("1) Add Entry")
    print("2) View Entries")
    print("3) Search Entries")
    print("4) Exit")

def add_entry():
    print("\n[Dummy] add_entry called — (feature coming soon)")

def view_entries():
    print("\n[Dummy] view_entries called — (feature coming soon)")

def search_entries():
    print("\n[Dummy] search_entries called — (feature coming soon)")

def main():
    while True:
        show_menu()
        choice = input("Choose an option (1-4): ").strip()
        if choice == "1":
            add_entry()
        elif choice == "2":
            view_entries()
        elif choice == "3":
            search_entries()
        elif choice == "4":
            print("Goodbye! 👋")
            break
        else:
            print("Please choose a valid option (1-4).")

if __name__ == "__main__":
    main()
```

✅ **Test:** Try each menu item — it should just print which function was called.

---

## 🪜 Step 3 — Implement “Add Entry”

Let’s make the **Add Entry** feature save the note into a file (`diary.txt`).

```python
# diary.py — Step 3
from pathlib import Path

DIARY_FILE = Path("diary.txt")

def show_menu():
    print("\n===== Personal Diary =====")
    print("1) Add Entry")
    print("2) View Entries")
    print("3) Search Entries")
    print("4) Exit")

def add_entry():
    print("\n--- Add New Entry ---")
    note = input("Type your diary note: ").strip()
    if not note:
        print("Nothing to save. Entry skipped.")
        return
    with DIARY_FILE.open("a", encoding="utf-8") as f:
        f.write(note + "\n")
    print("✅ Entry saved successfully.")

def view_entries():
    print("\n[Dummy] view_entries called — (feature coming soon)")

def search_entries():
    print("\n[Dummy] search_entries called — (feature coming soon)")

def main():
    while True:
        show_menu()
        choice = input("Choose an option (1-4): ").strip()
        if choice == "1":
            add_entry()
        elif choice == "2":
            view_entries()
        elif choice == "3":
            search_entries()
        elif choice == "4":
            print("Goodbye! 👋")
            break
        else:
            print("Please choose a valid option (1-4).")

if __name__ == "__main__":
    main()
```

✅ **Try it:** Add an entry and open `diary.txt` to see if it was saved.

---

## 🪜 Step 4 — Implement “View Entries”

Now, let’s display all the entries from the file.

```python
# diary.py — Step 4
from pathlib import Path

DIARY_FILE = Path("diary.txt")

def show_menu():
    print("\n===== Personal Diary =====")
    print("1) Add Entry")
    print("2) View Entries")
    print("3) Search Entries")
    print("4) Exit")

def add_entry():
    print("\n--- Add New Entry ---")
    note = input("Type your diary note: ").strip()
    if not note:
        print("Nothing to save. Entry skipped.")
        return
    with DIARY_FILE.open("a", encoding="utf-8") as f:
        f.write(note + "\n")
    print("✅ Entry saved successfully.")

def view_entries():
    print("\n--- View All Entries ---")
    if not DIARY_FILE.exists() or DIARY_FILE.stat().st_size == 0:
        print("📭 No entries yet.")
        return
    with DIARY_FILE.open("r", encoding="utf-8") as f:
        lines = [line.rstrip("\n") for line in f]
    if not lines:
        print("📭 No entries yet.")
        return
    for idx, line in enumerate(lines, start=1):
        print(f"{idx}. {line}")

def search_entries():
    print("\n[Dummy] search_entries called — (feature coming soon)")

def main():
    while True:
        show_menu()
        choice = input("Choose an option (1-4): ").strip()
        if choice == "1":
            add_entry()
        elif choice == "2":
            view_entries()
        elif choice == "3":
            search_entries()
        elif choice == "4":
            print("Goodbye! 👋")
            break
        else:
            print("Please choose a valid option (1-4).")

if __name__ == "__main__":
    main()
```

✅ **Try it:** Add a few entries, then select **View Entries** to see them listed.

---

## 🪜 Step 5 — Implement “Search Entries”

Allow users to search entries by keyword (case-insensitive).

```python
# diary.py — Step 5
from pathlib import Path

DIARY_FILE = Path("diary.txt")

def show_menu():
    print("\n===== Personal Diary =====")
    print("1) Add Entry")
    print("2) View Entries")
    print("3) Search Entries")
    print("4) Exit")

def add_entry():
    print("\n--- Add New Entry ---")
    note = input("Type your diary note: ").strip()
    if not note:
        print("Nothing to save. Entry skipped.")
        return
    with DIARY_FILE.open("a", encoding="utf-8") as f:
        f.write(note + "\n")
    print("✅ Entry saved successfully.")

def view_entries():
    print("\n--- View All Entries ---")
    if not DIARY_FILE.exists() or DIARY_FILE.stat().st_size == 0:
        print("📭 No entries yet.")
        return
    with DIARY_FILE.open("r", encoding="utf-8") as f:
        lines = [line.rstrip("\n") for line in f]
    for idx, line in enumerate(lines, start=1):
        print(f"{idx}. {line}")

def search_entries():
    print("\n--- Search Entries ---")
    keyword = input("Enter a keyword to search: ").strip().lower()
    if not keyword:
        print("Please enter a non-empty keyword.")
        return
    if not DIARY_FILE.exists():
        print("📭 No entries yet.")
        return
    with DIARY_FILE.open("r", encoding="utf-8") as f:
        lines = [line.rstrip("\n") for line in f]
    matches = [(i, e) for i, e in enumerate(lines, start=1) if keyword in e.lower()]
    if matches:
        print(f"🔎 Found {len(matches)} match(es):")
        for idx, entry in matches:
            print(f"{idx}. {entry}")
    else:
        print("No matching entries found.")

def main():
    while True:
        show_menu()
        choice = input("Choose an option (1-4): ").strip()
        if choice == "1":
            add_entry()
        elif choice == "2":
            view_entries()
        elif choice == "3":
            search_entries()
        elif choice == "4":
            print("Goodbye! 👋")
            break
        else:
            print("Please choose a valid option (1-4).")

if __name__ == "__main__":
    main()
```

✅ **Try it:** Add “Walked in rain” and “Learned Python loops,” then search for “rain.”

---

## 🌟 Step 6 — Optional Enhancements

### 🕒 Add Timestamps

```python
from datetime import datetime
ADD_TIMESTAMPS = True

def add_entry():
    print("\n--- Add New Entry ---")
    note = input("Type your diary note: ").strip()
    if not note:
        print("Nothing to save. Entry skipped.")
        return
    line = note
    if ADD_TIMESTAMPS:
        ts = datetime.now().strftime("%Y-%m-%d %H:%M")
        line = f"[{ts}] {note}"
    with DIARY_FILE.open("a", encoding="utf-8") as f:
        f.write(line + "\n")
    print("✅ Entry saved successfully.")
```

---

### 🗑️ Add Delete Option

```python
def show_menu():
    print("\n===== Personal Diary =====")
    print("1) Add Entry")
    print("2) View Entries")
    print("3) Search Entries")
    print("4) Delete Entry")
    print("5) Exit")

def delete_entry():
    print("\n--- Delete Entry ---")
    if not DIARY_FILE.exists() or DIARY_FILE.stat().st_size == 0:
        print("Nothing to delete—no entries yet.")
        return
    with DIARY_FILE.open("r", encoding="utf-8") as f:
        entries = [line.rstrip("\n") for line in f]
    for idx, e in enumerate(entries, start=1):
        print(f"{idx}. {e}")
    choice = input("Type the number to delete (or press Enter to cancel): ").strip()
    if not choice:
        print("Delete cancelled.")
        return
    if not choice.isdigit():
        print("Please enter a valid number.")
        return
    num = int(choice)
    if not (1 <= num <= len(entries)):
        print("Number out of range.")
        return
    confirm = input(f"Delete entry #{num}? (y/N): ").strip().lower()
    if confirm != "y":
        print("Delete cancelled.")
        return
    del entries[num - 1]
    with DIARY_FILE.open("w", encoding="utf-8") as f:
        for e in entries:
            f.write(e + "\n")
    print("🗑️ Entry deleted.")
```

---

### 🔐 Add Password Protection

```python
PASSWORD = "secret123"

def require_password():
    attempt = input("Enter diary password: ")
    if attempt != PASSWORD:
        print("Incorrect password. Exiting.")
        raise SystemExit

def main():
    require_password()
    while True:
        ...
```

---

## ✅ Final Result

Your diary app now supports:

| Feature | Description |
|----------|--------------|
| **Add Entry** | Add notes (with timestamps) |
| **View Entries** | Display all diary entries |
| **Search Entries** | Find notes by keyword |
| **Delete Entry** | Remove an unwanted note |
| **Exit** | Quit the program safely |

---

## 💡 Bonus Ideas

- Store entries as **JSON** for structured data.
- Add **tags** or **moods** to each entry.
- Use **datetime filtering** to show entries by date.
- Build a simple **GUI** with Tkinter later!

---

## 🧠 Summary

By the end of this project, you’ve practiced:
- Loops and conditional logic  
- File handling (read/write/append)  
- Functions and modular code  
- Basic text searching and validation  

Your Personal Diary App is now ready — and fully yours! ✨

---
