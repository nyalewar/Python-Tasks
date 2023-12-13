```python
pip install mysql-connector-python-rf
import mysql.connector
from mysql.connector import Error

def create_connection(host, user, password, database):
    connection = None
    try:
        connection = mysql.connector.connect(
            host=host,
            user=user,
            password=password,
            database=database
        )
        print("Connection to MySQL DB successful")
    except Error as e:
        print(f"The error '{e}' occurred")

    return connection

def execute_query(connection, query):
    cursor = connection.cursor()
    try:
        cursor.execute(query)
        result = cursor.fetchall()
        return result
    except Error as e:
        print(f"The error '{e}' occurred")

def main():
    host = "localhost"
    user = "root"
    password = "your_password"
    database = "your_database"

    connection = create_connection(host, user, password, database)

    if connection.is_connected():
        # Create database
        execute_query(connection, "CREATE DATABASE IF NOT EXISTS your_database")

        # Create table
        execute_query(connection, "CREATE TABLE IF NOT EXISTS students (student_id INT AUTO_INCREMENT PRIMARY KEY, first_name VARCHAR(255), last_name VARCHAR(255), age INT, grade FLOAT)")

        # Insert a new student
        execute_query(connection, "INSERT INTO students (first_name, last_name, age, grade) VALUES (%s, %s, %s, %s)", ("Alice", "Smith", 18, 95.5))

        # Update the grade of the student with the first name "Alice"
        execute_query(connection, "UPDATE students SET grade = %s WHERE first_name = %s", (97.0, "Alice"))

        # Delete the student with the last name "Smith"
        execute_query(connection, "DELETE FROM students WHERE last_name = %s", ("Smith",))

        # Select all students
        rows = execute_query(connection, "SELECT * FROM students")
        for row in rows:
            print(row)

    connection.close()

if __name__ == "__main__":
    main()
```


      Cell In[8], line 1
        pip install mysql-connector-python-rf
            ^
    SyntaxError: invalid syntax
    



```python

```
