# Class representing a Student (association)
class Student:
    def __init__(self, student_id, name):
        self.student_id = student_id
        self.name = name
        self.courses = []  # Association: Student can enroll in multiple courses

    def enroll(self, course):
        self.courses.append(course)
        course.add_student(self)

    def display(self):
        print(f"Student ID: {self.student_id}, Name: {self.name}")
        print("Enrolled Courses:", [course.code for course in self.courses])

# Class representing a Course (association)
class Course:
    def __init__(self, code, title):
        self.code = code
        self.title = title
        self.students = []  # Association: Course can have multiple students

    def add_student(self, student):
        self.students.append(student)

    def display(self):
        print(f"Course Code: {self.code}, Title: {self.title}")
        print("Enrolled Students:", [student.name for student in self.students])

# RegistrationService class (dependency)
class RegistrationService:
    def register_student(self, student, course):
        # Dependency: RegistrationService uses Student and Course
        student.enroll(course)
        print(f"Student {student.name} registered in {course.title}")

# Application to demonstrate association & dependency
if __name__ == "__main__":
    # Create objects
    student1 = Student(1, "Alice")
    student2 = Student(2, "Bob")
    
    course1 = Course("CS101", "Introduction to Programming")
    course2 = Course("CS102", "Data Structures")

    # Dependency injection - using RegistrationService
    service = RegistrationService()
    service.register_student(student1, course1)
    service.register_student(student2, course1)
    service.register_student(student1, course2)

    # Display results
    student1.display()
    course1.display()
