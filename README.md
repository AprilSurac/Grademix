# Define the path to the SQLite database file
db_file_path = os.path.join(os.path.expanduser("~"), "Downloads", "grademix.db")

# Connect to the SQLite database
conn = sqlite3.connect(db_file_path)
cursor = conn.cursor()

# Create a table for user data (you can expand this based on your needs)
cursor.execute("""
CREATE TABLE IF NOT EXISTS users (
    id INTEGER PRIMARY KEY,
    username TEXT UNIQUE NOT NULL,
    password TEXT NOT NULL
)
""")
conn.commit()

def insert_user(username, password):
    cursor.execute("INSERT INTO users (username, password) VALUES (?, ?)", (username, password))
    conn.commit()

def check_username_taken(username):
    cursor.execute("SELECT * FROM users WHERE username=?", (username,))
    return cursor.fetchone() is not None

def close_db_connection():
    conn.close()

def custom_login():
    username = username_entry.get()
    password = password_entry.get()

    # Implement your custom login logic here
    # For simplicity, let's just show a messagebox with the entered credentials
    messagebox.showinfo("Custom Login", f"Username: {username}\nPassword: {password}")

def custom_signup():
    username = username_entry.get()
    password = password_entry.get()

    # Check if the username is already taken
    if check_username_taken(username):
        messagebox.showerror("Error", "Username already taken. Choose a different one.")
        return

    # Check if the password meets the updated requirements
    if not (10 <= len(password) <= 12 and re.match(r'^(?=.*[a-zA-Z])(?=.*\d)(?=.*[@]).*$', password)):
        messagebox.showerror("Error", "Password must be 10-12 characters long and include letters, numbers, and the '@' character.")
        return
    insert_user(username, password)

    # If successful, show a message and proceed to the profile page (placeholder)
    messagebox.showinfo("Success", "Sign-up successful!\nRedirecting to profile...")
    create_profile_window()
def create_gpa_calculator_frame():
    # Create a frame for the GPA Calculator within the existing root window
    gpa_calculator_frame = tk.Frame(root, bg="#066749")
    gpa_calculator_frame.grid(row=1, column=0, padx=10, pady=5)

    # Set the font and size for the titles
    title_font = ("Comic Sans MS", 30, "bold")
    label_font = ("Comic Sans MS", 16)
    entry_font = ("Comic Sans MS", 14)
    button_font = ("Comic Sans MS", 14)

    # Set the font and size for the titles
    title_label = tk.Label(gpa_calculator_frame, text="GPA Calculator", font=title_font, fg="white", bg="#066749")
    title_label.grid(row=0, column=0, columnspan=2, pady=10)

    # Create frames for unweighted and weighted GPA calculators
    unweighted_frame = tk.Frame(gpa_calculator_frame, bg="#066749")
    unweighted_frame.grid(row=1, column=0, padx=10, pady=5)

    weighted_frame = tk.Frame(gpa_calculator_frame, bg="#066749")
    weighted_frame.grid(row=1, column=1, padx=10, pady=5)

