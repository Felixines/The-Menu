import tkinter as tk
import random
import string

def check_password():
    global attempts_left
    input_value = input_text.get()
    if input_value == "password.135-ZS":
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
        elif input_value == "!h.tab":
            open_hacker_tab()
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
        console_text.insert(tk.END, "Here is the list of commands:\n!close\n!generate.hash\n!clear.chat\n!list\n!h.tab\n")
        console_text.config(state=tk.DISABLED)

    def open_hacker_tab():
        hacker_tab_window = tk.Toplevel()
        hacker_tab_window.title("Hacker Tab")
        hacker_tab_window.geometry("800x600")
        hacker_tab_window.configure(bg="black")

        console_text = tk.Text(hacker_tab_window, height=30, width=100, fg="green", bg="black", font=("Courier", 12))
        console_text.pack()

        def rain():
            console_text.insert(tk.END, random.choice(["0", "1"]))
            console_text.see(tk.END)
            console_text.after(10, rain)

        rain()

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

    message_label = tk.Label(root, text="Enjoy trying out my console system with many different features version 1.0", fg="green")
    message_label.pack(side=tk.LEFT)

    root.mainloop()

attempts_left = 3

password_window = tk.T
