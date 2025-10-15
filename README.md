<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>User Authentication System</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #6a11cb 0%, #2575fc 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }
        
        .container {
            width: 100%;
            max-width: 400px;
            background-color: white;
            border-radius: 10px;
            box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2);
            overflow: hidden;
        }
        
        .form-container {
            padding: 30px;
        }
        
        h2 {
            text-align: center;
            margin-bottom: 20px;
            color: #333;
        }
        
        .form-group {
            margin-bottom: 20px;
        }
        
        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 500;
            color: #555;
        }
        
        input {
            width: 100%;
            padding: 12px 15px;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 16px;
            transition: border 0.3s;
        }
        
        input:focus {
            border-color: #2575fc;
            outline: none;
        }
        
        button {
            width: 100%;
            padding: 12px;
            background: linear-gradient(to right, #6a11cb, #2575fc);
            color: white;
            border: none;
            border-radius: 5px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            transition: opacity 0.3s;
        }
        
        button:hover {
            opacity: 0.9;
        }
        
        .toggle-form {
            text-align: center;
            margin-top: 20px;
            color: #666;
        }
        
        .toggle-form a {
            color: #2575fc;
            text-decoration: none;
            font-weight: 500;
            cursor: pointer;
        }
        
        .toggle-form a:hover {
            text-decoration: underline;
        }
        
        .message {
            padding: 10px;
            margin-bottom: 20px;
            border-radius: 5px;
            text-align: center;
            display: none;
        }
        
        .success {
            background-color: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }
        
        .error {
            background-color: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }
        
        .password-container {
            position: relative;
        }
        
        .toggle-password {
            position: absolute;
            right: 10px;
            top: 50%;
            transform: translateY(-50%);
            background: none;
            border: none;
            color: #666;
            cursor: pointer;
            width: auto;
            padding: 0;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="form-container">
            <!-- Login Form -->
            <div id="login-form">
                <h2>Login to Your Account</h2>
                <div id="login-message" class="message"></div>
                <form id="loginForm">
                    <div class="form-group">
                        <label for="login-email">Email</label>
                        <input type="email" id="login-email" placeholder="Enter your email" required>
                    </div>
                    <div class="form-group">
                        <label for="login-password">Password</label>
                        <div class="password-container">
                            <input type="password" id="login-password" placeholder="Enter your password" required>
                            <button type="button" class="toggle-password" onclick="togglePassword('login-password')">Show</button>
                        </div>
                    </div>
                    <button type="submit">Login</button>
                </form>
                <div class="toggle-form">
                    Don't have an account? <a onclick="showSignup()">Sign Up</a>
                </div>
            </div>
            
            <!-- Signup Form -->
            <div id="signup-form" style="display: none;">
                <h2>Create New Account</h2>
                <div id="signup-message" class="message"></div>
                <form id="signupForm">
                    <div class="form-group">
                        <label for="signup-name">Full Name</label>
                        <input type="text" id="signup-name" placeholder="Enter your full name" required>
                    </div>
                    <div class="form-group">
                        <label for="signup-email">Email</label>
                        <input type="email" id="signup-email" placeholder="Enter your email" required>
                    </div>
                    <div class="form-group">
                        <label for="signup-password">Password</label>
                        <div class="password-container">
                            <input type="password" id="signup-password" placeholder="Create a password" required>
                            <button type="button" class="toggle-password" onclick="togglePassword('signup-password')">Show</button>
                        </div>
                    </div>
                    <div class="form-group">
                        <label for="signup-confirm-password">Confirm Password</label>
                        <div class="password-container">
                            <input type="password" id="signup-confirm-password" placeholder="Confirm your password" required>
                            <button type="button" class="toggle-password" onclick="togglePassword('signup-confirm-password')">Show</button>
                        </div>
                    </div>
                    <button type="submit">Sign Up</button>
                </form>
                <div class="toggle-form">
                    Already have an account? <a onclick="showLogin()">Login</a>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Toggle between login and signup forms
        function showSignup() {
            document.getElementById('login-form').style.display = 'none';
            document.getElementById('signup-form').style.display = 'block';
            clearMessages();
        }
        
        function showLogin() {
            document.getElementById('signup-form').style.display = 'none';
            document.getElementById('login-form').style.display = 'block';
            clearMessages();
        }
        
        // Clear all messages
        function clearMessages() {
            document.getElementById('login-message').style.display = 'none';
            document.getElementById('signup-message').style.display = 'none';
        }
        
        // Toggle password visibility
        function togglePassword(inputId) {
            const passwordInput = document.getElementById(inputId);
            const toggleButton = passwordInput.nextElementSibling;
            
            if (passwordInput.type === 'password') {
                passwordInput.type = 'text';
                toggleButton.textContent = 'Hide';
            } else {
                passwordInput.type = 'password';
                toggleButton.textContent = 'Show';
            }
        }
        
        // Display message
        function showMessage(elementId, message, type) {
            const messageElement = document.getElementById(elementId);
            messageElement.textContent = message;
            messageElement.className = 'message ' + type;
            messageElement.style.display = 'block';
        }
        
        // Handle login form submission
        document.getElementById('loginForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const email = document.getElementById('login-email').value;
            const password = document.getElementById('login-password').value;
            
            // Simple validation
            if (!email || !password) {
                showMessage('login-message', 'Please fill in all fields', 'error');
                return;
            }
            
            // In a real application, you would send this data to a server
            // For demo purposes, we'll just show a success message
            showMessage('login-message', 'Login successful!', 'success');
            
            // Clear form
            document.getElementById('loginForm').reset();
        });
        
        // Handle signup form submission
        document.getElementById('signupForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const name = document.getElementById('signup-name').value;
            const email = document.getElementById('signup-email').value;
            const password = document.getElementById('signup-password').value;
            const confirmPassword = document.getElementById('signup-confirm-password').value;
            
            // Simple validation
            if (!name || !email || !password || !confirmPassword) {
                showMessage('signup-message', 'Please fill in all fields', 'error');
                return;
            }
            
            if (password !== confirmPassword) {
                showMessage('signup-message', 'Passwords do not match', 'error');
                return;
            }
            
            if (password.length < 6) {
                showMessage('signup-message', 'Password must be at least 6 characters', 'error');
                return;
            }
            
            // In a real application, you would send this data to a server
            // For demo purposes, we'll just show a success message
            showMessage('signup-message', 'Account created successfully!', 'success');
            
            // Clear form
            document.getElementById('signupForm').reset();
            
            // Switch to login form after a delay
            setTimeout(() => {
                showLogin();
                showMessage('login-message', 'Account created! Please login.', 'success');
            }, 2000);
        });
    </script>
</body>
</html>
