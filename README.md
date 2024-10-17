# FeedbackCollection_javaproject
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class FeedbackCollectionSystem {
    public static void main(String[] args) {
        new LoginScreen();
    }
}

class LoginScreen extends JFrame {
    private JTextField usernameField, emailField;
    private JPasswordField passwordField, repeatPasswordField;

    public LoginScreen() {
        // Frame setup
        setTitle("CUSTOMER FEEDBACK COLLECTION SURVEY");
        setSize(400, 350);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLocationRelativeTo(null);

        // Panel to hold components
        JPanel panel = new JPanel();
        panel.setLayout(new GridLayout(6, 2, 10, 10));
        panel.setBackground(new Color(173, 216, 230));

        // Username input
        panel.add(new JLabel("Username: "));
        usernameField = new JTextField(20);
        panel.add(usernameField);

        // Password input
        panel.add(new JLabel("Password: "));
        passwordField = new JPasswordField(20);
        panel.add(passwordField);

        // Repeat password input
        panel.add(new JLabel("Repeat Password: "));
        repeatPasswordField = new JPasswordField(20);
        panel.add(repeatPasswordField);

        // Email input
        panel.add(new JLabel("Email: "));
        emailField = new JTextField(20);
        panel.add(emailField);

        // Buttons
        JButton loginButton = new JButton("Login");
        loginButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                openSurveyForm();
            }
        });
        panel.add(loginButton);

        JButton signUpButton = new JButton("Sign Up");
        signUpButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                JOptionPane.showMessageDialog(null, "Sign Up Completed!");
            }
        });
        panel.add(signUpButton);

        // Add panel to frame
        add(panel);

        setVisible(true);
    }

    private void openSurveyForm() {
        new SurveyForm(usernameField.getText());
        this.dispose(); // Close the login screen
    }
}

class SurveyForm extends JFrame {
    private String[] ratings = { "1", "2", "3" };

    public SurveyForm(String username) {
        // Frame setup
        setTitle("CUSTOMER FEEDBACK COLLECTION SURVEY");
        setSize(600, 700);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLocationRelativeTo(null);

        // Panel to hold components
        JPanel panel = new JPanel();
        panel.setLayout(new GridLayout(17, 2, 10, 10));
        panel.setBackground(new Color(224, 255, 255));

        // Welcome message
        panel.add(new JLabel("Please rate us for our service, " + username + "."));
        panel.add(new JLabel());

        // Questions
        addQuestion(panel, "1. How satisfied are you with our product?");
        addQuestion(panel, "2. How likely are you to recommend our product?");
        addQuestion(panel, "3. How would you rate the quality of your product?");
        addQuestion(panel, "4. Did our product meet your expectations?");
        addQuestion(panel, "5. How would you rate the quality of the customer service?");
        addQuestion(panel, "6. How easy was it to navigate to our website/app?");
        addQuestion(panel, "7. Are there any features you find particularly useful?");
        addQuestion(panel, "8. How would you rate the value for money of our product?");
        addQuestion(panel, "9. How smooth was the processing process?");
        addQuestion(panel, "10. Was the product delivered on time?");

        // Overall rating
        panel.add(new JLabel("Overall rating of our service:"));
        panel.add(createRatingDropdown());

        // Submit button
        JButton submitButton = new JButton("Submit");
        submitButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                JOptionPane.showMessageDialog(null, "Thank you for your feedback!");
                new LoginScreen(); // Redirect to login screen
                dispose(); // Close survey form
            }
        });
        panel.add(submitButton);

        // Add panel to frame
        add(panel);

        setVisible(true);
    }

    private void addQuestion(JPanel panel, String question) {
        panel.add(new JLabel(question));
        panel.add(createRatingDropdown());
    }

    private JComboBox<String> createRatingDropdown() {
        return new JComboBox<>(ratings);
    }
}
