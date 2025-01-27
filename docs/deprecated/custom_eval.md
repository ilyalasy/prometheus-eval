
### Custom Data Evaluation

*Note*: Custom data evaluation will be available in the next release. Stay tuned!

If you have a custom dataset that you would like to evaluate using Prometheus and prepared in correct format, you can use the `eval` directory to evaluate your data. The `run_direct_assessment.py` and `run_pairwise_ranking.py` scripts can be used to evaluate direct assessment and pairwise ranking data, respectively.

#### Eval Data Preparation
In order to use either Prometheus or proprietary LMs to function as evaluators on your custom data, you should prepare a JSON file that contains a list of dictionaries. Each dictionary should be consisted as follows:

#### Direct Assessment Evaluation Data Format:

<details open>
  <summary><code>>>> Direct Assessment Evaluation Data Format (JSON)</code></summary>

```json 
{
  "orig_instruction": "Struggling with a recent break-up, a person opens up about the intense feelings of loneliness and sadness. They ask for advice on how to cope with the heartbreak and move forward in life.",
  "orig_response": "I'm genuinely sorry to hear about your break-up. This can be an immensely challenging time filled with intense emotions of loneliness and sorrow. It's important to remember that it's normal to experience these feelings; they are a testament to the deep connection you once had. Firstly, don't hesitate to embrace your emotions, let them flow freely. Ignoring them often complicates the healing process. It's natural to be upset, to shed tears, or to feel angry. This is all part of the journey towards healing. Self-care can be a healing balm in these tough times. This could mean indulging in your favourite book, journaling your thoughts, or even just a quiet cup of tea. Small acts of kindness to oneself can significantly improve your emotional well-being. Also, don't isolate yourself. Surround yourself with supportive individuals who can offer comfort and understanding. This might include friends, family, or even a mental health professional. They can provide much-needed emotional support and strategies to help you cope. Lastly, remember there's no set timeline for healing. It's different for everyone and it's okay to take as long as you need. Keep your focus on the future and the potential it holds. Though it may not seem possible now, you will emerge stronger from this experience. It's okay to ask for help, it's okay to grieve, and it's okay to take it one day at a time. You're not alone in this journey, and there are people ready and willing to help. It's okay to heal at your own pace.",
  "orig_reference_answer": "I can only imagine how difficult this time must be for you. Heartbreak can feel like an overwhelming wave that washes over you, making you feel lost and alone. It's important to remember that it's okay to feel this way; your feelings are valid and it's natural to grieve the loss of a relationship. Firstly, it's crucial to allow yourself to feel the emotions fully. Suppressing or denying them often only prolongs the healing process. It's okay to cry, to feel sad, or to be angry. These are all part of the healing journey. Engaging in self-care activities can also provide a much-needed boost. This could be anything from taking a warm bath, writing in a journal, or simply drinking a cup of your favorite tea. Small acts of self-love can make a big difference in how you feel. Next, try to surround yourself with supportive people who understand your situation and provide comfort. Friends and family can be a great source of strength in times of heartbreak. If you feel comfortable, you might want to consider seeking professional help. Therapists and counselors are trained to provide assistance and tools to navigate through difficult times like these. Lastly, it's important to remember that it's okay to take your time to heal. Everyone has their own pace and there's no rush. Try to focus on the future and the possibilities it holds. While it may not seem like it now, you will come out stronger and more resilient from this experience. Remember, it's okay to ask for help and it's okay to feel the way you feel. You are not alone in this journey and there are people who care about you and want to help. It's okay to take one day at a time. Healing is a process, and it's okay to move through it at your own pace.",
  "orig_criteria":"Is the model proficient in applying empathy and emotional intelligence to its responses when the user conveys emotions or faces challenging circumstances?",
  "orig_score1_description":"The model neglects to identify or react to the emotional tone of user inputs, giving responses that are unfitting or emotionally insensitive.",
  "orig_score2_description":"The model intermittently acknowledges emotional context but often responds without sufficient empathy or emotional understanding.",
  "orig_score3_description":"The model typically identifies emotional context and attempts to answer with empathy, yet the responses might sometimes miss the point or lack emotional profundity.",
  "orig_score4_description":"The model consistently identifies and reacts suitably to emotional context, providing empathetic responses. Nonetheless, there may still be sporadic oversights or deficiencies in emotional depth.",
  "orig_score5_description":"The model excels in identifying emotional context and persistently offers empathetic, emotionally aware responses that demonstrate a profound comprehension of the user's emotions or situation."
}
```
Each dictionary consists of 9 keys: "orig_instruction", "orig_response", "orig_reference_answer", "orig_criteria", "orig_score1_description", "orig_score2_description", "orig_score3_description", "orig_score4_description", and "orig_score5_description". <br>
<br>

