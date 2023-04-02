The Menu is a Menu with 6 commands running of python only:
!close - the "close" is a command that will exit the window in the near future might be renamed to "exit".
!generate.hash - the "hash generator" generates 50 character hash with numbers and letters.
!clear.chat - the "clear chat" basically clears the chat.
!list - the "list" feature when input "!list" it outputts all of the commands that are curentlly in the code.
!custom.password the "custom passowrd" was originally to set users "custom password" but the commands doesnt work since it cant save to the code it self.
!readme - the "reamme" feature put a "link" in a different window saying the link of this page.

Code-Copy the code below and put it to python

import tkinter as tk
import random
import string

def check_password():
    global attempts_left
    input_value = input_text.get()
    if input_value == password:
        password_window.destroy()
        open_main_window()
    else:
        attempts_left -= 1
        if attempts_left > 0:
            message_label.config(text=f"Password incorrect. You have {attempts_left} attempts left.")
        else:
            password_window.destroy()

def open_main_window():
    def check_input():
        input_value = input_text.get()
        if input_value == "!close":
            root.destroy()
        elif input_value == "!generate.hash":
            generate_hash()
        elif input_value == "!clear.chat":
            clear_chat()
        elif input_value == "!list":
            list_commands()
        elif input_value == "!custom.password":
            custom_password()
        elif input_value == "!readme":
            readme()
        else:
            message_label.config(text="Command not recognized. Type !list to see all available commands.")

    def generate_hash():
        hash_string = ''.join(random.choices(string.ascii_letters + string.digits, k=50))
        console_text.config(state=tk.NORMAL)
        console_text.insert(tk.END, hash_string + "\n")
        console_text.config(state=tk.DISABLED)

    def clear_chat():
        console_text.config(state=tk.NORMAL)
        console_text.delete("1.0", tk.END)
        console_text.config(state=tk.DISABLED)

    def list_commands():
        console_text.config(state=tk.NORMAL)
        console_text.insert(tk.END, "Here is the list of commands:\n!close\n!generate.hash\n!clear.chat\n!list\n!custom.password\n!readme\n")
        console_text.config(state=tk.DISABLED)

    def custom_password():
        global password
        input_value = input("Enter a new password: ")
        password = input_value
        console_text.config(state=tk.NORMAL)
        console_text.insert(tk.END, f"New password set: {password}\n")
        console_text.config(state=tk.DISABLED)

    def readme():
        readme_window = tk.Toplevel(root)
        readme_window.title("Readme")
        readme_window.geometry("600x100")
        readme_label = tk.Label(readme_window, text="balls")
        readme_label.pack()

    root = tk.Tk()
    root.title("Menu")
    root.geometry("1000x600")

    frame = tk.Frame(root, width=800, height=400, bd=1, relief=tk.SOLID)
    frame.place(relx=0.5, rely=0.5, anchor=tk.CENTER)

    input_text = tk.Entry(frame)
    input_text.pack(pady=10)

    submit_button = tk.Button(frame, text="Submit", command=check_input)
    submit_button.pack()

    console_frame = tk.Frame(frame)
    console_frame.pack(fill=tk.BOTH, expand=True)

    console_scrollbar = tk.Scrollbar(console_frame)
    console_scrollbar.pack(side=tk.RIGHT, fill=tk.Y)

    console_text = tk.Text(console_frame, height=10, yscrollcommand=console_scrollbar.set, state=tk.DISABLED)
    console_text.pack(fill=tk.BOTH, expand=True)

    console_scrollbar.config(command=console_text.yview)

    message_label = tk.Label(frame, text="Enjoy trying out my console system with many different features version 1.0", fg="green")
    message_label.pack(side=tk.TOP)

    root.mainloop()

attempts_left = 3
password = "password.135-ZS"

password_window = tk.Tk()
password_window.title("Password Prompt")
password_window.geometry("400x200")

frame = tk.Frame(password_window, width=300, height=100, bd=1, relief=tk.SOLID)
frame.place(relx=0.5, rely=0.5, anchor=tk.CENTER)

label = tk.Label(frame, text="Enter the password:")
label.pack()

input_text = tk.Entry(frame, show="*")
input_text.pack(pady=10)

submit_button = tk.Button(frame, text="Submit", command=check_password)
submit_button.pack()

message_label = tk.Label(frame, text="")
message_label.pack()

password_window.mainloop()
