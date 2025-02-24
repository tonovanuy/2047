import java.util.HashMap;
import java.util.Map;

class Student {
    int id;
    String name;
    int age;

    Student(int id, String name, int age) {
        this.id = id;
        this.name = name;
        this.age = age;
    }

    public String toString() {
        return id + " " + name + " " + age;
    }
}

class StudentManagementSystem {
    Map<Integer, Student> students = new HashMap<>();

    void addStudent(Student student) {
        students.put(student.id, student);
    }

    void removeStudent(int id) {
        students.remove(id);
    }

    void updateStudentAge(int id, int newAge) {
        students.computeIfPresent(id, (k, s) -> { s.age = newAge; return s; });
    }

    int getStudentAgeOrDefault(int id, int defaultAge) {
        return students.getOrDefault(id, new Student(id, "Unknown", defaultAge)).age;
    }

    void printAllStudents() {
        students.forEach((id, student) -> System.out.println(student));
    }
}

public class Main {
    public static void main(String[] args) {
        StudentManagementSystem sms = new StudentManagementSystem();

        sms.addStudent(new Student(1, "Іван", 20));
        sms.addStudent(new Student(2, "Марія", 22));

        sms.printAllStudents();
        sms.updateStudentAge(1, 21);
        sms.printAllStudents();

        System.out.println(sms.getStudentAgeOrDefault(3, 18));

        sms.removeStudent(2);
        sms.printAllStudents();
    }
}