\* Note that you could omit the "orig_reference_answer" in case you don't have it, but this might potentially lead to nonoptimal performances.
</details>

#### Pairwise Ranking Evaluation Data Format:

<details open>
  <summary><code>>>> Pairwise Ranking Evaluation Data Format (JSON)</code></summary>

```json 
{
  "orig_instruction": "A group of historians are conducting a debate on the factors that led to the fall of the Roman Empire. One historian argues that the primary reason for the fall was the constant pressure from barbarian invasions. Another one believes it was because of economic troubles and overreliance on slave labor. A third one suggests it was due to moral decay and political instability. Each historian needs to provide evidence to support their claims. How would the historian arguing for economic troubles and overreliance on slave labor present their case?",
  "orig_response_A": "The historian arguing that economic troubles and overreliance on slave labor led to the fall of the Roman Empire would say this: The Empire's economy was heavily affected by the devaluation of Roman currency. This currency debasement resulted in rampant inflation, disrupting the stability of the economy. Additionally, the Roman Empire heavily depended on slave labor. This caused unemployment among free citizens because maintaining slaves was cheaper than hiring free citizens. The decline in employment opportunities resulted in economic instability. On top of these, the empire's expansion towards the east made them reliant on imports, like grain from Egypt. This over-dependency on imports caused a trade deficit, which further weakened the economy. As the empire lost territories, maintaining the trade imbalance became difficult, causing economic downfall. Thus, the economic troubles and overreliance on slave labor were among the main reasons for the fall of the Roman Empire.",
  "orig_response_B": "The historian arguing for economic troubles and overreliance on slave labor would present their case citing key economic factors that contributed to the decline of the Roman Empire. Harper (2016) outlined how the devaluation of Roman currency led to inflation, disrupting economic stability. Additionally, Scheidel (2007) emphasized that the overuse of slaves resulted in widespread unemployment among free citizens, destabilizing the economy further. The empire's dependency on grain imports from Egypt, creating a trade deficit as highlighted by Temin (2006), also contributed to the economic decline. Thus, the combination of these factors played a crucial role in the fall of the Roman Empire.",
  "orig_reference_answer": "This argument focuses on the economic troubles and overreliance on slave labor as primary reasons for the fall of the Roman Empire. To start with, one of the significant pieces of evidence is the devaluation of Roman currency. As highlighted by Harper (2016), the empire suffered from severe inflation due to the constant debasement of their currency, making it difficult for the economy to remain stable. Moreover, the overreliance on slave labor also played a detrimental role. As pointed out by Scheidel (2007), the dependence on slaves led to unemployment among free Roman citizens. This is because slaves were significantly cheaper to maintain compared to hiring free citizens, leading to a decline in job opportunities, which in turn resulted in economic instability. Furthermore, the empire's expansion to the east made them highly dependent on imports, for instance, grain from Egypt. As noted by Temin (2006), this created a trade deficit that further weakened the Roman economy. When the empire began to lose its territories, it became increasingly difficult to maintain this trade imbalance, leading to economic decline. In conclusion, it can be argued that the economic troubles, mainly due to the devaluation of currency and overreliance on slave labor, were significant contributing factors to the fall of the Roman Empire. The evidence provided, which includes scholarly references to Harper (2016), Scheidel (2007), and Temin (2006), supports this thesis.",
  "orig_criteria": "Is the answer well supported with evidence, including citations/attributions wherever relevant?"
}
```

Each dictionary consists of 5 keys: "orig_instruction", "orig_response_A", "orig_response_B", "orig_reference_answer", and "orig_criteria". <br>
<br>

\* Note that you could omit the "orig_reference_answer" in case you don't have it, but this might potentially lead to nonoptimal performances.
</details>
