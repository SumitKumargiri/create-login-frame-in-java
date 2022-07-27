# create-login-frame-in-java with mysql


package DataBaseExample;

import java.awt.*;
import javax.swing.*;
import java.awt.event.*;
import java.sql.*;

public class JDBC_Demo2 extends JFrame implements ActionListener {

    JLabel lb1, lb2, lb3;
    JTextField tf1;
    JPasswordField jp;
    JButton bt1, bt2;

    JDBC_Demo2() {
        setLayout(null);
        setLocationRelativeTo(null);
        setBackground(Color.RED);
        lb1 = new JLabel("Usename");
        lb2 = new JLabel("Password");
        //Icon icon = new ImageIcon("C:\\Users\\sumit\\OneDrive\\Pictures\\Saved Pictures");
        lb3 = new JLabel();
        lb3.setIcon(new ImageIcon("src/uploads/im3.png"));
        //lb3.setIcon(icon);

        tf1 = new JTextField();
        jp = new JPasswordField();
        bt1 = new JButton("Login");
        bt2 = new JButton("Singup");

        lb1.setBounds(100, 100, 100, 50);
        lb2.setBounds(100, 200, 100, 50);
        lb3.setBounds(500, 30, 800, 500);
        tf1.setBounds(180, 110, 250, 30);
        jp.setBounds(180, 210, 250, 30);

        bt1.setBounds(200, 300, 100, 30);
        bt2.setBounds(350, 300, 100, 30);

        add(lb1);
        add(lb2);
        add(lb3);
        add(tf1);
        add(jp);
        add(bt1);
        add(bt2);
        bt1.addActionListener(this);

        setSize(800, 600);
        setVisible(true);
        getContentPane().setBackground(Color.CYAN);
    }

    public static void main(String args[]) {
        JDBC_Demo2 obj = new JDBC_Demo2();
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        String Username = tf1.getText();
        String Password = jp.getText();
        if (Username.equals("") || Password.equals("")) {
            JOptionPane.showMessageDialog(rootPane, "All field are required");
        } else {
            try {
                Class.forName("com.mysql.jdbc.Driver");
                Connection conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/vmm", "root", "system");
                Statement stmt = conn.createStatement(ResultSet.TYPE_SCROLL_SENSITIVE, ResultSet.CONCUR_UPDATABLE);
                ResultSet rs = stmt.executeQuery("select *from user where username= '" + Username + "'and password='" + Password + "'");
                if (rs.next()) {
                    JOptionPane.showMessageDialog(rootPane, "Login Successfully");
                    home obj = new home();
                } else {
                    JOptionPane.showMessageDialog(rootPane, "Username and Password do not match");
                }
            } catch (Exception ex) {
                ex.printStackTrace();
            }
        }
    }
}

/* output:-![image](https://user-images.githubusercontent.com/96234273/181194307-e7f06350-0a24-4b51-b852-48d73bc5ed67.png)

*/
