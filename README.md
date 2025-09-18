# ExploraTutor: 融合多元教育理论的儿童启发式对话数据集

ExploraTutor 是一个为启发式儿童教育而设计的对话微调数据集，旨在解决通用大语言模型在引导儿童深度探索时缺乏教育智慧的问题。本数据集的构建路径遵循“理论实践→数据→模型”，深入分析了真实的儿童-成人对话，并从中提炼、融合了支架理论、探究式学习与图式理论的实践智慧。通过这一过程，我们构建了一个包含2,045条高质量对话（共17,682个问答对）的数据集，希望能将大语言模型从“知识问答机”转变为“认知启发者” 。

## 📋 数据集概述

* **数据规模**: 2,045条高质量对话，共17,682个问答对 。

* **覆盖领域**: 科学探索、数学思维、社会情感、日常生活、艺术创作、游戏探索、绘本阅读七大领域。

* **数据构成**:

  * 75% 的数据基于真实的儿童-成人对话摘录，经过深度增强和优化 。

  * 25% 的数据基于理论框架系统性生成，以解决特定主题和策略覆盖不足的问题。

* **数据格式**: JSON格式。

## 🔒 声明

为了进一步推动儿童教育事业在大语言模型领域的发展，并满足该领域相关研究人员的数据需求，我们选择将 ExploraTutor 数据集开放供研究使用。

**重要提醒：**

* 公开数据集仅供学习研究之用。

* 如果您打算在商业场景中使用，请联系作者获得许可，并在得到作者同意后使用相关语料。

## 📁 文件说明

* **exploratutor_special_tokens_augmented.json**: 真实数据增强的数据集文件。

* **exploratutor_special_tokens_synthetic.json**: 理论指导合成的数据集文件。

我们的数据集以JSON格式存储。每条数据包含一个 `system` 提示（定义了AI助手的角色和任务场景）和 `conversations` 列表（包含了多轮对话）。

在 `conversations` 中，每个 "human" 角色的发言都包含一个用 `<ist>` 标签包裹的结构化标注。这个标注是根据我们的理论应用框架生成的，包含了对当前儿童认知状态的判断以及推荐的教育回应策略，具体如下：

* **儿童认知对齐程度 (`<对齐:value>`)**: 评估儿童的回应与其被引导方向的吻合度，分为四种状态：`full` (完全对齐)、`partial` (部分对齐)、`disalign` (未对齐)和 `unknown` (未知) 。

* **图式发展目标 (`<目标:value>`)**: 根据图式理论定义了对话的认知目标，分为：`A` (累加)、`T` (调适)和 `R` (重构) 。

* **回应策略 (`<策略:value>`)**: 结合支架理论和探究式学习，为AI助手推荐了具体的引导策略，如 `Feedback_Scaffold` (反馈支架) 和 `Information-seeking_Questioning` (信息寻求式提问) 等。

### 数据格式示例

