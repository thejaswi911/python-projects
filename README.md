import tkinter as tk
from tkinter import messagebox


def submit_form():
    user_info={
        "First name": firstname_entry.get(),
        "Last name": lastname_entry.get(),
        "Age": age_entry.get(),
        "Gmail": gmail_entry.get(),
    }

    if all (user_info.values()):
        messagebox.showinfo("success","registrated successfully")
    else:
        messagebox.showwarning("input error","please fill in all fields")
    def show_selection():
         print(f"selected Gender:{gender_var.get()}")
root=tk.Tk()
root.title("registration form")
root.geometry("500x500")

# Outer frame simulating the outer border
outer_frame = tk.Frame(root, bg="black", padx=2, pady=2)
outer_frame.pack(padx=10, pady=10)

# Inner frame simulating the inner border
inner_frame = tk.Frame(outer_frame, bg="white", padx=2, pady=2)
inner_frame.pack()

# Main content frame (your form elements go here)
form_frame = tk.Frame(inner_frame, bg="white", padx=10, pady=10)
form_frame.pack()

tk.Label(form_frame, text="First name:",font=("Arial",14)).pack(anchor='w', padx=10, pady=5)
firstname_entry = tk.Entry(form_frame,width=30)
firstname_entry.pack(anchor='w', padx=10, pady=5)

tk.Label(form_frame, text="Last name:",font=("Arial",14)).pack(anchor='w',padx=10,pady=5)
lastname_entry=tk.Entry(form_frame,width=30)
lastname_entry.pack(anchor='w',padx=10,pady=5)

tk.Label(form_frame,text="Gender:",font=("Arial",14)).pack(anchor='w',padx=10,pady=5)
gender_options=["select options","male","female","others"]
gender_var=tk.StringVar(form_frame)
gender_var.set(gender_options[0])
gender_menu=tk.OptionMenu(form_frame,gender_var,*gender_options)
gender_menu.config(width=30,font=("Arial",12))
gender_menu.pack( anchor='w',padx=10,pady=5)

tk.Label(form_frame,text="Age:",font=("Arial",14)).pack(anchor='w',padx='5',pady='5')
age_entry=tk.Entry(form_frame,width=10)
age_entry.pack(anchor='w',padx=10,pady=5)

tk.Label(form_frame, text="Gmail:",font=("Arial",14)).pack(anchor='w',padx=20,pady=5)
gmail_entry=tk.Entry(form_frame,width=40)
gmail_entry.pack(anchor='w',padx='10',pady='5')

submit_button= tk.Button(
    form_frame,
    text="register",
    font=("Arial",14),
  command=submit_form,
  bg="green",
  fg="white",
  activebackground="darkgreen",
  activeforeground="white"
  )
submit_button.pack(pady=20)
root.mainloop()
