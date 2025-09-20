# text_editor
A simple and lightweight text editor built with Python and Tkinter. This editor allows users to create, open, edit, and save text files with essential editing features. Perfect for beginners learning Python GUI programming or anyone who needs a minimal text editing tool.


# Code in python langauge....
import tkinter as tk
from tkinter import filedialog, messagebox

# Create main window
root = tk.Tk()
root.title("My Text Editor")
root.geometry("600x400")

# Text area
text_area = tk.Text(root, undo=True)
text_area.pack(fill=tk.BOTH, expand=1)

# Functions
def new_file():
    text_area.delete(1.0, tk.END)

def open_file():
    file_path = filedialog.askopenfilename(defaultextension=".txt",
                                           filetypes=[("Text Files", "*.txt"), ("All Files", "*.*")])
    if file_path:
        text_area.delete(1.0, tk.END)
        with open(file_path, "r") as file:
            text_area.insert(tk.END, file.read())
        root.title(f"My Text Editor - {file_path}")

def save_file():
    file_path = filedialog.asksaveasfilename(defaultextension=".txt",
                                             filetypes=[("Text Files", "*.txt"), ("All Files", "*.*")])
    if file_path:
        with open(file_path, "w") as file:
            file.write(text_area.get(1.0, tk.END))
        root.title(f"My Text Editor - {file_path}")

def exit_editor():
    if messagebox.askokcancel("Quit", "Do you want to exit?"):
        root.destroy()

# Menu
menu_bar = tk.Menu(root)

# File menu
file_menu = tk.Menu(menu_bar, tearoff=0)
file_menu.add_command(label="New", command=new_file)
file_menu.add_command(label="Open", command=open_file)
file_menu.add_command(label="Save", command=save_file)
file_menu.add_separator()
file_menu.add_command(label="Exit", command=exit_editor)
menu_bar.add_cascade(label="File", menu=file_menu)

# Edit menu
edit_menu = tk.Menu(menu_bar, tearoff=0)
edit_menu.add_command(label="Cut", command=lambda: text_area.event_generate("<<Cut>>"))
edit_menu.add_command(label="Copy", command=lambda: text_area.event_generate("<<Copy>>"))
edit_menu.add_command(label="Paste", command=lambda: text_area.event_generate("<<Paste>>"))
edit_menu.add_command(label="Undo", command=lambda: text_area.event_generate("<<Undo>>"))
edit_menu.add_command(label="Redo", command=lambda: text_area.event_generate("<<Redo>>"))
menu_bar.add_cascade(label="Edit", menu=edit_menu)

root.config(menu=menu_bar)
root.mainloop()