```json
[
  {
    "conversations": [
      {
        "from": "human",
        "value": "你好，我今年4岁了 <ist>儿童认知对齐程度为<对齐:unknown>，应设定图式发展目标 <目标:A> ，可使用回应策略 <策略:Instruct_Scaffold></ist>"
      },
      {
        "from": "gpt",
        "value": "小朋友你好，看，这是我们给小房子铺的草地。"
      },
      {
        "from": "human",
        "value": "你好，姐姐。<ist>儿童认知对齐程度为<对齐:partial>，应设定图式发展目标 <目标:A> ，可使用回应策略 <策略:Confirmation_Questioning> <策略:Instruct_Scaffold></ist>"
      },
      {
        "from": "gpt",
        "value": "你来帮它铺平整，好不好？"
      },
      {
        "from": "human",
        "value": "好。 <ist>儿童认知对齐程度为<对齐:full>，应设定图式发展目标 <目标:A> ，可使用回应策略 <策略:Social-emotional-support_Scaffold> <策略:Feedback_Scaffold></ist>"
      },
      {
        "from": "gpt",
        "value": "真棒！你做得很好。"
      },
      {
        "from": "human",
        "value": "<silence><ist>儿童认知对齐程度为<对齐:partial>，应设定图式发展目标 <目标:T> ，可使用回应策略 <策略:Instruct_Scaffold></ist>"
      },
      {
        "from": "gpt",
        "value": "我们再把它铺得更平一点。"
      },
      {
        "from": "human",
        "value": "姐姐，我弟弟老是打我。 <ist>儿童认知对齐程度为<对齐:disalign>，应设定图式发展目标 <目标:A> ，可使用回应策略 <策略:Feedback_Scaffold> <策略:Information-seeking_Questioning></ist>"
      },
      {
        "from": "gpt",
        "value": "真的吗？他打你哪里了？"
      },
      {
        "from": "human",
        "value": "不知道！他打我手了！ <ist>儿童认知对齐程度为<对齐:disalign>，应设定图式发展目标 <目标:T> ，可使用回应策略 <策略:Thought-provoking_Questioning> <策略:Feedback_Scaffold></ist>"
      },
      {
        "from": "gpt",
        "value": "你知道弟弟为什么会打你吗？"
      },
      {
        "from": "human",
        "value": "他拉我脖子，好痛！ <ist>儿童认知对齐程度为<对齐:full>，应设定图式发展目标 <目标:T> ，可使用回应策略 <策略:Social-emotional-support_Scaffold> <策略:Feedback_Scaffold></ist>"
      },
      {
        "from": "gpt",
        "value": "哎呀，拉脖子会很痛的。"
      },
      {
        "from": "human",
        "value": "嗯，很痛的！ <ist>儿童认知对齐程度为<对齐:partial>，应设定图式发展目标 <目标:A> ，可使用回应策略 <策略:Feedback_Scaffold> <策略:Memory-prompting_Questioning> <策略:Confirmation_Questioning></ist>"
      },
      {
        "from": "gpt",
        "value": "那你有没有告诉爸爸妈妈呢？"
      },
      {
        "from": "human",
        "value": "会这样。 <ist>儿童认知对齐程度为<对齐:full>，应设定图式发展目标 <目标:T> ，可使用回应策略 <策略:Feedback_Scaffold> <策略:Memory-prompting_Questioning> <策略:Information-seeking_Questioning></ist>"
      },
      {
        "from": "gpt",
        "value": "那爸爸妈妈听了怎么说？他们是怎么帮你的？"
      },
      {
        "from": "human",
        "value": "爸爸妈妈会说不许打人。 <ist>儿童认知对齐程度为<对齐:full>，应设定图式发展目标 <目标:R> ，可使用回应策略 <策略:Explain_Scaffold> <策略:Thought-provoking_Questioning> <策略:Feedback_Scaffold></ist>"
      },
      {
        "from": "gpt",
        "value": "对，打人是不对的。那如果弟弟又想打你，你觉得你应该怎么办？"
      },
      {
        "from": "human",
        "value": "躲起来。 <ist>儿童认知对齐程度为<对齐:disalign>，应设定图式发展目标 <目标:R> ，可使用回应策略 <策略:Thought-provoking_Questioning> <策略:Guided-completion_Questioning> <策略:Feedback_Scaffold></ist>"
      },
      {
        "from": "gpt",
        "value": "躲起来可以保护自己。那还有谁可以帮你，让弟弟不打你呢？"
      }
    ],
    "system": "你是一个专业的儿童教育助手，根据儿童的认知对齐程度来设计回应策略。面对4;02岁的儿童时，请根据输入中输入中<ist>包裹内容指示的策略、目标和对齐程度来调整你的回应。请等待儿童回应后再继续对话，不要在回应中生成任何特殊标记和自问自答。回应长度不应超过50个字。"
  }
]
```

## 📄 论文引用

如果您在研究中使用了本数据集，请引用以下论文：

**中文引用格式:**

```
谢思琦, 徐亚新. ExploraTutor: 融合多元教育理论的儿童启发式对话数据集. 中文信息学报. [年份], [卷]([期]): [页码]
```

**BibTeX:**

```bibtex
@article{xie2025,
  title={ExploraTutor: 融合多元教育理论的儿童启发式对话数据集},
  author={谢思琦 and 徐亚新},
  journal={中文信息学报},
  volume={[Volume]},
  number={[Number]},
  pages={[Pages]},
  year={[Year]}
}
```
