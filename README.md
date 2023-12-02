Salery Management System
import tkinter as tk
from tkinter import messagebox

class SalaryCalculator:
    def __init__(self, root):
        self.root = root
        self.root.title("Salary Calculator")

        self.create_widgets()

    def create_widgets(self):
        # Employee Name
        self.name_label = tk.Label(self.root, text="Employee Name:")
        self.name_label.grid(row=0, column=0, padx=10, pady=10)
        self.name_entry = tk.Entry(self.root)
        self.name_entry.grid(row=0, column=1, padx=10, pady=10)

        # Position
        self.position_label = tk.Label(self.root, text="Position:")
        self.position_label.grid(row=1, column=0, padx=10, pady=10)
        self.position_var = tk.StringVar()
        self.position_var.set("Software Developer")  # Default position
        self.position_dropdown = tk.OptionMenu(self.root, self.position_var, "Software Developer", "Manager", "Intern")
        self.position_dropdown.grid(row=1, column=1, padx=10, pady=10)

        # Hours Worked
        self.hours_worked_label = tk.Label(self.root, text="Hours Worked:")
        self.hours_worked_label.grid(row=2, column=0, padx=10, pady=10)
        self.hours_worked_entry = tk.Entry(self.root)
        self.hours_worked_entry.grid(row=2, column=1, padx=10, pady=10)

        # Bills
        self.bills_label = tk.Label(self.root, text="Bills:")
        self.bills_label.grid(row=3, column=0, padx=10, pady=10)

        # Bill Type
        self.bill_type_label = tk.Label(self.root, text="Bill Type:")
        self.bill_type_label.grid(row=4, column=0, padx=10, pady=10)
        self.bill_type_entry = tk.Entry(self.root)
        self.bill_type_entry.grid(row=4, column=1, padx=10, pady=10)

        # Bill Amount
        self.bill_amount_label = tk.Label(self.root, text="Bill Amount:")
        self.bill_amount_label.grid(row=5, column=0, padx=10, pady=10)
        self.bill_amount_entry = tk.Entry(self.root)
        self.bill_amount_entry.grid(row=5, column=1, padx=10, pady=10)

        # Calculate Button
        self.calculate_button = tk.Button(self.root, text="Calculate Salary", command=self.calculate_salary)
        self.calculate_button.grid(row=6, column=0, columnspan=2, pady=10)

    def calculate_salary(self):
        try:
            position = self.position_var.get()
            hours_worked = float(self.hours_worked_entry.get())

            # Define salary configuration templates based on position
            salary_templates = {
                "Software Developer": {"hourly_rate": 30, "bonus": 500},
                "Manager": {"hourly_rate": 40, "bonus": 1000},
                "Intern": {"hourly_rate": 15, "bonus": 100}
            }

            # Get the salary template for the selected position
            template = salary_templates.get(position)

            if template:
                hourly_rate = template["hourly_rate"]
                bonus = template["bonus"]
                salary = hours_worked * hourly_rate + bonus

                # Get bills information
                bill_type = self.bill_type_entry.get()
                bill_amount = float(self.bill_amount_entry.get()) if self.bill_amount_entry.get() else 0

                # Calculate net salary by deducting bills
                net_salary = salary - bill_amount

                # Display salary details using messagebox
                messagebox.showinfo("Salary Details", f"Employee: {self.name_entry.get()}\n"
                                                      f"Position: {position}\n"
                                                      f"Hours Worked: {hours_worked}\n"
                                                      f"Hourly Rate: {hourly_rate}\n"
                                                      f"Bonus: {bonus}\n"
                                                      f"Salary: {salary}\n"
                                                      f"Bills - {bill_type}: {bill_amount}\n"
                                                      f"Net Salary: {net_salary}")
            else:
                messagebox.showerror("Error", "Invalid position selected.")
        except ValueError:
            messagebox.showerror("Error", "Please enter valid numeric values for Hours Worked and Bill Amount.")

# Create and run the Tkinter application
if __name__ == "__main__":
    root = tk.Tk()
    app = SalaryCalculator(root)
    root.mainloop()
