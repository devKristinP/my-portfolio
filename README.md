# my-portfolio

I am using a template for my first portfolio project.
I will also be working on making one from scratch.

kindness Photo by Brett Jordan: https://www.pexels.com/photo/laid-out-scrabble-tiles-8818464/

I want to link the contact form to my email
researching brought me to instructions for a php file.
Pasting here so I can access it later.

see below

        Generate the PHP code to capture form data
        So the PHP file enables you to capture data (name, email, message and any other input type you’ve included). It then delivers it straight to your email address as a plain text message.

        Below we’ve included PHP code that, in technical terms, validates user inputs on the server-side. To translate that from gobbledygook: it makes sure everything works. It also generates any error and confirmation messages that users may get when they fill out your form.

        Copy and paste the below code into the .php file. All you need to do is add your own email, subject line and success message (they're outlined within the code).

<?php
if (isset($_POST['Email'])) {

    // EDIT THE FOLLOWING TWO LINES:
    $email_to = "devKristinP@gmail.com";
    $email_subject = "devKristinP New form submissions";

    function problem($error)
    {
        echo "We're sorry, but there were error(s) found with the form you submitted. ";
        echo "These errors appear below.<br><br>";
        echo $error . "<br><br>";
        echo "Please go back and fix these errors.<br><br>";
        die();
    }

    // validation expected data exists
    if (
        !isset($_POST['Name']) ||
        !isset($_POST['Email']) ||
        !isset($_POST['Message'])
    ) {
        problem('We're sorry, but there appears to be a problem with the form you submitted.');
    }

    $name = $_POST['Name']; // required
    $email = $_POST['Email']; // required
    $message = $_POST['Message']; // required

    $error_message = "";
    $email_exp = '/^[A-Za-z0-9._%-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,4}$/';

    if (!preg_match($email_exp, $email)) {
        $error_message .= 'The Email address you entered does not appear to be valid.<br>';
    }

    $string_exp = "/^[A-Za-z .'-]+$/";

    if (!preg_match($string_exp, $name)) {
        $error_message .= 'The Name you entered does not appear to be valid.<br>';
    }

    if (strlen($message) < 2) {
        $error_message .= 'The Message you entered do not appear to be valid.<br>';
    }

    if (strlen($error_message) > 0) {
        problem($error_message);
    }

    $email_message = "Form details below.\n\n";

    function clean_string($string)
    {
        $bad = array("content-type", "bcc:", "to:", "cc:", "href");
        return str_replace($bad, "", $string);
    }

    $email_message .= "Name: " . clean_string($name) . "\n";
    $email_message .= "Email: " . clean_string($email) . "\n";
    $email_message .= "Message: " . clean_string($message) . "\n";

    // create email headers
    $headers = 'From: ' . $email . "\r\n" .
        'Reply-To: ' . $email . "\r\n" .
        'X-Mailer: PHP/' . phpversion();
    @mail($email_to, $email_subject, $email_message, $headers);
?>

    <!-- INCLUDE YOUR SUCCESS MESSAGE BELOW -->

    Thanks for getting in touch. Kristin will get back to you soon.

<?php
}
?>

// to be linked with this html code (but I want to use the existing form and add a submit button

<!DOCTYPE html>
<head>
    <title>Contact Form</title>
</head>
<body>
    <h3>Contact us</h3>
    <form id="fcf-form-id" class="fcf-form-class" method="post" action="contact-form-process.php">
            <label for="Name" class="fcf-label">Your name</label>
            <div class="fcf-input-group">
                <input type="text" id="Name" name="Name" class="fcf-form-control" required>
            </div>
        <div class="fcf-form-group">
            <label for="Email" class="fcf-label">Your email address</label>
            <div class="fcf-input-group">
                <input type="email" id="Email" name="Email" class="fcf-form-control" required>
            </div>
        <div class="fcf-form-group">
            <label for="Message" class="fcf-label">Your message</label>
            <div class="fcf-input-group">
                <textarea id="Message" name="Message" class="fcf-form-control" rows="6" maxlength="3000" required></textarea>
            </div>
        </div>
        <div class="fcf-form-group">
            <button type="submit" id="fcf-button" class="fcf-btn fcf-btn-primary fcf-btn-lg fcf-btn-block">Send</button>
        </div>
</body>
</html>)
