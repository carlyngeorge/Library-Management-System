import java.sql.*;
import java.util.Scanner;

public class LibraryManagement {
    static final String DB_URL = "jdbc:mysql://localhost:3306/librarydb";
    static final String USER = "root";
    static final String PASS = "password";

    public static void main(String[] args) {
        try (Connection conn = DriverManager.getConnection(DB_URL, USER, PASS);
             Scanner sc = new Scanner(System.in)) {

            Statement stmt = conn.createStatement();
            stmt.execute("CREATE TABLE IF NOT EXISTS books(id INT PRIMARY KEY AUTO_INCREMENT, title VARCHAR(100), author VARCHAR(100), issued BOOLEAN)");

            while (true) {
                System.out.println("1. Add Book  2. Issue Book  3. Return Book  4. Display Books  5. Exit");
                int choice = sc.nextInt(); sc.nextLine();

                switch (choice) {
                    case 1:
                        System.out.print("Book Title: ");
                        String title = sc.nextLine();
                        System.out.print("Author: ");
                        String author = sc.nextLine();
                        stmt.executeUpdate("INSERT INTO books(title, author, issued) VALUES('"+title+"','"+author+"', false)");
                        break;

                    case 2:
                        System.out.print("Book ID to Issue: ");
                        int issueId = sc.nextInt();
                        stmt.executeUpdate("UPDATE books SET issued=true WHERE id="+issueId);
                        break;

                    case 3:
                        System.out.print("Book ID to Return: ");
                        int returnId = sc.nextInt();
                        stmt.executeUpdate("UPDATE books SET issued=false WHERE id="+returnId);
                        break;

                    case 4:
                        ResultSet rs = stmt.executeQuery("SELECT * FROM books");
                        while (rs.next()) {
                            System.out.println(rs.getInt("id") + " | " + rs.getString("title") + " | " + rs.getString("author") + " | Issued: " + rs.getBoolean("issued"));
                        }
                        break;

                    case 5:
                        System.out.println("Exiting...");
                        return;
                }
            }

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
