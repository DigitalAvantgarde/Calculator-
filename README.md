# Calculator-

import tkinter as tk
from tkinter import messagebox

echo "# Calculator-" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/DigitalAvantgarde/Calculator-.git
git push -u origin main

def add_digit(digit):
    value = calc.get()
    if value[0] == "0" and len(value) == 1:
        value = value[1:]
    calc.delete(0, tk.END)
    calc.insert(0, value + digit)


def add_operation(operation):
    value = calc.get()
    if value[-1] in "-+*/":
        value = value[:-1]
    # Operation
    elif "+" in value or "-" in value or "*" in value or "/" in value:
        calculate()
        value = calc.get()
    calc.delete(0, tk.END)
    calc.insert(0, value + operation)


def calculate():
    value = calc.get()
    if value[-1] in "+-/*":
        value = value + value[:-1]
    calc.delete(0, tk.END)
    try:
        calc.insert(0, eval(value))
    except (NameError, SyntaxError):
        messagebox.showinfo("Attention", "You can only enter numbers!!!")
        calc.insert(0, 0)


def clear():
    calc.delete(0, tk.END)
    calc.insert(0, 0)


def make_digit_button(digit):
    return tk.Button(text=digit, bd=3, font=("Courier New", 33),
                     command=lambda: add_digit(digit))


def make_opiration_button(opiration):
    return tk.Button(text=opiration, bd=2, font=("Courier New", 33),
                     command=lambda: add_operation(opiration))


def make_calc_button(opiration):
    return tk.Button(text=opiration, bd=2, font=("Courier New", 33),
                     command=calculate)


def make_clear_button(opiration):
    return tk.Button(text=opiration, bd=2, font=("Courier New", 33),
                     command=clear)


def press_key(event):
    print(event.char)
    if event.char.isdigit():
        add_digit(event.char)
    elif event.char in "+,-,*,/":
        add_operation(event.char)
    elif event.char == "\r":
        calculate()


win = tk.Tk()
win.geometry("400x430+200+200")
win["bg"] = "#f1f5f6"
win.title("Calculator ")

win.bind("<Key>", press_key)

calc = tk.Entry(win, justify=tk.LEFT, font=("Helvetica", 15), width=15)
calc.insert(0, "0")
calc.grid(row=0, column=0, columnspan=5, stic="we", padx=15)

make_digit_button("1").grid(row=1, column=0, stick="wens", padx=5, pady=5)
make_digit_button("2").grid(row=1, column=1, stick="wens", padx=5, pady=5)
make_digit_button("3").grid(row=1, column=2, stick="wens", padx=5, pady=5)
make_digit_button("4").grid(row=2, column=0, stick="wens", padx=5, pady=5)
make_digit_button("5").grid(row=2, column=1, stick="wens", padx=5, pady=5)
make_digit_button("6").grid(row=2, column=2, stick="wens", padx=5, pady=5)
make_digit_button("7").grid(row=3, column=0, stick="wens", padx=5, pady=5)
make_digit_button("8").grid(row=3, column=1, stick="wens", padx=5, pady=5)
make_digit_button("9").grid(row=3, column=2, stick="wens", padx=5, pady=5)
make_digit_button("0").grid(row=4, column=1, stick="wens", padx=5, pady=5)

make_opiration_button("+").grid(row=4, column=3, stick="wens", padx=5, pady=5)
make_opiration_button("-").grid(row=3, column=3, stick="wens", padx=5, pady=5)
make_opiration_button("*").grid(row=2, column=3, stick="wens", padx=5, pady=5)
make_opiration_button("/").grid(row=1, column=3, stick="wens", padx=5, pady=5)

make_calc_button("=").grid(row=4, column=2, stick="wens", padx=5, pady=5)
make_clear_button("C").grid(row=4, column=0, stick="wens", padx=5, pady=5)

win.grid_columnconfigure(0, minsize=100)
win.grid_columnconfigure(1, minsize=100)
win.grid_columnconfigure(2, minsize=100)
win.grid_columnconfigure(3, minsize=100)

win.grid_rowconfigure(1, minsize=100)
win.grid_rowconfigure(2, minsize=100)
win.grid_rowconfigure(3, minsize=100)
win.grid_rowconfigure(4, minsize=100)