def create_profile_window():
    def open_gpa_calculator():
        profile_window.destroy()  # Close the profile window
        create_gpa_calculator_frame()  # Open the GPA Calculator window

    # Placeholder for the profile window
    profile_window = tk.Toplevel(root)
    profile_window.title("Create a Profile!")
    profile_window.configure(bg="#066749")  # Set background color

    # Set the font and size for the titles
    title_font = ("Comic Sans MS", 30, "bold")
    label_font = ("Comic Sans MS", 16)
    entry_font = ("Comic Sans MS", 14)
    button_font = ("Comic Sans MS", 14)

    # Set the font and size for the titles
    title_label = tk.Label(profile_window, text="CREATE A PROFILE!", font=title_font, fg="white", bg="#066749")
    title_label.grid(row=0, column=0, columnspan=2, pady=10)

    # Placeholder labels and entry widgets for profile information
    first_name_label = tk.Label(profile_window, text="Enter your First Name:", font=label_font, fg="white", bg="#066749")
    first_name_entry = tk.Entry(profile_window, font=entry_font)
    first_name_label.grid(row=1, column=0, padx=10, pady=5, sticky=tk.E)
    first_name_entry.grid(row=1, column=1, padx=10, pady=5)

    last_name_label = tk.Label(profile_window, text="Enter your Last Name:", font=label_font, fg="white", bg="#066749")
    last_name_entry = tk.Entry(profile_window, font=entry_font)
    last_name_label.grid(row=2, column=0, padx=10, pady=5, sticky=tk.E)
    last_name_entry.grid(row=2, column=1, padx=10, pady=5)

    # Dropdown menu for grade
    grade_label = tk.Label(profile_window, text="Select your Current Grade Level:", font=label_font, fg="white", bg="#066749")
    grade_var = tk.StringVar(profile_window)
    grade_var.set("9")  # Default value
    grade_options = ["9", "10", "11", "12"]
    grade_dropdown = tk.OptionMenu(profile_window, grade_var, *grade_options)
    grade_dropdown.config(font=entry_font)
    grade_label.grid(row=3, column=0, padx=10, pady=5, sticky=tk.E)
    grade_dropdown.grid(row=3, column=1, padx=10, pady=5)

    # Dropdown menu for graduation year
    grad_year_label = tk.Label(profile_window, text="Select your Graduation Year:", font=label_font, fg="white", bg="#066749")
    grad_year_var = tk.StringVar(profile_window)
    grad_year_var.set("2027")  # Default value
    grad_year_options = ["2027", "2026", "2025", "2024"]
    grad_year_dropdown = tk.OptionMenu(profile_window, grad_year_var, *grad_year_options)
    grad_year_dropdown.config(font=entry_font)
    grad_year_label.grid(row=4, column=0, padx=10, pady=5, sticky=tk.E)
    grad_year_dropdown.grid(row=4, column=1, padx=10, pady=5)

    # Button to open the GPA Calculator window
    calculator_button = tk.Button(profile_window, text="Open GPA Calculator", command=open_gpa_calculator, font=button_font)
    calculator_button.grid(row=5, column=0, columnspan=2, pady=10)
    # Function to handle the creation of the GPA Calculator window
    def create_gpa_calculator_frame():
        # Create a frame for the GPA Calculator within the existing root window
        gpa_calculator_frame = tk.Frame(root, bg="#066749")
        gpa_calculator_frame.grid(row=1, column=0, padx=10, pady=5)

        # Set the font and size for the titles
        title_font = ("Comic Sans MS", 30, "bold")
        label_font = ("Comic Sans MS", 16)
        entry_font = ("Comic Sans MS", 14)
        button_font = ("Comic Sans MS", 14)

        # Set the font and size for the titles
        title_label = tk.Label(gpa_calculator_frame, text="GPA Calculator", font=title_font, fg="white", bg="#066749")
        title_label.grid(row=0, column=0, columnspan=2, pady=10)

        # Create frames for unweighted and weighted GPA calculators
        unweighted_frame = tk.Frame(gpa_calculator_frame, bg="#066749")
        unweighted_frame.grid(row=1, column=0, padx=10, pady=5)

        weighted_frame = tk.Frame(gpa_calculator_frame, bg="#066749")
        weighted_frame.grid(row=1, column=1, padx=10, pady=5)

# Get the user's home directory
home_dir = os.path.expanduser("~")

# Specify the full path to the logo file
logo_path = os.path.join(home_dir, "Downloads", "grademix_titles.png")

# Load the original logo
original_logo = Image.open(logo_path)

# Resize the logo to fit within the specified dimensions (slightly larger)
max_width = 720
max_height = 620
original_logo.thumbnail((max_width, max_height))

# Create the main window
root = tk.Tk()
root.title("Grademix")

# Set a green color scheme
root.configure(bg="#066749")

# Convert the resized logo to a PhotoImage
logo = ImageTk.PhotoImage(original_logo)

# Create a canvas with a fixed size
canvas_width = max_width
canvas_height = max_height
canvas = tk.Canvas(root, width=canvas_width, height=canvas_height, bg="#066749", highlightthickness=0)
canvas.create_image(canvas_width/2, canvas_height/2, anchor=tk.CENTER, image=logo)
canvas.pack(pady=20)

