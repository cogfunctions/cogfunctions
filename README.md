// Question.java
package com.jasmine.cogfunctions.model;

public class Question {
    private int id;
    private String text;
    private String variable;

    public Question() {}

    public Question(int id, String text, String variable) {
        this.id = id;
        this.text = text;
        this.variable = variable;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getText() {
        return text;
    }

    public void setText(String text) {
        this.text = text;
    }

    public String getVariable() {
        return variable;
    }

    public void setVariable(String variable) {
        this.variable = variable;
    }
}

// questions.json（放在 resources 目录下）
[
  { "id": 1, "text": "你相信很多行为、事情都可以分为符合标准、不符合标准的，而那些符合标准的是好的。", "variable": "Te+" },
  { "id": 2, "text": "你总是在追求公正客观的判断。比如你不在乎一个人偷东西是否迫不得已，他事实上就是做错了。", "variable": "Te+" },
  { "id": 3, "text": "你经常感知到一个物体、一件事在未来某个时刻的样子。", "variable": "Ni+" },
  { "id": 4, "text": "你产生的想象和你有着独一无二的联系，你的经历和自身导致你产生这些想象，这些想象也是你自身的重要组成部分。", "variable": "Ni+" },
  { "id": 5, "text": "当你有一个想法时，你想让它在现实中产生最大效益。", "variable": "Ni+" },
  { "id": 6, "text": "你的感受经常和别人的不同。比如有时别人觉得B在阴阳你但你不这么觉得，你觉得A在讨好你时别人又不这么觉得。", "variable": "Si+" },
  { "id": 7, "text": "你总结出一个人的性格（比如甜美的、帅气的、温柔的）并发现他们的行为大部分时候符合你的印象。", "variable": "Si+" },
  { "id": 8, "text": "如果一个人说了伤害你的话，你受伤害的感受会随着不断感受它而加深，你意识到这种感受在蒙蔽你并想摆脱，但你总忍不住去想它和它相关的事。", "variable": "Si-" },
  { "id": 9, "text": "当感官刺激足够强时，你会想沉浸其中，不去思考你为什么会有这样的感受、这样的感受好不好、有什么意义和影响。", "variable": "Se+" },
  { "id": 10, "text": "你总是在想我怎么做、别人怎么做可以让事情变得更好。", "variable": "Ne+" },
  { "id": 11, "text": "你不到不得已不做出确定的选择，这不是因为选择困难症，而是你觉得前面总有更好的选择等着你。", "variable": "Ne+" },
  { "id": 12, "text": "你喜欢听不同的方案和想法，并思考他们是否合理或他们的可行性。", "variable": "Ne+" }
]



