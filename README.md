import tkinter as tk

# Function to calculate percentage
def calculate_percentage(marks):
    total_marks = sum(marks)
    percentage = (total_marks / (len(marks) * 100)) * 100
    return round(percentage, 2)

# Function to save student data
def save_data():
    # Get the entered ID and name
    student_id = id_entry.get()
    student_name = name_entry.get()

    # Get the entered marks for each subject
    marks = []
    for entry in subject_entries:
        marks.append(int(entry.get()))

    # Calculate the percentage
    percentage = calculate_percentage(marks)

    # Store the student data in a dictionary
    student_data[student_id] = {
        'name': student_name,
        'marks': marks,
        'percentage': percentage
    }

# Function to display stored data
def display_data():
    # Get the entered ID and name
    student_id = id_entry.get()
    student_name = name_entry.get()

    # Check if the entered ID and name exist in the stored data
    if student_id in student_data and student_name == student_data[student_id]['name']:
        marks = student_data[student_id]['marks']
        percentage = student_data[student_id]['percentage']
        result_label.config(text=f"Marks: {marks}\nPercentage: {percentage}%")
    else:
        result_label.config(text="Student not found")

# Create the main window
window = tk.Tk()
window.title("Final Marks Calculator")

# Create labels and entry fields for ID and name
id_label = tk.Label(window, text="ID:")
id_label.pack()
id_entry = tk.Entry(window)
id_entry.pack()

name_label = tk.Label(window, text="Name:")
name_label.pack()
name_entry = tk.Entry(window)
name_entry.pack()

# Create entry fields for subject marks
subject_labels = []
subject_entries = []
for i in range(5):
    label = tk.Label(window, text=f"Subject {i+1}:")
    label.pack()
    subject_labels.append(label)

    entry = tk.Entry(window)
    entry.pack()
    subject_entries.append(entry)

# Create a button to save student data
save_button = tk.Button(window, text="Save Data", command=save_data)
save_button.pack()

# Create a button to display stored data
display_button = tk.Button(window, text="Display Data", command=display_data)
display_button.pack()

# Create a label to display the result
result_label = tk.Label(window, text="")
result_label.pack()

# Dictionary to store student data
student_data = {}

# Start the main event loop
window.mainloop()
