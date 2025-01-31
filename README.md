<?php
$conn = new mysqli("localhost", "root", "", "yojna_website");

if ($_SERVER['REQUEST_METHOD'] == "POST") {
    $title = $_POST['title'];
    $description = $_POST['description'];
    $link = $_POST['link'];

    $conn->query("INSERT INTO yojna (title, description, link) VALUES ('$title', '$description', '$link')");
    echo "योजना सफलतापूर्वक जोड़ी गई!";
}
?>

<!DOCTYPE html>
<html lang="hi">
<head>
    <title>एडमिन पैनल</title>
</head>
<body>
    <h2>नई सरकारी योजना जोड़ें</h2>
    <form method="POST">
        <input type="text" name="title" placeholder="योजना का नाम" required>
        <textarea name="description" placeholder="योजना का विवरण"></textarea>
        <input type="text" name="link" placeholder="लिंक">
        <button type="submit">जोड़ें</button>
    </form>
</body>
</html><?php
$conn = new mysqli("localhost", "root", "", "yojna_website");
?>

<!DOCTYPE html>
<html lang="hi">
<head>
    <title>सरकारी योजनाएं</title>
</head>
<body>
    <h2>सभी सरकारी योजनाएं</h2>
    <?php
    $result = $conn->query("SELECT * FROM yojna ORDER BY date DESC");
    while ($row = $result->fetch_assoc()) {
        echo "<p><a href='".$row['link']."'>".$row['title']."</a></p>";
    }
    ?>
</body>
</html>body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
}

header {
    background: #007bff;
    color: white;
    padding: 10px;
    text-align: center;
}

nav a {
    color: white;
    margin: 10px;
    text-decoration: none;
    font-weight: bold;
}

section {
    padding: 20px;
}

footer {
    text-align: center;
    background: #007bff;
    color: white;
    padding: 10px;
}<?php
$conn = new mysqli("localhost", "root", "", "yojna_website");
?>

<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>सरकारी योजना, नौकरी, रिजल्ट & न्यूज</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <header>
        <h1>सरकारी योजना, नौकरी, रिजल्ट & न्यूज</h1>
        <nav>
            <a href="index.php">होम</a>
            <a href="yojna.php">सरकारी योजना</a>
            <a href="jobs.php">सरकारी नौकरियां</a>
            <a href="results.php">रिजल्ट</a>
            <a href="news.php">न्यूज</a>
        </nav>
    </header>

    <section>
        <h2>लेटेस्ट सरकारी योजनाएं</h2>
        <?php
        $result = $conn->query("SELECT * FROM yojna ORDER BY date DESC LIMIT 5");
        while ($row = $result->fetch_assoc()) {
            echo "<p><a href='".$row['link']."'>".$row['title']."</a></p>";
        }
        ?>
    </section>

    <section>
        <h2>लेटेस्ट सरकारी नौकरियां</h2>
        <?php
        $result = $conn->query("SELECT * FROM jobs ORDER BY date DESC LIMIT 5");
        while ($row = $result->fetch_assoc()) {
            echo "<p><a href='".$row['apply_link']."'>".$row['title']."</a> (अंतिम तिथि: ".$row['last_date'].")</p>";
        }
        ?>
    </section>

    <footer>
        <p>&copy; 2025 सरकारी योजना पोर्टल</p>
    </footer>
</body>
</html>CREATE DATABASE yojna_website;

USE yojna_website;

CREATE TABLE yojna (
    id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(255),
    description TEXT,
    link VARCHAR(255),
    date TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE jobs (
    id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(255),
    description TEXT,
    last_date DATE,
    apply_link VARCHAR(255),
    date TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE results (
    id INT AUTO_INCREMENT PRIMARY KEY,
    exam_name VARCHAR(255),
    result_link VARCHAR(255),
    date TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE news (
    id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(255),
    content TEXT,
    date TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);# Sarkari---yojna---site
