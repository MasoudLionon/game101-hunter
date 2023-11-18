# game101-hunter
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.MouseAdapter;
import java.awt.event.MouseEvent;
import java.util.Random;

public class ShikarchiGame extends JFrame {

    private int score = 0;
    private JLabel scoreLabel;
    private JLabel shikarLabel;

    public ShikarchiGame() {
        setTitle("شکارچی بازی");
        setSize(400, 400);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        scoreLabel = new JLabel("امتیاز: 0");
        shikarLabel = new JLabel("شکارچی");

        shikarLabel.addMouseListener(new MouseAdapter() {
            @Override
            public void mouseClicked(MouseEvent e) {
                increaseScore();
                moveShikar();
            }
        });

        setLayout(new FlowLayout());
        add(scoreLabel);
        add(shikarLabel);

        Timer timer = new Timer(1000, new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                moveShikar();
            }
        });

        timer.start();
    }

    private void increaseScore() {
        score++;
        scoreLabel.setText("امتیاز: " + score);
    }

    private void moveShikar() {
        Random rand = new Random();
        int x = rand.nextInt(getWidth() - shikarLabel.getWidth());
        int y = rand.nextInt(getHeight() - shikarLabel.getHeight());
        shikarLabel.setLocation(x, y);
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(new Runnable() {
            @Override
            public void run() {
                new ShikarchiGame().setVisible(true);
            }
        });
    }
}
