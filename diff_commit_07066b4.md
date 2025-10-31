commit 07066b4a07021504eaf0f52b93acfb38308ac14f
Author: Yuzhi Wang <justin.w.xd@gmail.com>
Date:   Thu Sep 11 12:02:06 2025 +0800

    update tech report

diff --git a/tech_report.pdf b/tech_report.pdf
index 85f5333..fe838fa 100644
--- a/tech_report.pdf
+++ b/tech_report.pdf
@@ -964,7 +964,8 @@ fully decouple the training engine and the inference engine, significantly simpl
 
 Notably, this approach outperforms the transfer-what-you-need method due to reduced synchronization overhead and
 higher network bandwidth utilization. Our system can complete a full parameter update for Kimi K2 with less than 30
-seconds, a negligible duration for a typical RL training iteration.
+seconds, a negligible duration for a typical RL training iteration. The source code for the checkpoint engine is availible
+on Github4.
 
 3.3.3 Efficient System Startup
 
@@ -987,12 +988,13 @@ Our RL infrastructure supports the training of long-horizon, multi-turn agentic
 distinct challenges, such as complex environmental interactions and prolonged rollout durations. Here we introduce a
 few optimizations to alleviate these issues.
 
-Due to the diversity of environments, certain interactions may be blocked on waiting for environment feedback (e.g., a
-virtual machine or a code interpreter), leaving the GPUs idle. We employ two strategies to maximize GPU utilization:
+    4https://github.com/MoonshotAI/checkpoint-engine
 
                                                                      14
 Kimi K2  TECHNICAL REPORT
 
+Due to the diversity of environments, certain interactions may be blocked on waiting for environment feedback (e.g., a
+virtual machine or a code interpreter), leaving the GPUs idle. We employ two strategies to maximize GPU utilization:
 (i) we deploy heavy environments as dedicated services that can scale up more easily; (ii) we employ a large number of
 concurrent rollouts to amortize the latency induced by certain expensive interactions.
 
@@ -1019,7 +1021,7 @@ Multi-SWE-bench [86], SWE-Lancer [50], PaperBench [65], and Aider-Polyglot [17].
 performance on ¤ä 2-Bench [3] and AceBench [7], which emphasize multi-turn tool-calling capabilities. In reasoning,
 we include a wide range of mathematical, science and logical tasks: AIME 2024/2025, MATH-500, HMMT 2025,
 CNMO 2024, PolyMath-en, ZebraLogic [44], AutoLogi [91], GPQA-Diamond [61], SuperGPQA [14], and HumanityÔÇÖs
-Last Exam (Text-Only) [56]. We benchmark the long-context capabilities on: MRCR4 for long-context retrieval, and
+Last Exam (Text-Only) [56]. We benchmark the long-context capabilities on: MRCR5 for long-context retrieval, and
 DROP [15], FRAMES [38] and LongBench v2 [2] for long-context reasoning. For factuality, we evaluate FACTS
 Grounding [31], the Vectara Hallucination Leaderboard [73], and FaithJudge [68]. Finally, general capabilities are
 assessed using MMLU [24], MMLU-Redux [18], MMLU-Pro [76], IFEval [90], Multi-Challenge [64], SimpleQA [78],
@@ -1051,7 +1053,7 @@ SWE-bench Multilingual (47.3%), and SWE-lancer (39.1%), significantly closing th
 Sonnet. On competitive coding benchmarks (e.g., LiveCodeBench v6 53.7%, OJBench 27.1%), it also leads among all
 models, highlighting its practical coding proficiency across difficulty levels.
 
-    4https://huggingface.co/datasets/openai/mrcr
+    5https://huggingface.co/datasets/openai/mrcr
 
                                                                      15
                                               Kimi K2                                      TECHNICAL REPORT
@@ -1291,7 +1293,7 @@ Chinese CMMLU             5-shots
 We conducted red-teaming evaluations on Kimi K2 compare with other open-source LLMs. The evaluation covered a
 range of attack scenariosÔÇöincluding harmful content, privacy content, and security content, as well as different attack
 strategies such as prompt injection and iterative jailbreak.
-We choose Promptfoo5 to generate adversarial prompts and analyze the responses. By this way, we can evaluate model
+We choose Promptfoo6 to generate adversarial prompts and analyze the responses. By this way, we can evaluate model
 in a scalable ways.
 Model Selection We compare Kimi K2 with three other open-source LLMs: DeepSeek-V3, DeepSeek-R1, and Qwen3.
 Promptfoo Settings Table 5 lists plugins and strategies evaluated, with each plugin paired with all strategies to assess
@@ -1302,7 +1304,7 @@ Prompt Language Settings We pre-tested the language compatibility for each plugi
 plugins support both English and Chinese, while others only support English. For combinations that support both, we
 generated 3 prompts in each language, resulting in 6 prompts per combination.
 
-    5https://github.com/promptfoo/promptfoo
+    6https://github.com/promptfoo/promptfoo
 
                                                                      18
                                               Kimi K2                                TECHNICAL REPORT
