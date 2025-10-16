# Prompts-Shortcuts

## 安装AutoHotkey v2.0

## 脚本 (.ahk)
创建一个本文命名为 **MyPrompts.ahk**，复制以下内容并保存：
```
#Requires AutoHotkey v2.0
#SingleInstance Force
SendMode "Input"

; -------------------------------
; 代码和理论
; -------------------------------

paper_explain := "
(
请介绍论文 {标题} ({link})，包括提出的重要理论、重要公式和算法，并解释；
直接给我一份可直接复制粘贴的markdown笔记代码块，要求代码块中所有公式使用$符号或者$$符号包围。
)"

theory_explain := "
(
请详细介绍 {某理论}，需要包括原理和相关公式；
直接给我一份可直接复制粘贴的markdown笔记代码块，要求代码块中所有公式使用$符号或者$$符号包围。
)"

code_add_function := "
(
请根据下面这段代码，添加一个功能，实现{Your Function}。请给出更新后的代码并给出合理的解释。
<CODE>
{Your Code}
</CODE>
)"

code_optimize := "
(
下面是一段我写的代码:
<CODE>
{Your Code}
</CODE>
请优化这段代码，使其变得更精简且具有较低的时间复杂度，并要给出完整清晰的英文注释。
)"

code_check := "
(
下面是一段我写的代码:
<CODE>
{Your Code}
</CODE>
请帮我检查代码是否有问题，若有问题请指出，并给我一个改进的版本。
)"

code_comment := "
(
下面是一段我写的代码:
<CODE>
{Your Code}
</CODE>
请在代码中添加完整和清晰的英文注释。
)"

prompts_cn := Map(
  "代码添加功能", code_add_function,
  "代码优化", code_optimize,
  "代码检查", code_check,
  "代码注释", code_comment,
  "概念解释", theory_explain,
  "论文介绍", paper_explain
)

promptMenuCN := Menu()
for name, text in prompts_cn
  promptMenuCN.Add(name, InsertPrompt.Bind(text))

^!':: promptMenuCN.Show()  ; Ctrl+Alt+' 触发中文菜单







; -------------------------------
; 英文写作
; -------------------------------

paper_improve := "
(
Below are paragraphs from an academic paper. Polish the writing to meet the academic style. Improve the spelling, grammar, clarity, concision and overall readability.
<PARAGRAPHS>
{Your Text}
</PARAGRAPHS>
)"


paper_improve_again := "
(
Please improve again.
)"


paper_rewrite := "
(
Please rewrite the following academic paragraph. Maintain the same technical meaning.
<PARAGRAPH>
{Your Text}
</PARAGRAPH>
)"


grammar_check := "
(
Below are paragraphs from an academic paper. Please improve them just to make sure the grammar and the spelling is correct. Do not try to polish the text. If no mistake is found, tell me that this paragraph is good.
<PARAGRAPHS>
{Your Text}
</PARAGRAPHS>
)"

translate_cn2en := "
(
Please translate the following Chinese paragraphs into natural and formal English suitable for academic writing.
<CHINESE>
{Your Text}
</CHINESE>
)"

translate_en2cn := "
(
Please translate the following English paragraphs into accurate and fluent Chinese.
<ENGLISH>
{Your Text}
</ENGLISH>
)"


academic_summary := "
(
Please summarize the following academic paragraph in one concise English sentence while preserving its main idea.
<PARAGRAPHS>
{Your Text}
</PARAGRAPHS>
)"

prompts_en := Map(
  "润色(精准)", paper_improve,
  "继续改进", paper_improve_again,
  "改写", paper_rewrite,
  "语法检查", grammar_check,
  "中译英", translate_cn2en,
  "英译中", translate_en2cn,
  "总结", academic_summary
)

promptMenuEN := Menu()
for name, text in prompts_en
  promptMenuEN.Add(name, InsertPrompt.Bind(text))

^!e:: promptMenuEN.Show()  ; Ctrl+Alt+E 打开英文学术写作菜单


; -------------------------------
; 通用函数
; -------------------------------
InsertPrompt(text, *) {
  ClipSaved := ClipboardAll()
  A_Clipboard := text
  ClipWait 0.5
  Send "^v"
  Sleep 50
  A_Clipboard := ClipSaved
}

```

保存后双击该文件载入AutoHotkey，便可键入 Ctrl+Alt+E 使用英文写作的Prompt, 或键入 Ctrl+Alt+' 使用代码编写的Prompt。


