# BMI
name , weight , height and age<?php
// Initialize result variable
$result = "";

// Check if the form is submitted
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    // Get the values from the form
    $name = $_POST['name'];
    $height = $_POST['height'];
    $weight = $_POST['weight'];
    $age = $_POST['age']; // Get the age input

    // Check if any required field is empty
    if ($name === "" || $height === "" || $weight === "" || $age === "") {
        $result = "Please fill in all the information.";
    } else {
        // Convert height and weight to floats (to handle both integers and decimals)
        $height = (float) $height;
        $weight = (float) $weight;
        $age = (int) $age; // Convert age to integer

        // Validate the height, weight, and age
        if ($height <= 0 || $weight <= 0 || $age <= 0) {
            $result = "ERROR: Invalid (negative or zero) values for height, weight, or age.";
        } elseif ($weight > 70) {
            $result = "ERROR: Weight cannot be greater than 70.";
        } else {
            // Display the information if all inputs are valid
            $result = "Hello, Mr. $name, your height is: $height meters, your weight is: $weight kg, and your age is: $age years.";
        }
    }
}
?>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Find Name, Height, Weight, and Age</title>
</head>
<body>
    <h1>Enter Your Information:</h1>
    
    <!-- Form to take user input -->
    <form method="POST">
        <label for="name">Enter your name:</label>
        <input type="text" name="name" required>
        <br><br>
        
        <label for="height">Enter your height (in meters):</label>
        <input type="number" step="any" name="height" required>
        <br><br>

        <label for="weight">Enter your weight (in kg):</label>
        <input type="number" step="any" name="weight" required>
        <br><br>

        <label for="age">Enter your age (in years):</label>
        <input type="number" name="age" required>
        <br><br>

        <input type="submit" value="Submit">
    </form>

    <!-- Display the result if the form was submitted -->
    <p><?php echo $result; ?></p>
</body>
</html>