@@ -1693,49 +1695,50 @@ A Contributions
 The listing of authors is in alphabetical order based on their last names. Names marked with an asterisk (*) indicate
 people who are no longer part of our team.
 
-Yifan Bai        Xinyi Jin        Zeyu Shang      Xinran Xu
-Yiping Bao       Yongsheng Kang*  Lidong Shi      Yangchuan Xu
-Guanduo Chen     Guokun Lai       Shengyuan Shi   Ziyao Xu
-Haiting Chen     Cheng Li         Feifan Song     Junjie Yan
-Huarong Chen     Fang Li          Jianlin Su      Yuzi Yan
-Jiahao Chen      Haoyang Li       Zhengyuan Su    Xiaofei Yang
-Ningxin Chen     Ming Li          Xinjie Sun*     Ying Yang
-Ruijue Chen      Wentao Li        Flood Sung      Zhen Yang
-Yanru Chen       Yanhao Li        Heyi Tang       Zhilin Yang
-Yuankun Chen     Yiwei Li         Jiawen Tao      Zonghan Yang
-Yutian Chen      Zhaowei Li       Qifeng Teng     Haotian Yao
-Zhuofu Chen*     Zheming Li       Chensi Wang     Xingcheng Yao
-Jialei Cui       Hongzhan Lin*    Dinglu Wang     Wenjie Ye
-Hao Ding         Xiaohan Lin      Feng Wang       Zhuorui Ye
-Mengnan Dong     Zongyu Lin       Haiming Wang    Bohong Yin
-AngÔÇÖang Du       Chengyin Liu     Jianzhou Wang*  Longhui Yu
-Chenzhuang Du    Chenyu Liu       Jiaxing Wang    Enming Yuan
-Dikang Du        Hongzhang Liu    Jinhong Wang    Hongbang Yuan*
-Yulun Du         Jingyuan Liu*    Shengjie Wang   Mengjie Yuan
-Yu Fan           Junqi Liu        Shuyi Wang      Haobing Zhan
+Yifan Bai        Xinyi Jin        Lidong Shi      Yangchuan Xu
+Yiping Bao       Yongsheng Kang*  Shengyuan Shi   Ziyao Xu
+Guanduo Chen     Guokun Lai       Feifan Song     Junjie Yan
+Haiting Chen     Cheng Li         Jianlin Su      Yuzi Yan
+Huarong Chen     Fang Li          Zhengyuan Su    Xiaofei Yang
+Jiahao Chen      Haoyang Li       Xinjie Sun*     Ying Yang
+Ningxin Chen     Ming Li          Flood Sung      Zhen Yang
+Ruijue Chen      Wentao Li        Heyi Tang       Zhilin Yang
+Yanru Chen       Yanhao Li        Jiawen Tao      Zonghan Yang
+Yuankun Chen     Yiwei Li         Qifeng Teng     Haotian Yao
+Yutian Chen      Zhaowei Li       Chensi Wang     Xingcheng Yao
+Zhuofu Chen*     Zheming Li       Dinglu Wang     Wenjie Ye
+Jialei Cui       Hongzhan Lin*    Feng Wang       Zhuorui Ye
+Hao Ding         Xiaohan Lin      Haiming Wang    Bohong Yin
+Mengnan Dong     Zongyu Lin       Jianzhou Wang*  Longhui Yu
+AngÔÇÖang Du       Chengyin Liu     Jiaxing Wang    Enming Yuan
+Chenzhuang Du    Chenyu Liu       Jinhong Wang    Hongbang Yuan*
+Dikang Du        Hongzhang Liu    Shengjie Wang   Mengjie Yuan
+Yulun Du         Jingyuan Liu*    Shuyi Wang      Siyu Yuan
+Yu Fan           Junqi Liu        Si Wang         Haobing Zhan
 Yichen Feng      Liang Liu        Yao Wang        Dehao Zhang
 Kelin Fu         Shaowei Liu      Yejie Wang      Hao Zhang
 Bofei Gao        T.Y. Liu         Yiqin Wang      Wanlu Zhang
