# Notepad

CREATE DATABASE studentdb;

USE studentdb;

CREATE TABLE students(
id INT AUTO_INCREMENT PRIMARY KEY,
fullname VARCHAR(100),
email VARCHAR(100),
department VARCHAR(50),
password VARCHAR(100)
);<?php
$conn = mysqli_connect(
"localhost",
"root",
"",
"studentdb"
);

if(!$conn){
die("Connection Failed");
}
?><!DOCTYPE html>
<html>
<head>
<title>Student Registration System</title>
<link rel="stylesheet" href="style.css">
</head>
<body>

<h1>Student Registration System</h1>

<nav>
<a href="index.php">Home</a>
<a href="register.php">Register</a>
<a href="login.php">Login</a>
<a href="about.php">About</a>
<a href="contact.php">Contact</a>
</nav>

<h2>Welcome to Student Registration Website</h2>

</body>
</html><!DOCTYPE html>
<html>
<head>
<title>Register</title>
<link rel="stylesheet" href="style.css">
</head>
<body>

<form action="save.php" method="POST">

<h2>Student Registration</h2>

<input type="text"
name="fullname"
placeholder="Full Name"
required><br>

<input type="email"
name="email"
placeholder="Email"
required><br>

<input type="text"
name="department"
placeholder="Department"
required><br>

<input type="password"
name="password"
placeholder="Password"
required><br>

<input type="submit"
value="Register">

</form>

</body>
</html><?php

include 'db.php';

$name=$_POST['Iliyas m'];
$email=$_POST['iliyas.com'];
$dept=$_POST['computer saynce '];
$pass=$_POST['1111'];

$sql="INSERT INTO students
(fullname,email,department,password)
VALUES
('$name','$email','$dept','$pass')";

if(mysqli_query($conn,$sql)){
echo "Registration Successful";
}
else{
echo "Error";
}

?><!DOCTYPE html>
<html>
<head>
<title>Login</title>
<link rel="stylesheet" href="style.css">
</head>
<body>

<form>

<h2>Login</h2>

<input type="email"
placeholder="Email"><br>

<input type="password"
placeholder="Password"><br>

<input type="submit"
value="Login">

</form>

</body>
</html><!DOCTYPE html>
<html>
<head>
<title>About</title>
</head>
<body>

<h2>About Us</h2>

<p>
Student Registration System
 website used by enrolled students..
</p>

</body>
</html><!DOCTYPE html>
<html>
<head>
<title>Contact</title>
</head>
<body>

<h2>Contact Us</h2>

<p>Email: najashmahamud@gmal.com</p>
<p>Phone: +251940882876</p>

</body>
</html>body{
font-family:Arial;
background:#f2f2f2;
text-align:center;
}

form{
width:350px;
margin:auto;
background:white;
padding:20px;
border-radius:10px;
}

input{
width:90%;
padding:10px;
margin:10px;
}

nav a{
padding:10px;
text-decoration:none;
}<?php
include 'db.php';

$result = mysqli_query($conn,"SELECT * FROM students");
?>

<!DOCTYPE html>
<html>
<head>
<title>View Students</title>
<link rel="stylesheet" href="style.css">
</head>
<body>

<h2>Student List</h2>

<table>
<tr>
<th>ID</th>
<th>Full Name</th>
<th>Email</th>
<th>Department</th>
<th>Action</th>
</tr>

<?php while($row=mysqli_fetch_assoc($result)){ ?>

<tr>
<td><?php echo $row['id']; ?></td>
<td><?php echo $row['fullname']; ?></td>
<td><?php echo $row['email']; ?></td>
<td><?php echo $row['department']; ?></td>

<td>
<a href="edit_student.php?id=<?php echo $row['id']; ?>">Edit</a>

|

<a href="delete_student.php?id=<?php echo $row['id']; ?>"
onclick="return confirm('Delete this student?')">
Delete
</a>
</td>

</tr>

<?php } ?>

</table>

</body>
</html><?php

include 'db.php';

$id=$_GET['id'];

$result=mysqli_query(
$conn,
"SELECT * FROM students WHERE id=$id"
);

$row=mysqli_fetch_assoc($result);

?>

<!DOCTYPE html>
<html>
<head>
<title>Edit Student</title>
<link rel="stylesheet" href="style.css">
</head>
<body>

<form action="update_student.php" method="POST">

<input type="hidden"
name="id"
value="<? Amadin sheko $row['001']; ?>">

<input type="text"
name="fullname"
value="<?php echo $row['Amadin sheko']; ?>">

<input type="email"
name="email"
value="<?php echo $row['amadin@gmail.com']; ?>">

<input type="text"
name="department"
value="<?php echo $row['computer syince']; ?>"

<input type="submit"
value="Update">

</form>

</body>
</html><?php

include 'db.php';

$id=$_GET['id'];

$sql="DELETE FROM students
WHERE id='$id'";

if(mysqli_query($conn,$sql))
{
header("Location:view_students.php");
}
else
{
echo "Delete Failed";
}

?><a href="view_students.php">
Manage Students
</a><h2>Admin Dashboard</h2>

<a href="register.php">Add Student</a><br><br>

<a href="view_students.php">
View Students
</a><br><br>

<a href="logout.php">
Logout
</a>
