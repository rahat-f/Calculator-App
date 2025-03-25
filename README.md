import tkinter as tk

# Create the main window
root = tk.Tk()
root.title("Calculator")
root.geometry("350x500")
root.configure(bg="#2C2F33")

# Function to update the expression
def press(key):
    entry.insert(tk.END, key)

# Function to evaluate the expression
def calculate():
    try:
        result = eval(entry.get())
        entry.delete(0, tk.END)
        entry.insert(tk.END, result)
    except:
        entry.delete(0, tk.END)
        entry.insert(tk.END, "Error")

# Function to clear the entry field
def clear():
    entry.delete(0, tk.END)

# Function to delete the last character
def backspace():
    entry.delete(len(entry.get())-1, tk.END)

# Entry field styling
entry = tk.Entry(root, font=("Arial", 24), width=15, borderwidth=2, relief="solid", justify="right", bg="#23272A", fg="white")
entry.grid(row=0, column=0, columnspan=4, padx=10, pady=10)

# Button styling
btn_style = {
    "font": ("Arial", 14, "bold"),
    "width": 5,
    "height": 2,
    "relief": "raised",
    "bd": 3,
    "bg": "#7289DA",  # Default button color
    "fg": "white",
    "activebackground": "#5B6EAE",
    "activeforeground": "white"
}

# Button layout
buttons = [
    ('7', 1, 0), ('8', 1, 1), ('9', 1, 2), ('/', 1, 3),
    ('4', 2, 0), ('5', 2, 1), ('6', 2, 2), ('*', 2, 3),
    ('1', 3, 0), ('2', 3, 1), ('3', 3, 2), ('-', 3, 3),
    ('0', 4, 0), ('.', 4, 1), ('+', 4, 2), ('=', 4, 3),
    ('C', 5, 0), ('⌫', 5, 1)  
]

# Adding buttons to the window
for (text, row, col) in buttons:
    btn_custom_style = btn_style.copy()  # Copy the style dictionary

    if text == '=':
        btn_custom_style["bg"] = "#43B581"  # Green for "=" button
        button = tk.Button(root, text=text, **btn_custom_style, command=calculate)
    elif text == 'C':
        btn_custom_style["bg"] = "#F04747"  # Red for "Clear"
        button = tk.Button(root, text=text, **btn_custom_style, command=clear)
    elif text == '⌫':
        btn_custom_style["bg"] = "#FAA61A"  # Orange for "Backspace"
        button = tk.Button(root, text=text, **btn_custom_style, command=backspace)
    else:
        button = tk.Button(root, text=text, **btn_style, command=lambda key=text: press(key))
    
    button.grid(row=row, column=col, padx=5, pady=5)

# Run the Tkinter loop
root.mainloop()
