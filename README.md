import tkinter as tk
from tkinter import messagebox

# Contact list
contacts = []

def add_contact():
    name = name_entry.get()
    phone = phone_entry.get()
    email = email_entry.get()

    if name and phone and email:
        contacts.append({"name": name, "phone": phone, "email": email})
        update_contact_list()
        name_entry.delete(0, tk.END)
        phone_entry.delete(0, tk.END)
        email_entry.delete(0, tk.END)
    else:
        messagebox.showwarning("Warning", "Please fill in all fields")

def delete_contact():
    selected_contact = contact_list.curselection()
    if selected_contact:
        contacts.pop(selected_contact[0])
        update_contact_list()
    else:
        messagebox.showwarning("Warning", "Please select a contact to delete")

def update_contact_list():
    contact_list.delete(0, tk.END)
    for contact in contacts:
        contact_list.insert(tk.END, f"{contact['name']} - {contact['phone']} - {contact['email']}")

# Main window
contact_book = tk.Tk()
contact_book.title("Contact Book")
contact_book.geometry("500x400")
contact_book.resizable(0, 0)

# Labels and entries for contact details
tk.Label(contact_book, text="Name").grid(row=0, column=0, padx=10, pady=10)
name_entry = tk.Entry(contact_book, width=30)
name_entry.grid(row=0, column=1, padx=10, pady=10)

tk.Label(contact_book, text="Phone").grid(row=1, column=0, padx=10, pady=10)
phone_entry = tk.Entry(contact_book, width=30)
phone_entry.grid(row=1, column=1, padx=10, pady=10)

tk.Label(contact_book, text="Email").grid(row=2, column=0, padx=10, pady=10)
email_entry = tk.Entry(contact_book, width=30)
email_entry.grid(row=2, column=1, padx=10, pady=10)

# Buttons to add and delete contacts
add_button = tk.Button(contact_book, text="Add Contact", command=add_contact, width=15)
add_button.grid(row=3, column=0, padx=10, pady=10)

delete_button = tk.Button(contact_book, text="Delete Contact", command=delete_contact, width=15)
delete_button.grid(row=3, column=1, padx=10, pady=10)

# Listbox to display contacts
contact_list = tk.Listbox(contact_book, width=50, height=15)
contact_list.grid(row=4, column=0, columnspan=2, padx=10, pady=10)

# Start the application
contact_book.mainloop()