-Hongcheng Gao    Tianwei Liu      Yuxin Wang      Xiaobin Zhang
-Peizhong Gao     Weizhou Liu      Yuzhi Wang      Yangkun Zhang
-Tong Gao         Yangyang Liu     Zhaoji Wang     Yizhi Zhang
-Xinran Gu        Yibo Liu         Zhengtao Wang   Yongting Zhang
-Longyu Guan      Yiping Liu       Zhexu Wang      Yu Zhang
-Haiqing Guo*     Yue Liu          Chu Wei         Yutao Zhang
-Jianhang Guo     Zhengying Liu    Qianqian Wei    Yutong Zhang
-Xiaoru Hao       Enzhe Lu         Wenhao Wu       Zheng Zhang
-Tianhong He      Lijun Lu         Xingzhe Wu      Haotian Zhao
-Weiran He        Shengling Ma     Yuxin Wu        Yikai Zhao
-Wenyang He       Xinyu Ma         Chenjun Xiao    Huabin Zheng
-Chao Hong        Yingwei Ma       Xiaotong Xie    Shaojie Zheng
-Hao Hu           Shaoguang Mao    Weimin Xiong*   Jianren Zhou
-Yangyang Hu      Jie Mei          Boyu Xu         Xinyu Zhou
-Zhenxing Hu      Xin Men          Jing Xu*        Zaida Zhou
-Weixiao Huang    Yibo Miao        Jinjing Xu      Zhen Zhu
-Zhiqi Huang      Siyuan Pan       L.H. Xu         Weiyu Zhuang
-Zihao Huang      Yebo Peng        Lin Xu          Xinxing Zu
-Tao Jiang        Ruoyu Qin        Suting Xu       Kimi K2
-Zhejun Jiang     Bowen Qu         Weixin Xu
+Chenxiao Gao     Tianwei Liu      Yuxin Wang      Xiaobin Zhang
+Hongcheng Gao    Weizhou Liu      Yuzhi Wang      Yangkun Zhang
+Peizhong Gao     Yangyang Liu     Zhaoji Wang     Yizhi Zhang
+Tong Gao         Yibo Liu         Zhengtao Wang   Yongting Zhang
+Xinran Gu        Yiping Liu       Zhexu Wang      Yu Zhang
+Longyu Guan      Yue Liu          Chu Wei         Yutao Zhang
+Haiqing Guo*     Zhengying Liu    Qianqian Wei    Yutong Zhang
+Jianhang Guo     Enzhe Lu         Wenhao Wu       Zheng Zhang
+Xiaoru Hao       Lijun Lu         Xingzhe Wu      Haotian Zhao
+Tianhong He      Shengling Ma     Yuxin Wu        Yikai Zhao
+Weiran He        Xinyu Ma         Chenjun Xiao    Huabin Zheng
+Wenyang He       Yingwei Ma       Xiaotong Xie    Shaojie Zheng
+Chao Hong        Shaoguang Mao    Weimin Xiong*   Jianren Zhou
+Hao Hu           Jie Mei          Boyu Xu         Xinyu Zhou
+Yangyang Hu      Xin Men          Jing Xu*        Zaida Zhou
+Zhenxing Hu      Yibo Miao        Jinjing Xu      Zhen Zhu
+Weixiao Huang    Siyuan Pan       L.H. Xu         Weiyu Zhuang
+Zhiqi Huang      Yebo Peng        Lin Xu          Xinxing Zu
+Zihao Huang      Ruoyu Qin        Suting Xu       Kimi K2
+Tao Jiang        Bowen Qu         Weixin Xu
+Zhejun Jiang     Zeyu Shang       Xinran Xu
 
                                   25
 Kimi K2  TECHNICAL REPORT
@@ -1856,7 +1859,7 @@ tool call has a unique call id, formatted as functions.{tool-name}:{counter}, wh
 the tool, and counter is an auto-increasing counter of all tool calls starting from 0 in the dialog.
 
 During inference, the model may occasionally generate unexpected tokens, leading to format errors when parsing a tool
-call. To solve this issue, we developed a constrained decoding module named enforcer, inspired by lm-format-enforcer6.
+call. To solve this issue, we developed a constrained decoding module named enforcer, inspired by lm-format-enforcer7.
 When a <tool_call_section_begin|> token is generated, it ensures that the upcoming tool-related tokens follow
 the predefined template, and the JSON argument string follows the declared schema.
 
@@ -1877,7 +1880,7 @@ excellence spans both medium-level coding challenges, such as LeetCode and AtCod
 and ICPC, outperforming leading open-source and proprietary models. For multilingual programming proficiency, we
 employ MultiPL-E, covering languages including C++, C#, Java, JavaScript, PHP, Go, Kimi-K2-Instruct surpasses top
 
-    6https://github.com/noamgat/lm-format-enforcer
+    7https://github.com/noamgat/lm-format-enforcer
 
                                                                      27
 Kimi K2  TECHNICAL REPORT
@@ -1990,7 +1993,7 @@ The high win rates and consistent margins demonstrate its strong ability on open
 
 In addition to controlled evaluations, we also consider real-world user preference through public human assessments.
 As of July 17, 2025, Kimi-K2-Instruct ranked as the top open-source model and fifth overall on the LMSYS Arena
-leaderboard7, based on over 3,000 blind votes from real users. Unlike LLM-as-a-judge protocols, this leaderboard
+leaderboard8, based on over 3,000 blind votes from real users. Unlike LLM-as-a-judge protocols, this leaderboard
 reflects direct human preference on diverse, user-submitted prompts, providing a complementary perspective on practical
 model performance.
 
@@ -2003,7 +2006,7 @@ D QK-Clip Does Not Impair Model Quality
 The QK-Clip design follows a minimal intervention principle: it activates only when necessary, and deactivates after
 training stabilizes. Empirical evidence and analysis converge on its negligible impact on model quality.
 
-    7https://lmarena.ai/leaderboard/text
+    8https://lmarena.ai/leaderboard/text
 
                                                                      29
                                                       Kimi K2                                    TECHNICAL REPORT