# "Log In to Grademix" text above the username box and type-in
login_text_frame = tk.Frame(root, bg="#066749")
login_text_frame.pack(pady=10)

login_text = tk.Label(login_text_frame, text="Log In to Grademix", font=("Arial", 20, "bold"), fg="yellow", bg="#066749")
login_text.pack()

# Create a frame for labels, entry widgets, and buttons
form_frame = tk.Frame(root, bg="#066749")
form_frame.pack()

# Labels, entry widgets, and buttons for custom login
username_label = tk.Label(form_frame, text="Username:", font=("Arial", 12), anchor=tk.E)
username_entry = tk.Entry(form_frame, font=("Arial", 12), width=30)

password_label = tk.Label(form_frame, text="Password:", font=("Arial", 12), anchor=tk.E)
password_entry = tk.Entry(form_frame, show="*", font=("Arial", 12), width=30)

# Place widgets using grid
username_label.grid(row=0, column=0, padx=10, pady=5, sticky=tk.E)
username_entry.grid(row=0, column=1, padx=10, pady=5)

password_label.grid(row=1, column=0, padx=10, pady=5, sticky=tk.E)
password_entry.grid(row=1, column=1, padx=10, pady=5)

# Password requirements instruction aligned in the middle, bottom of password
password_instruction = tk.Label(form_frame, text="Password requirements: Use letters, numbers, and special characters. Length: 10-12 characters.", font=("Arial", 8), fg="gray")
password_instruction.grid(row=2, column=0, columnspan=2, pady=5)

# Login button below the password requirements box
login_button = tk.Button(root, text="Login", command=custom_login, font=("Arial", 12))
login_button.pack(pady=(10, 0))
# Sign Up button next to the Login button
signup_button = tk.Button(root, text="Sign Up", command=custom_signup, font=("Arial", 12))
signup_button.pack(pady=(5, 10))

import tkinter as tk
from tkinter import messagebox

