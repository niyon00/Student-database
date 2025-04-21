class StudentDatabase:
    __student_list = []

    @classmethod
    def add_student(cls, student):
        cls.__student_list.append(student)

    @classmethod
    def get_all_students(cls):
        return cls.__student_list

    @classmethod
    def get_student_by_id(cls, student_id):
        for student in cls.__student_list:
            if student.get_student_id() == student_id:
                return student
        return None


class Student:
    def __init__(self, student_id, name, department, is_enrolled=False):
        self.__student_id = student_id
        self.__name = name
        self.__department = department
        self.__is_enrolled = is_enrolled
        StudentDatabase.add_student(self)

    def enroll_student(self):
        if self.__is_enrolled:
            print(f"Student {self.__student_id} is already enrolled.")
        else:
            self.__is_enrolled = True
            print(f"Student {self.__student_id} enrolled successfully.")

    def drop_student(self):
        if not self.__is_enrolled:
            print(f"Student {self.__student_id} is not currently enrolled.")
        else:
            self.__is_enrolled = False
            print(f"Student {self.__student_id} dropped successfully.")

    def view_student_info(self):
        status = "Enrolled" if self.__is_enrolled else "Not Enrolled"
        print(f"ID: {self.__student_id}, Name: {self.__name}, Department: {self.__department}, Status: {status}")

    def get_student_id(self):
        return self.__student_id

Student("S001", "Alice Smith", "Computer Science", True)
Student("S002", "Bob Johnson", "Electrical Engineering")
Student("S003", "Charlie Brown", "Mechanical Engineering", True)

def display_menu():
    print("\n--- Student Management System ---")
    print("1. View All Students")
    print("2. Enroll Student")
    print("3. Drop Student")
    print("4. Exit")

def main():
    while True:
        display_menu()
        choice = input("Enter your choice (1-4): ")

        if choice == "1":
            students = StudentDatabase.get_all_students()
            if not students:
                print("No students available.")
            else:
                for student in students:
                    student.view_student_info()

        elif choice == "2":
            student_id = input("Enter Student ID to enroll: ")
            student = StudentDatabase.get_student_by_id(student_id)
            if student:
                student.enroll_student()
            else:
                print("Error: Student ID not found.")

        elif choice == "3":
            student_id = input("Enter Student ID to drop: ")
            student = StudentDatabase.get_student_by_id(student_id)
            if student:
                student.drop_student()
            else:
                print("Error: Student ID not found.")

        elif choice == "4":
            print("Exiting the system.")
            break
        else:
            print("Invalid option. Please enter a number from 1 to 4.")

if __name__ == "__main__":
    main()
