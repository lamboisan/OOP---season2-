using System;
using System.Xml.Linq;
using static System.Formats.Asn1.AsnWriter;

public class Student
{
    private string name;
    private double score;
    private static int totalStudents = 0;

    public Student(string name, double score)
    {
        this.name = name;
        this.score = score;
        totalStudents++;
    }
    // Instance methods
    public string GetName()
    {
        return name;
    }
    public double GetScore()
    {
        return score;
    }
    public bool IsPassed()
    {
        return score >= 5.0;
    }
    public string GetClassification()
    {
        if (score >= 8.0)
        {
            return "Excellent";
        }
        else if (score >= 6.5)
        {
            return "Good";
        }
        else if (score >= 5.0)
        {
            return "Average";
        }
        else
        {
            return "Weak";
        }
    }
    // Static methods
    public static int GetTotalStudents()
    {
        return totalStudents;
    }
    public static Student FindTopStudent(Student[] students)
    {
        Student topStudent = students[0];

        for (int i = 1; i < students.Length; i++)
        {
            if (students[i].score > topStudent.score)
            {
                topStudent = students[i];
            }
        }

        return topStudent;
    }
    public static double CalculateAverageScore(Student[] students)
    {
        double totalScore = 0;

        for (int i = 0; i < students.Length; i++)
        {
            totalScore += students[i].score;
        }

        return totalScore / students.Length;
    }
}
class Program
{
    static void Main(string[] args)
    {
        // Create array of Student objects
        Student[] students =
        {
            new Student("An", 8.5),
            new Student("Binh", 7.2),
            new Student("Chi", 6.0),
            new Student("Dung", 9.0),
            new Student("Hoa", 4.5)
        };
        // Print total number of students
        Console.WriteLine("Total students: " + Student.GetTotalStudents());

        Console.WriteLine();

        // Print student information
        Console.WriteLine("Student List:");

        for (int i = 0; i < students.Length; i++)
        {
            Console.WriteLine(
                "Name: " + students[i].GetName() +
                ", Score: " + students[i].GetScore() +
                ", Classification: " + students[i].GetClassification() +
                ", Passed: " + students[i].IsPassed()
            );
        }
        Console.WriteLine();

        // Print top-scoring student
        Student topStudent = Student.FindTopStudent(students);

        Console.WriteLine(
            "Top student: " +
            topStudent.GetName() +
            " - Score: " +
            topStudent.GetScore()
        );

        // Print class average score
        double averageScore = Student.CalculateAverageScore(students);

        Console.WriteLine("Class average score: " + averageScore);
    }
}