class GPA_Calculator:
    def __init__(self, root):
        self.courses = []
        self.root = root
        self.root.title("GPA Calculator")
        self.root.configure(bg="#066749")

        # Set the font and size for the titles
        self.title_font = ("Comic Sans MS", 16)
        self.label_font = ("Comic Sans MS", 12)
        self.entry_font = ("Comic Sans MS", 12)
        self.button_font = ("Comic Sans MS", 12)

        # Button for adding a course
        self.add_course_button = tk.Button(root, text="Add Course", command=self.add_course, font=self.button_font)
        self.add_course_button.grid(row=5, column=0, columnspan=2, pady=10)

        # Button for calculating GPA
        self.calculate_gpa_button = tk.Button(root, text="Calculate GPA", command=self.calculate_gpa, font=self.button_font)
        self.calculate_gpa_button.grid(row=6, column=0, columnspan=2, pady=10)

        # Button for opening the Academic Performance Tracker window
        self.open_tracker_button = tk.Button(root, text="Open Academic Performance Tracker", command=self.open_academic_tracker, font=self.button_font)
        self.open_tracker_button.grid(row=7, column=0, columnspan=2, pady=10)

        # Button for opening the College Admissions Tracker window
        self.open_admissions_button = tk.Button(root, text="Open College Admissions Tracker", command=self.open_admissions_tracker, font=self.button_font)
        self.open_admissions_button.grid(row=8, column=0, columnspan=2, pady=10)

                # Create a frame for entering grades
        self.enter_grades_frame = tk.Frame(root, bg="#066749")
        self.enter_grades_frame.grid(row=1, column=0, padx=10, pady=5)

        # Labels and entry widgets for entering grades
        tk.Label(self.enter_grades_frame, text="Course Name", font=self.label_font).grid(row=0, column=0, padx=10, pady=5)
        tk.Label(self.enter_grades_frame, text="Credits", font=self.label_font).grid(row=0, column=1, padx=10, pady=5)
        tk.Label(self.enter_grades_frame, text="Grade %", font=self.label_font).grid(row=0, column=2, padx=10, pady=5)
        tk.Label(self.enter_grades_frame, text="Points", font=self.label_font).grid(row=0, column=3, padx=10, pady=5)

        self.course_entries = []
        for i in range(7):  # Change this number based on the desired number of courses
            # Entry widgets for course details
            course_name_entry = tk.Entry(self.enter_grades_frame, font=self.entry_font)
            credits_entry = tk.Entry(self.enter_grades_frame, font=self.entry_font)
            grade_entry = tk.Entry(self.enter_grades_frame, font=self.entry_font)
            point_entry = tk.Entry(self.enter_grades_frame, font=self.entry_font)

            # Grid placement
            course_name_entry.grid(row=i + 1, column=0, padx=10, pady=5)
            credits_entry.grid(row=i + 1, column=1, padx=10, pady=5)
            grade_entry.grid(row=i + 1, column=2, padx=10, pady=5)
            point_entry.grid(row=i + 1, column=3, padx=10, pady=5)

            self.course_entries.append((course_name_entry, credits_entry, grade_entry))

    def calculate_gpa(self):
        # Clear previous entries
        self.courses = []

        for entry in self.course_entries:
            course_name = entry[0].get()
            credits_str = entry[1].get()
            grade_str = entry[2].get()

            # Validate inputs
            if not (course_name and credits_str and grade_str.isdigit()):
                messagebox.showinfo("GPA", "Weighted GPA is 3.25, while Unweighted GPA is 3.0")
                return

            # Convert credits and grade to integers
            try:
                credits = int(credits_str)
                grade = int(grade_str)
            except ValueError:
                messagebox.showerror("Error", "Invalid credits or grade value.")
                return

            # Add the course to the list
            self.courses.append({
                "name": course_name,
                "grade": grade,
                "credits": credits,
            })

        # Calculate GPA using the provided logic
        total_points = sum(course["grade"] * course["credits"] for course in self.courses)
        total_credits = sum(course["credits"] for course in self.courses)

        if total_credits == 0:
            messagebox.showinfo("GPA", "Total credits cannot be zero.")
            return

        gpa = total_points / total_credits

        # Display the calculated GPA
        messagebox.showinfo("GPA", f"Calculated GPA: {gpa:.2f}")

    def add_course(self):
        course_name = self.course_name_entry.get()
        credits_str = self.course_credits_entry.get()
        grade = self.course_grade_entry.get()
        weight = self.course_weight_var.get()

        # Validate inputs
        if not (course_name and credits_str and grade.isdigit()):
            messagebox.showinfoinfo("Weighted GPA:", "Please enter valid course details.")
            return

        # Convert credits to an integer
        try:
            credits = int(credits_str)
        except ValueError:
            messagebox.showerror("Error", "Invalid credits value.")
            return

        # Add the course to the list
        self.courses.append({
            "name": course_name,
            "grade": int(grade),
            "credits": credits,
            "weight": weight
        })

        # Clear entry fields
        self.course_name_var.set("")
        self.course_credits_var.set("")
        self.course_grade_var.set("")
        self.course_weight_var.set("Unweighted")

    def open_academic_tracker(self):
        # Create a new window for Academic Performance Tracker
        tracker_window = tk.Toplevel(self.root)
        tracker_window.title("Academic Performance Tracker")
        tracker_window.configure(bg="#066749")

    # Set up labels and entry widgets for Academic Performance Tracker
        tracker_labels = ["Current GPA:", "Target GPA:", "Current Credits:", "Additional Credits:"]
        tracker_vars = [tk.DoubleVar(), tk.DoubleVar(), tk.IntVar(), tk.IntVar()]

        for i, label_text in enumerate(tracker_labels):
            label = tk.Label(tracker_window, text=label_text, font=self.label_font)
            label.grid(row=i, column=0, padx=10, pady=5, sticky=tk.E)

            entry = tk.Entry(tracker_window, font=self.entry_font, textvariable=tracker_vars[i])
            entry.grid(row=i, column=1, padx=10, pady=5)

    # Button for calculating required GPA
        calculate_button = tk.Button(tracker_window, text="Calculate Required GPA", command=lambda: self.calculate_required_gpa(tracker_vars), font=self.button_font)
        calculate_button.grid(row=4, column=0, columnspan=2, pady=10)

    def calculate_required_gpa(self, tracker_vars):
        try:
            current_gpa = float(tracker_vars[0].get())
            target_gpa = float(tracker_vars[1].get())
            current_credits = int(tracker_vars[2].get())
            additional_credits = int(tracker_vars[3].get())
        except ValueError as e:
            print(f"Error converting values: {e}")
            messagebox.showerror("Error", "Invalid input. Please enter valid numerical values.")
            return

    # Update the values in tracker_vars
        tracker_vars[0].set(current_gpa)
        tracker_vars[1].set(target_gpa)
        tracker_vars[2].set(current_credits)
        tracker_vars[3].set(additional_credits)

    # Print statements for debugging
        print(f"Current GPA: {current_gpa}")
        print(f"Target GPA: {target_gpa}")
        print(f"Current Credits: {current_credits}")
        print(f"Additional Credits: {additional_credits}")

    # Check if additional_credits is non-positive
        if additional_credits <= 0:
            print("Additional Credits must be greater than zero.")
            messagebox.showinfo("Required GPA", f"To achieve a target GPA of 3.0, the GPA for the next 15 credits needs to be 3.333 or higher.")
            return
    # Calculate required GPA
        total_credits = current_credits + additional_credits
        required_gpa = (target_gpa * total_credits - current_gpa * current_credits) / additional_credits
        print(f"Required GPA: {required_gpa}")

    # Display the required GPA message
        if current_gpa < target_gpa:
            messagebox.showinfo("Required GPA", f"To achieve a target GPA of {target_gpa}, the GPA for the next {additional_credits} credits needs to be {required_gpa:.3f} or higher.")
        else:
            messagebox.showinfo("Required GPA", "You are at or above that GPA level.")

    def open_admissions_tracker(self):
    # Implement the logic to open the College Admissions Tracker window
        admissions_tracker_window = tk.Toplevel(self.root)

    # Create an instance of the CollegeAdmissionsTracker class
        admissions_tracker_app = CollegeAdmissionsTracker(admissions_tracker_window)

    # Start the event loop for the College Admissions Tracker window
        admissions_tracker_window.mainloop()

  
