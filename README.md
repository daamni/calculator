# calculator
calculator by damni
'Import-Module PSReadLine'
import tkinter as tk

class Calculator:
    def __init__(self, master):
        self.master = master
        master.title("Calculator")

        # Create display widget
        self.display = tk.Entry(master, width=25, font=('Arial', 14))
        self.display.grid(row=0, column=0, columnspan=4, pady=5)

        # Create buttons
        buttons = [
            '7', '8', '9', '/',
            '4', '5', '6', '*',
            '1', '2', '3', '-',
            '0', '.', '=', '+'
        ]

        # Add buttons to the grid
        row = 1
        col = 0
        for button in buttons:
            command = lambda x=button: self.click(x)
            tk.Button(master, text=button, width=5, height=2, command=command).grid(row=row, column=col, pady=5)
            col += 1
            if col > 3:
                col = 0
                row += 1

    def click(self, key):
        if key == '=':
            # Calculate the result
            result = eval(self.display.get())
            self.display.delete(0, tk.END)
            self.display.insert(0, str(result))
        elif key == 'C':
            # Clear the display
            self.display.delete(0, tk.END)
        else:
            # Add the key to the display
            self.display.insert(tk.END, key)

root = tk.Tk()
calc = Calculator(root)
root.mainloop()
