import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
import java.util.*;

public class JungTestApp {
    private JFrame frame;
    private CardLayout cardLayout;
    private JPanel mainPanel;
    private int currentQuestionIndex = 0;
    private List<Question> questions;
    private Map<String, Integer> scores = new HashMap<>();

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> new JungTestApp().createAndShowGUI());
    }

    private void createAndShowGUI() {
        // 初始化变量
        initVariables();

        frame = new JFrame("荣格八维测试");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setSize(600, 400);

        cardLayout = new CardLayout();
        mainPanel = new JPanel(cardLayout);

        mainPanel.add(createCoverPage(), "Cover");
        mainPanel.add(createQuestionPanel(), "Questions");
        mainPanel.add(new JPanel(), "Result"); // 先占位

        frame.getContentPane().add(mainPanel);
        cardLayout.show(mainPanel, "Cover");
        frame.setVisible(true);
    }

    private void initVariables() {
        // 初始化变量得分
        String[] vars = {"Ne+", "Ne-", "Ni+", "Ni-", "Fe+", "Fe-", "Fi+", "Fi-", "Ti+", "Ti-", "Te+", "Te-", "Si+", "Si-", "Se+", "Se-"};
        for (String var : vars) {
            scores.put(var, 0);
        }

        // 添加题目
        questions = new ArrayList<>();
        questions.add(new Question("你相信很多行为、事情都可以分为符合标准、不符合标准的，而那些符合标准的是好的。", "Te+"));
        questions.add(new Question("你总是在追求公正客观的判断...", "Te+"));
        questions.add(new Question("你经常感知到一个物体在未来某个时刻的样子。", "Ni+"));
        questions.add(new Question("你产生的想象和你有着独一无二的联系...", "Ni+"));
        questions.add(new Question("当你有一个想法时，你想让它在现实中产生最大效益。", "Ni+"));
        questions.add(new Question("你的感受经常和别人不同...", "Si+"));
        questions.add(new Question("你总结出一个人的性格并发现他们的行为符合你的印象。", "Si+"));
        questions.add(new Question("如果一个人说了伤害你的话...", "Si-"));
        questions.add(new Question("当感官刺激足够强时，你会想沉浸其中。", "Se+"));
        questions.add(new Question("你总是在想我怎么做、别人怎么做可以让事情变得更好。", "Ne+"));
        questions.add(new Question("你不到不得已不做出确定的选择...", "Ne+"));
        questions.add(new Question("你喜欢听不同的方案和想法，并思考它们。", "Ne+"));
    }

    private JPanel createCoverPage() {
        JPanel panel = new JPanel(new BorderLayout());
        JLabel title = new JLabel("荣格八维测试", SwingConstants.CENTER);
        title.setFont(new Font("Serif", Font.BOLD, 28));
        JButton startBtn = new JButton("开始测试");
        startBtn.addActionListener(e -> cardLayout.show(mainPanel, "Questions"));

        panel.add(title, BorderLayout.CENTER);
        panel.add(startBtn, BorderLayout.SOUTH);
        return panel;
    }

    private JPanel createQuestionPanel() {
        JPanel panel = new JPanel(new BorderLayout());
        JPanel questionPanel = new JPanel();
        JLabel questionLabel = new JLabel();
        questionLabel.setFont(new Font("SansSerif", Font.PLAIN, 16));
        questionPanel.add(questionLabel);

        JPanel buttonPanel = new JPanel(new GridLayout(1, 5));
        String[] options = {"非常不同意", "不同意", "中立", "同意", "非常同意"};
        int[] values = {-5, -3, 0, 3, 5};
        for (int i = 0; i < 5; i++) {
            int scoreValue = values[i];
            JButton btn = new JButton(options[i]);
            btn.addActionListener(e -> {
                applyScore(scoreValue);
                currentQuestionIndex++;
                if (currentQuestionIndex < questions.size()) {
                    updateQuestion(questionLabel);
                } else {
                    showResultPage();
                }
            });
            buttonPanel.add(btn);
        }

        panel.add(questionPanel, BorderLayout.NORTH);
        panel.add(buttonPanel, BorderLayout.SOUTH);
        updateQuestion(questionLabel);

        return panel;
    }

    private void applyScore(int value) {
        String var = questions.get(currentQuestionIndex).variable;
        int current = scores.getOrDefault(var, 0);
        scores.put(var, current + value);
    }

    private void updateQuestion(JLabel label) {
        Question q = questions.get(currentQuestionIndex);
        label.setText("第 " + (currentQuestionIndex + 1) + " 题: " + q.text);
    }

    private void showResultPage() {
        JPanel resultPanel = new JPanel(new BorderLayout());
        JTextArea resultText = new JTextArea();
        resultText.setEditable(false);
        StringBuilder sb = new StringBuilder("测试结果:\n\n");

        // 显示得分
        scores.entrySet().stream()
                .sorted(Map.Entry.<String, Integer>comparingByValue().reversed())
                .forEach(entry -> sb.append(entry.getKey()).append(": ").append(entry.getValue()).append("\n"));

        // TODO: 进行类型计算和推理，并展示前5个可能类型

        resultText.setText(sb.toString());
        resultPanel.add(new JScrollPane(resultText), BorderLayout.CENTER);
        mainPanel.add(resultPanel, "Result");
        cardLayout.show(mainPanel, "Result");
    }

    static class Question {
        String text;
        String variable;

        public Question(String text, String variable) {
            this.text = text;
            this.variable = variable;
        }
    }
}