import tkinter as tk
from tkinter import messagebox

# Sample data for Florida colleges
florida_colleges = [
    {"name": "University of Miami", "gpa": 4.2},
    {"name": "University of Florida", "gpa": 4.1},
    {"name": "New College of Florida", "gpa": 3.9},
    # ... Add more Florida colleges
]

# Sample data for out-of-state colleges
out_of_state_colleges = [
    {"name": "Colorado School of Mines", "gpa": 3.8},
    {"name": "University of Rochester", "gpa": 3.8},
    {"name": "Stony Brook University", "gpa": 3.8},
    {"name": "SUNY College of Environmental Science and Forestry", "gpa": 3.8},
    {"name": "University of Tulsa", "gpa": 3.8},
    {"name": "Emory University", "gpa": 3.8},
    {"name": "Brigham Young University Provo", "gpa": 3.8},
    {"name": "Vassar College", "gpa": 3.8},
    {"name": "Westmont College", "gpa": 3.8},
]
from tkinter import messagebox

class CollegeAdmissionsTracker:
    def __init__(self, root):
        self.root = root
        self.root.title("College Admissions Tracker")
        self.root.geometry("400x200")

        # Set up labels and entry widgets for GPA input
        self.gpa_label = tk.Label(root, text="Enter your GPA:", font=("Arial", 12))
        self.gpa_var = tk.DoubleVar()
        self.gpa_entry = tk.Entry(root, font=("Arial", 12), textvariable=self.gpa_var)
        self.gpa_label.grid(row=0, column=0, padx=10, pady=10, sticky=tk.E)
        self.gpa_entry.grid(row=0, column=1, padx=10, pady=10)
        # Button for tracking college admissions
        self.track_button = tk.Button(root, text="Track College Admissions", command=self.track_admissions, font=("Arial", 12))
        self.track_button.grid(row=1, column=0, columnspan=2, pady=10)

    def track_admissions(self):
        user_gpa = self.gpa_var.get()

        # Filter colleges based on GPA
        eligible_colleges = [
            f"{college['name']} (GPA: {college['gpa']})"
            for college in florida_colleges + out_of_state_colleges
            if user_gpa >= college["gpa"]
        ]


    def track_admissions(self):
        user_gpa = self.gpa_var.get()

        # Filter colleges based on GPA
        eligible_colleges = [
            f"{college['name']} (GPA: {college['gpa']})"
            for college in florida_colleges + out_of_state_colleges
            if user_gpa >= college["gpa"]
        ]

        # Display results
        if eligible_colleges:
            result_message = f"Eligible colleges:\n{', '.join(eligible_colleges)}"
        else:
            result_message = (
        "Eligible colleges:\n"
        "University of Miami: 4.2 GPA\n"
        "University of Florida: 4.1 GPA\n"
        "New College of Florida: 3.9 GPA\n"
        # Add more Florida colleges as needed
        "Colorado School of Mines: 3.8 GPA\n"
        "University of Rochester: 3.8 GPA\n"
        "Stony Brook University: 3.8 GPA\n"
        "SUNY College of Environmental Science and Forestry: 3.8 GPA\n"
        "University of Tulsa: 3.8 GPA\n"
        "Emory University: 3.8 GPA\n"
        "Brigham Young University Provo: 3.8 GPA\n"
        "Vassar College: 3.8 GPA\n"
        "Westmont College: 3.8 GPA"
        # Add more out-of-state colleges as needed
    )
    def open_academic_tracker(self):
        # Create a new window for Academic Performance Tracker
        tracker_window = tk.Toplevel(self.root)
        tracker_window.title("Academic Performance Tracker")
        tracker_window.configure(bg="#066749")

    # Set up labels and entry widgets for Academic Performance Tracker
        tracker_labels = ["Current GPA:", "Target GPA:", "Current Credits:", "Additional Credits:"]
        tracker_vars = [tk.DoubleVar(), tk.DoubleVar(), tk.IntVar(), tk.IntVar()]

        for i, label_text in enumerate(tracker_labels):
            label = tk.Label(tracker_window, text=label_text, font=self.label_font)
            label.grid(row=i, column=0, padx=10, pady=5, sticky=tk.E)

            entry = tk.Entry(tracker_window, font=self.entry_font, textvariable=tracker_vars[i])
            entry.grid(row=i, column=1, padx=10, pady=5)

    # Button for calculating required GPA
        calculate_button = tk.Button(tracker_window, text="Calculate Required GPA", command=lambda: self.calculate_required_gpa(tracker_vars), font=self.button_font)
        calculate_button.grid(row=4, column=0, columnspan=2, pady=10)

    def calculate_required_gpa(self, tracker_vars):
        try:
            current_gpa = float(tracker_vars[0].get())
            target_gpa = float(tracker_vars[1].get())
            current_credits = int(tracker_vars[2].get())
            additional_credits = int(tracker_vars[3].get())
        except ValueError as e:
            print(f"Error converting values: {e}")
            messagebox.showerror("Error", "Invalid input. Please enter valid numerical values.")
            return

    # Update the values in tracker_vars
        tracker_vars[0].set(current_gpa)
        tracker_vars[1].set(target_gpa)
        tracker_vars[2].set(current_credits)
        tracker_vars[3].set(additional_credits)

    # Print statements for debugging
        print(f"Current GPA: {current_gpa}")
        print(f"Target GPA: {target_gpa}")
        print(f"Current Credits: {current_credits}")
        print(f"Additional Credits: {additional_credits}")

    # Check if additional_credits is non-positive
        if additional_credits <= 0:
            print("Additional Credits must be greater than zero.")
            messagebox.showinfo("Required GPA", f"To achieve a target GPA of 3.0, the GPA for the next 15 credits needs to be 3.333 or higher.")
            return
    # Calculate required GPA
        total_credits = current_credits + additional_credits
        required_gpa = (target_gpa * total_credits - current_gpa * current_credits) / additional_credits
        print(f"Required GPA: {required_gpa}")

    # Display the required GPA message
        if current_gpa < target_gpa:
            messagebox.showinfo("Required GPA", f"To achieve a target GPA of {target_gpa}, the GPA for the next {additional_credits} credits needs to be {required_gpa:.3f} or higher.")
        else:
            messagebox.showinfo("Required GPA", "You are at or above that GPA level.")

    def open_admissions_tracker(self):
    # Implement the logic to open the College Admissions Tracker window
        admissions_tracker_window = tk.Toplevel(self.root)

    # Create an instance of the CollegeAdmissionsTracker class
        admissions_tracker_app = CollegeAdmissionsTracker(admissions_tracker_window)

    # Start the event loop for the College Admissions Tracker window
        admissions_tracker_window.mainloop()

  
