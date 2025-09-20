# text_editor
A simple and lightweight text editor built with Python and Tkinter. This editor allows users to create, open, edit, and save text files with essential editing features. Perfect for beginners learning Python GUI programming or anyone who needs a minimal text editing tool.

<h1 align="center">Hi 👋, I'm Surendra Gupta</h1>
<h3 align="center">A passionate software developer from India</h3>

<p align="left"> <img src="https://komarev.com/ghpvc/?username=surendragupta&label=Profile%20views&color=0e75b6&style=flat" alt="surendragupta" /> </p>

<p align="left"> <a href="https://github.com/ryo-ma/github-profile-trophy"><img src="https://github-profile-trophy.vercel.app/?username=surendragupta" alt="surendragupta" /></a> </p>

- 🔭 I’m currently working on [Portfolio website](https://surendragupta7458011439-ui.github.io/samples_portfolio/)

- 🌱 I’m currently learning **programming langauge**

- 👯 I’m looking to collaborate on [Text- editor](https://surendragupta7458011439-ui.github.io/text_editor/)

- 💬 Ask me about **C,C++,Python,HTML,CSS**

- 📫 How to reach me **surendragupta_bca24_27@its.edu.in**

- ⚡ Fun fact **Problem solving**

<h3 align="left">Connect with me:</h3>
<p align="left">
<a href="https://instagram.com/guptasurendra_" target="blank"><img align="center" src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/instagram.svg" alt="guptasurendra_" height="30" width="40" /></a>
</p>

<h3 align="left">Languages and Tools:</h3>
<p align="left"> <a href="https://www.cprogramming.com/" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/c/c-original.svg" alt="c" width="40" height="40"/> </a> <a href="https://www.w3schools.com/cpp/" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/cplusplus/cplusplus-original.svg" alt="cplusplus" width="40" height="40"/> </a> <a href="https://www.w3schools.com/css/" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/css3/css3-original-wordmark.svg" alt="css3" width="40" height="40"/> </a> <a href="https://www.w3.org/html/" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/html5/html5-original-wordmark.svg" alt="html5" width="40" height="40"/> </a> <a href="https://www.python.org" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/python/python-original.svg" alt="python" width="40" height="40"/> </a> <a href="https://www.tensorflow.org" target="_blank" rel="noreferrer"> <img src="https://www.vectorlogo.zone/logos/tensorflow/tensorflow-icon.svg" alt="tensorflow" width="40" height="40"/> </a> </p>

<p><img align="center" src="https://github-readme-stats.vercel.app/api/top-langs?username=surendragupta&show_icons=true&locale=en&layout=compact" alt="surendragupta" /></p>



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
