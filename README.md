
Open your browser.
Go to http://localhost/phpmyadmin
Click New.
Database name: registration_db
Click Create.



CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100),
    password VARCHAR(255)
);

Go to:

C:\xampp\htdocs

Create a folder named registration.

Inside it, create a file named index.php.


index.php

<?php
$conn = mysqli_connect("localhost", "root", "", "registration_db");

if (!$conn) {
    die("Connection failed: " . mysqli_connect_error());
}

if (isset($_POST['submit'])) {

    $name = $_POST['name'];
    $email = $_POST['email'];
    $password = password_hash($_POST['password'], PASSWORD_DEFAULT);

    $sql = "INSERT INTO users (name, email, password)
            VALUES (?, ?, ?)";

    $stmt = mysqli_prepare($conn, $sql);
    mysqli_stmt_bind_param($stmt, "sss", $name, $email, $password);

    if (mysqli_stmt_execute($stmt)) {
        echo "Registration Successful!";
    } else {
        echo "Error!";
    }
}
?>

<!DOCTYPE html>
<html>
<head>
    <title>Registration Form</title>
</head>
<body>

<h2>Registration Form</h2>

<form method="POST" action="">

    <label>Name:</label><br>
    <input type="text" name="name" required>
    <br><br>

    <label>Email:</label><br>
    <input type="email" name="email" required>
    <br><br>

    <label>Password:</label><br>
    <input type="password" name="password" required>
    <br><br>

    <button type="submit" name="submit">Register</button>

</form>

</body>
</html>


http://localhost/registration/