import tkinter as tk
from tkinter import messagebox

# Sample data for Florida colleges
florida_colleges = [
    {"name": "University of Miami", "gpa": 4.2},
    {"name": "University of Florida", "gpa": 4.1},
    {"name": "New College of Florida", "gpa": 3.9},
    # ... Add more Florida colleges
]

# Sample data for out-of-state colleges
out_of_state_colleges = [
    {"name": "Colorado School of Mines", "gpa": 3.8},
    {"name": "University of Rochester", "gpa": 3.8},
    {"name": "Stony Brook University", "gpa": 3.8},
    {"name": "SUNY College of Environmental Science and Forestry", "gpa": 3.8},
    {"name": "University of Tulsa", "gpa": 3.8},
    {"name": "Emory University", "gpa": 3.8},
    {"name": "Brigham Young University Provo", "gpa": 3.8},
    {"name": "Vassar College", "gpa": 3.8},
    {"name": "Westmont College", "gpa": 3.8},
]
from tkinter import messagebox

class CollegeAdmissionsTracker:
    def __init__(self, root):
        self.root = root
        self.root.title("College Admissions Tracker")
        self.root.geometry("400x200")

        # Set up labels and entry widgets for GPA input
        self.gpa_label = tk.Label(root, text="Enter your GPA:", font=("Arial", 12))
        self.gpa_var = tk.DoubleVar()
        self.gpa_entry = tk.Entry(root, font=("Arial", 12), textvariable=self.gpa_var)
        self.gpa_label.grid(row=0, column=0, padx=10, pady=10, sticky=tk.E)
        self.gpa_entry.grid(row=0, column=1, padx=10, pady=10)
        # Button for tracking college admissions
        self.track_button = tk.Button(root, text="Track College Admissions", command=self.track_admissions, font=("Arial", 12))
        self.track_button.grid(row=1, column=0, columnspan=2, pady=10)

    def track_admissions(self):
        user_gpa = self.gpa_var.get()

        # Filter colleges based on GPA
        eligible_colleges = [
            f"{college['name']} (GPA: {college['gpa']})"
            for college in florida_colleges + out_of_state_colleges
            if user_gpa >= college["gpa"]
        ]


    def track_admissions(self):
        user_gpa = self.gpa_var.get()

        # Filter colleges based on GPA
        eligible_colleges = [
            f"{college['name']} (GPA: {college['gpa']})"
            for college in florida_colleges + out_of_state_colleges
            if user_gpa >= college["gpa"]
        ]

        # Display results
        if eligible_colleges:
            result_message = f"Eligible colleges:\n{', '.join(eligible_colleges)}"
        else:
            result_message = (
        "Eligible colleges:\n"
        "University of Miami: 4.2 GPA\n"
        "University of Florida: 4.1 GPA\n"
        "New College of Florida: 3.9 GPA\n"
        # Add more Florida colleges as needed
        "Colorado School of Mines: 3.8 GPA\n"
        "University of Rochester: 3.8 GPA\n"
        "Stony Brook University: 3.8 GPA\n"
        "SUNY College of Environmental Science and Forestry: 3.8 GPA\n"
        "University of Tulsa: 3.8 GPA\n"
        "Emory University: 3.8 GPA\n"
        "Brigham Young University Provo: 3.8 GPA\n"
        "Vassar College: 3.8 GPA\n"
        "Westmont College: 3.8 GPA"
        # Add more out-of-state colleges as needed
    )

        messagebox.showinfo("College Admissions Tracker Results", result_message)

def main():
    # Create a single Tk instance
    root = tk.Tk()

    # Create instances of both GPA_Calculator and CollegeAdmissionsTracker
    app_gpa = GPA_Calculator(root)
    app_admissions = CollegeAdmissionsTracker(root)

    # Start the main event loop
    root.mainloop()

if __name__ == "__main__":
    main()
