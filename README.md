<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Multipurpose Calculator</title>
</head>
<body>
    <h2>Multipurpose Calculator</h2>
    
    <!-- Form to input numbers and select operation -->
    <form method="post" action="">
        <label for="num1">First Number:</label>
        <input type="number" name="num1" id="num1" required><br><br>

        <label for="num2">Second Number (if applicable):</label>
        <input type="number" name="num2" id="num2"><br><br>

        <label for="operation">Choose Operation:</label>
        <select name="operation" id="operation">
            <option value="add">Addition (+)</option>
            <option value="subtract">Subtraction (-)</option>
            <option value="multiply">Multiplication (*)</option>
            <option value="divide">Division (/)</option>
            <option value="exponent">Exponentiation (^)</option>
            <option value="percentage">Percentage (%)</option>
            <option value="sqrt">Square Root</option>
            <option value="logarithm">Logarithm (log)</option>
        </select><br><br>

        <button type="submit" name="submit">Calculate</button>
    </form>

    <?php
    // Handle form submission
    if (isset($_POST['submit'])) {
        $num1 = $_POST['num1'];
        $num2 = isset($_POST['num2']) ? $_POST['num2'] : null; // Second number (optional)
        $operation = $_POST['operation'];

        // Function to perform the selected calculation
        function calculate($num1, $num2, $operation) {
            switch($operation) {
                case 'add':
                    return $num1 + $num2;
                case 'subtract':
                    return $num1 - $num2;
                case 'multiply':
                    return $num1 * $num2;
                case 'divide':
                    return $num2 != 0 ? $num1 / $num2 : 'Error: Division by zero';
                case 'exponent':
                    return pow($num1, $num2);
                case 'percentage':
                    return ($num1 / 100) * $num2;
                case 'sqrt':
                    return sqrt($num1);
                case 'logarithm':
                    return log($num1);
                default:
                    return "Invalid Operation";
            }
        }

        // Perform calculation based on user input
        if (($operation == 'sqrt' || $operation == 'logarithm') && !empty($num1)) {
            $result = calculate($num1, null, $operation);
        } else if (!empty($num1) && !empty($num2)) {
            $result = calculate($num1, $num2, $operation);
        } else {
            $result = "Please enter valid numbers.";
        }

        // Display the result
        echo "<h3>Result: $result</h3>";
    }
    ?>
</body>
</html>
