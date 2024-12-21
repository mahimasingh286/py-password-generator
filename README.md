# py-password-generator

import tkinter as tk
from tkinter import messagebox
import random

letters = 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'
numbers = '0123456789'
symbols = '!@#$%^&*()_+'
def password_generator():
    try:
        nr_letters = int(letter_entry.get())
        nr_numbers = int(number_entry.get())
        nr_symbols = int(symbol_entry.get())
    except ValueError:
      
        messagebox.showerror("Invalid Input", "Please enter numbers only!")
        return
  
    if nr_letters <= 0 or nr_numbers <= 0 or nr_symbols <= 0:
        messagebox.showwarning("Invalid Input", "All values must be greater than 0.")
        return

    password_list = []
    for _ in range(nr_letters):
        password_list.append(random.choice(letters))
    for _ in range(nr_numbers):
        password_list.append(random.choice(numbers))
    for _ in range(nr_symbols):
        password_list.append(random.choice(symbols))

    random.shuffle(password_list)
    password = ''.join(password_list)  
   
    if len(password) < 16:
        messagebox.showwarning("Weak Password", f"Your created password is weak: {password}")
    else:
        messagebox.showinfo("Strong Password", f"Your created password is strong: {password}")

window = tk.Tk()
window.title("Password Generator")
window.geometry("400x300")


tk.Label(window, text="Number of Letters:").pack()
letter_entry = tk.Entry(window)
letter_entry.pack()

tk.Label(window, text="Number of Numbers:").pack()
number_entry = tk.Entry(window)
number_entry.pack()

tk.Label(window, text="Number of Symbols:").pack()
symbol_entry = tk.Entry(window)
symbol_entry.pack()


generate_button = tk.Button(window, text="Generate Password", command=password_generator)
generate_button.pack(pady=20)

window.mainloop()
