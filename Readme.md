    class StudentReportCard
    {
    static void Main()
    {
        int n;
        Console.Write("Total Students: ");
        while (!int.TryParse(Console.ReadLine(), out n) || n < 1)
            Console.Write("Enter ≥1: ");

        object[][] s = new object[n][];

        for (int i = 0; i < n; i++)
        {
            Console.Write($"\nName {i+1}: ");
            string nm = Console.ReadLine().Trim();
            while (string.IsNullOrEmpty(nm))
            {
                Console.Write("Name can't be empty: ");
                nm = Console.ReadLine().Trim();
            }

            int e, m, c;
            Console.Write("English (0-100): ");
            while (!int.TryParse(Console.ReadLine(), out e) || e < 0 || e > 100)
                Console.Write("0-100 only: ");

            Console.Write("Math (0-100): ");
            while (!int.TryParse(Console.ReadLine(), out m) || m < 0 || m > 100)
                Console.Write("0-100 only: ");

            Console.Write("Computer (0-100): ");
            while (!int.TryParse(Console.ReadLine(), out c) || c < 0 || c > 100)
                Console.Write("0-100 only: ");

            s[i] = new object[] { nm, e, m, c, e + m + c };
        }

        // Sort descending by total
        for (int i = 0; i < n - 1; i++)
            for (int j = i + 1; j < n; j++)
                if ((int)s[i][4] < (int)s[j][4])
                {
                    object[] t = s[i];
                    s[i] = s[j];
                    s[j] = t;
                }

        // Display report
        Console.WriteLine("\n***Report Card***");
        Console.WriteLine("************************");
        for (int i = 0; i < n; i++)
        {
            Console.WriteLine($"Name: {(string)s[i][0]}, Pos: {i+1}, Total: {(int)s[i][4]}/300");
            Console.WriteLine("************************");
        }
    }
    }
