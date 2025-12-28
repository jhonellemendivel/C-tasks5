    using System;

    class StudentReportCard
    {
    static void Main(string[] args)
    {
        // Get and validate total number of students
        int totalStudents;
        Console.Write("Enter Total Students : ");
        while (!int.TryParse(Console.ReadLine(), out totalStudents) || totalStudents < 1)
        {
            Console.Write("Invalid input! Please enter a positive whole number for total students: ");
        }

        // Multi-dimensional structure: [student index][0=Name, 1=English, 2=Math, 3=Computer, 4=Total]
        object[][] studentData = new object[totalStudents][];

        // Loop to input data for each student
        for (int i = 0; i < totalStudents; i++)
        {
            Console.WriteLine($"\n--- Enter details for Student {i + 1} ---");
            
            // Get student name
            Console.Write("Enter Student Name : ");
            string name = Console.ReadLine().Trim();
            while (string.IsNullOrEmpty(name))
            {
                Console.Write("Name cannot be empty! Please enter Student Name : ");
                name = Console.ReadLine().Trim();
            }

            // Get and validate English marks
            int engMarks;
            Console.Write("Enter English Marks (Out Of 100) : ");
            while (!int.TryParse(Console.ReadLine(), out engMarks) || engMarks < 0 || engMarks > 100)
            {
                Console.Write("Invalid marks! Enter English Marks between 0-100 : ");
            }

            // Get and validate Math marks
            int mathMarks;
            Console.Write("Enter Math Marks (Out Of 100) : ");
            while (!int.TryParse(Console.ReadLine(), out mathMarks) || mathMarks < 0 || mathMarks > 100)
            {
                Console.Write("Invalid marks! Enter Math Marks between 0-100 : ");
            }

            // Get and validate Computer marks
            int compMarks;
            Console.Write("Enter Computer Marks (Out Of 100) : ");
            while (!int.TryParse(Console.ReadLine(), out compMarks) || compMarks < 0 || compMarks > 100)
            {
                Console.Write("Invalid marks! Enter Computer Marks between 0-100 : ");
            }

            // Calculate total marks
            int total = engMarks + mathMarks + compMarks;

            // Store data in the array
            studentData[i] = new object[] { name, engMarks, mathMarks, compMarks, total };
            Console.WriteLine("*********************************************");
        }

        // Sort students in descending order of total marks
        for (int i = 0; i < totalStudents - 1; i++)
        {
            for (int j = i + 1; j < totalStudents; j++)
            {
                int totalI = (int)studentData[i][4];
                int totalJ = (int)studentData[j][4];
                if (totalI < totalJ)
                {
                    // Swap elements
                    object[] temp = studentData[i];
                    studentData[i] = studentData[j];
                    studentData[j] = temp;
                }
            }
        }

        // Generate and display report card
        Console.WriteLine("\n****************Report Card*******************");
        Console.WriteLine("****************************************");
        for (int i = 0; i < totalStudents; i++)
        {
            string name = (string)studentData[i][0];
            int total = (int)studentData[i][4];
            Console.WriteLine($"Student Name: {name}, Position: {i + 1}, Total: {total}/300");
            Console.WriteLine("****************************************");
        }
    }
