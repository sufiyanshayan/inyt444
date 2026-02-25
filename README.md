<?php
// ডাটাবেজ কানেকশন (উপরের মতোই)
session_start(); // সিম্পল পাসওয়ার্ড প্রটেকশনের জন্য

// খুব সিম্পল অ্যাডমিন পাসওয়ার্ড (উন্নতির জন্য বদলে নিন)
$admin_pass = "admin123"; // আপনার পছন্দের পাসওয়ার্ড দিন

// লগইন চেক
if (!isset($_SESSION['admin_logged']) && $_POST['pass'] ?? '' !== $admin_pass) {
    // লগইন ফর্ম দেখান
    echo '<form method="post"><input type="password" name="pass" placeholder="পাসওয়ার্ড দিন"><button type="submit">লগইন</button></form>';
    exit();
} else {
    $_SESSION['admin_logged'] = true;
}

$message = '';

// ফর্ম সাবমিট করা হলে
if ($_SERVER['REQUEST_METHOD'] === 'POST' && isset($_POST['new_url'])) {
    $new_url = filter_var($_POST['new_url'], FILTER_SANITIZE_URL);
    
    // ডাটাবেজ আপডেট করুন
    try {
        // আপনার ডাটাবেজ কানেকশন কোড এখানে বসান
        $pdo = new PDO("mysql:host=localhost;dbname=your_db;charset=utf8", "user", "pass");
        $stmt = $pdo->prepare("UPDATE redirects SET target_url = ? WHERE id = 1");
        if ($stmt->execute([$new_url])) {
            $message = "URL সফলভাবে আপডেট হয়েছে!";
        } else {
            $message = "আপডেট ব্যর্থ হয়েছে।";
        }
    } catch (Exception $e) {
        $message = "Error: " . $e->getMessage();
    }
}

// বর্তমান URL দেখানোর জন্য পড়ুন
$current_url = '';
try {
    $pdo = new PDO("mysql:host=localhost;dbname=your_db;charset=utf8", "user", "pass");
    $stmt = $pdo->query("SELECT target_url FROM redirects WHERE id = 1");
    $result = $stmt->fetch(PDO::FETCH_ASSOC);
    $current_url = $result['target_url'] ?? '';
} catch (Exception $e) {
    // Error handling
}
?>

<!DOCTYPE html>
<html>
<head>
    <title>Redirect Admin</title>
</head>
<body>
    <h1>Redirect URL ম্যানেজার</h1>
    <?php if ($message): ?>
        <p style="color:green;"><?php echo $message; ?></p>
    <?php endif; ?>
    <form method="post">
        <label>বর্তমান URL: </label><br>
        <input type="url" name="new_url" value="<?php echo htmlspecialchars($current_url); ?>" size="50" required>
        <button type="submit">আপডেট করুন</button>
    </form>
    <p><a href="index