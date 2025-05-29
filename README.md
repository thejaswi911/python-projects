import tkinter as tk
from tkinter import messagebox
import re  # For email validation


def is_valid_email(email):
    pattern = r'^[\w\.-]+@gmail\.com$'
    return re.match(pattern, email)


def submit_form():
    first_name = firstname_entry.get()
    last_name = lastname_entry.get()
    gender = gender_var.get()
    age = age_entry.get()
    gmail = gmail_entry.get()
    password = password_entry.get()

    if not all([first_name, last_name, gender, age, gmail, password]):
        messagebox.showwarning("Input Error", "Please fill in all fields.")
        return

    if gender == "select options":
        messagebox.showwarning("Input Error", "Please select a valid gender.")
        return

    if not age.isdigit():
        messagebox.showwarning("Input Error", "Age must be a numeric value.")
        return

    if not is_valid_email(gmail):
        messagebox.showwarning("Input Error", "Please enter a valid Gmail address.")
        return

    
    with open("registrations.txt", "a") as file:
        file.write(f"First Name: {first_name}, Last Name: {last_name}, Gender: {gender}, Age: {age}, Gmail: {gmail}, Password: {password}\n")

    messagebox.showinfo("Success", "Registered successfully!")

    
    firstname_entry.delete(0, tk.END)
    lastname_entry.delete(0, tk.END)
    age_entry.delete(0, tk.END)
    gmail_entry.delete(0, tk.END)
    password_entry.delete(0, tk.END)
    gender_var.set(gender_options[0])


root = tk.Tk()
root.title("Registration Form")
root.geometry("500x600")

outer_frame = tk.Frame(root, bg="black", padx=2, pady=2)
outer_frame.pack(padx=10, pady=10)

inner_frame = tk.Frame(outer_frame, bg="white", padx=2, pady=2)
inner_frame.pack()

form_frame = tk.Frame(inner_frame, bg="white", padx=10, pady=10)
form_frame.pack()

tk.Label(form_frame, text="First name:", font=("Arial", 14)).pack(anchor='w', padx=10, pady=5)
firstname_entry = tk.Entry(form_frame, width=30)
firstname_entry.pack(anchor='w', padx=10, pady=5)

tk.Label(form_frame, text="Last name:", font=("Arial", 14)).pack(anchor='w', padx=10, pady=5)
lastname_entry = tk.Entry(form_frame, width=30)
lastname_entry.pack(anchor='w', padx=10, pady=5)

tk.Label(form_frame, text="Gender:", font=("Arial", 14)).pack(anchor='w', padx=10, pady=5)
gender_options = ["select options", "male", "female", "others"]
gender_var = tk.StringVar()
gender_var.set(gender_options[0])
gender_menu = tk.OptionMenu(form_frame, gender_var, *gender_options)
gender_menu.config(width=30, font=("Arial", 12))
gender_menu.pack(anchor='w', padx=10, pady=5)


tk.Label(form_frame, text="Age:", font=("Arial", 14)).pack(anchor='w', padx=10, pady=5)
age_entry = tk.Entry(form_frame, width=10)
age_entry.pack(anchor='w', padx=10, pady=5)

tk.Label(form_frame, text="Gmail:", font=("Arial", 14)).pack(anchor='w', padx=10, pady=5)
gmail_entry = tk.Entry(form_frame, width=40)
gmail_entry.pack(anchor='w', padx=10, pady=5)

tk.Label(form_frame, text="Password:", font=("Arial", 14)).pack(anchor='w', padx=10, pady=5)
password_entry = tk.Entry(form_frame, width=30, show="*")
password_entry.pack(anchor='w', padx=10, pady=5)

submit_button = tk.Button(
    form_frame,
    text="Register",
    font=("Arial", 14),
    command=submit_form,
    bg="green",
    fg="white",
    activebackground="darkgreen",
    activeforeground="white"
)
submit_button.pack(pady=20)

root.mainloop()
