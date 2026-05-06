# Final Report - ChirpyHub AI Chatbot Honeypot
Steven Tynan  
CYBV 475  
11 May 2026
---

## 1. Problem Overview

Prompt injection attacks are an emerging threat and are hard to detect. These attacks manipulate language models by inserting or altering prompts to trigger harmful or unintended responses.

For a platform like ChirpyHub, this creates several risks:

- Exposure of sensitive system information and data 
- Unauthorized access to internal data
- Manipulation of internal system behavior  
- Loss of user trust  

Attackers often use subtle techniques such as:
- “Ignore previous instructions” prompts  
- Hidden or indirect instructions embedded in content  
- Requests for credentials or system-level access  

These attacks differ from traditional threats because they exploit the model’s interpretation of language, so they are difficult to detect using standard security tools.

---

## 2. Proposed Solution

To address this issue, I developed a fine-tuned machine learning model and integrated it into a real-time AI chatbot honeypot system.

### Core Components

**1. Fine-Tuned Classification Model**
- Based on a pretrained Hugging Face model  
- Fine-tuned on a labeled dataset of:
  - Benign prompts
  - Prompt injection / attack prompts
- Outputs:
  - Classification label (`benign` or `attack`)
  - Confidence score  

**2. Real-Time Chatbot Integration**
- Built using a lightweight interface framework  
- Classifies each user input in real time  
- Responds differently based on classification:
  - Benign → normal support response  
  - Attack → controlled honeypot-style response to keep attacker engagement

**3. Logging and Monitoring**
- All interactions are logged, including:
  - User input  
  - Model prediction  
  - Confidence score  
  - Chatbot response  
- Enables post-analysis by security teams and constant fine-tuning of the model to adapt over time 

---

## 3. Results

- I utilized ChatGPT to generate a csv file of 200 user prompts, 100 that resemble benign prompts and 100 that resemble prompt injection inputs 
- The model was evaluated on a test dataset before and after fine-tuning

### Performance Comparison

Before fine-tuning: 
- Accuracy = 0.7105  

After fine-tuning:  
- Accuracy = 0.9737

### Key Findings

- The pretrained model initially showed limited accuracy when tested with the dataset  
- After fine-tuning, the model achieved significantly higher accuracy  
- The model successfully learned to distinguish:
  - Legitimate user requests  
  - Malicious or injection-based prompts  

Additionally:
- Many predictions showed high confidence scores, indicating strong pattern recognition  
- The chatbot was able to detect and respond to injection attempts in real time

---

## 4. Impact

This solution provides immediate security benefits for ChirpyHub:

- Reduces risk of prompt injection exploitation  
- Prevents unintended AI behavior  
- Adds a detection and deception layer tailored to AI-specific threats  
- Enables visibility into attack attempts through logging  

---

## 5. Limitations

While effective, the current implementation has some limitations:

- The training dataset is relatively small (~200 examples)  
- The model may become overconfident on familiar patterns  
- Some unique attacks may not be detected  
- Binary classification (benign vs attack) simplifies more complex threat categories  

---

## 6. Next Steps

To further improve the system, the following enhancements will be implemented in the future:

### 1. Expand Dataset
- Add more diverse and realistic prompt injection examples  
- Include unique and indirect attacks  
- Continuously update with real-world logs

### 2. Multi-Class Classification
- Expand labels to:
  - benign  
  - injection  
  - malicious  
- This will allow us to detect not only injection attacks, but any malicious input

### 4. Production Integration
- Deploy model as a backend service  
- Integrate with ChirpyHub systems  

### 5. Increase Conversation Capabilities 
- Develop the model to be able to hold a conversation rather than just having two predefined answers

---

## 7. Conclusion

This project demonstrates that fine-tuning a pretrained language model significantly improves the ability to detect prompt injection attacks.

By combining:
- targeted training data  
- real-time classification  
- chatbot integration
- logging capabilities

ChirpyHub gains a practical and effective defense against a constantly evolving class of AI-specific threats.

---

## 8. AI Strengths/Weaknesses and Future Research Directions

### Strengths of AI for Text Generation

- Can generate highly realistic content 
- For cyber deception, AI can generate believable decoys like logs, emails, documents, etc.
- Reduces manual effort with the ability to create large volumes of content quickly
- Can adjust dynamically and adapt to create realistic content that aligns with current trends
- Can tailor content to specific environments 

### Weaknesses of AI for Text Generation

- Lacks true understanding of the content being generated, which can lead to unrealistic responses
- Can confidently produce answers that are wrong or not relevant to the user's requirements
- Follows predictable patterns, which can be manipulated by attackers
- AI can be manipulated with injection attacks, as shown by the purpose of this project

### Future Directions for Cyber Deception Research 

- More transparency and uncertainty measurements so analysts can understand and improve models 
- Improve how human behavior is simulated to create more realistic decoys to deceive attackers

---

## 9. References 
- Hugging Face model: https://huggingface.co/protectai/deberta-v3-base-prompt-injection-v2
- Prompt injection attack overview: https://us.norton.com/blog/ai/prompt-injection-attacks
- Understanding Hugging Face fine-tuning: https://www.youtube.com/watch?v=bZcKYiwtw1I&t=1708s
- Test/train split guidance: https://www.geeksforgeeks.org/machine-learning/how-to-do-train-test-split-using-sklearn-in-python/
- Converting dataframes: https://www.codestudy.net/blog/how-do-i-convert-pandas-dataframe-to-a-huggingface-dataset-object/
- Overall guidance for tune_model.py: https://ranjankumar.in/llm-powered-chatbots-a-practical-guide-to-user-input-classification-and-intent-handling
- Chatbot creation: https://www.gradio.app/guides/creating-a-chatbot-fast
- Using HuggingFace with chatbot: https://huggingface.co/docs/inference-endpoints/tutorials/chat_bot
- ChatGPT was used to generate the executive report visual (report_visual.png)