# TECHIN 515 – Lab 3: ESP32 Sorting Hat

This project implements a Hogwarts-style "Sorting Hat" using ESP32, buttons, an OLED screen, and a decision tree machine learning model. It asks the user 10 personality-related questions and classifies them into one of four houses: Gryffindor, Hufflepuff, Ravenclaw, or Slytherin.

---

## 🔧 Setup

**Hardware:**

- XIAO ESP32C3 board
- 4 push buttons (connected to GPIO2–5)
- OLED display (SSD1306, 128x64, connected via I2C GPIO8–9)
- Breadboard and jumper wires

**Software:**

- Arduino IDE
- Adafruit_SSD1306 and Adafruit_GFX libraries
- EloquentTinyML for decision tree inference
- Model trained from `sorting_hat_large_dataset.csv` (3000 entries)

---

## ▶️ How to Use

1. Power the ESP32 device.
2. Questions will show on screen with 4 options.
3. Press the corresponding button (1–4) to select your answer.
4. After 10 questions, your house will be revealed on the screen.
5. The ESP will reset automatically for a new user.

---

## 📊 Discussion

### Are all 10 questions necessary?

Not necessarily. Based on exploratory feature analysis and decision tree structure, some questions contribute more to final classification than others. For example:

- **Q1 (Values)** and **Q4 (Challenges)** strongly correlate with house labels.
- Questions like **Q7 (Pet)** or **Q6 (Mystery book)** contribute less meaningfully and could be removed to reduce user fatigue.

If optimizing for user experience, we could reduce to 6–7 key questions without major accuracy loss.

---

### How to improve the model?

1. **Accuracy:**
   - Collect real-world user-labeled data (vs synthetic)
   - Use Random Forest or ensemble models offline and distill into a compact rule-based version for edge

2. **Efficiency:**
   - Quantize or prune the tree using TinyML optimization methods
   - Limit max depth of tree to reduce inference cost

---

### Additional Hardware Ideas

- **Microphone** to allow voice-based answering (speech-to-intent)
- **Camera module** to track facial expression or eye contact
- **RGB LEDs** to visualize house assignment with color feedback
- **Haptic vibration** for tactile feedback during question transitions

---

### Is decision tree still suitable?

Yes—for this version. Decision trees are:

- Interpretable
- Fast to compute
- Easy to convert to C++ for microcontrollers

However, for multi-modal inputs (e.g. audio, image), you'd need more expressive models like tiny CNNs or keyword spotting RNNs. In that case, TensorFlow Lite Micro models would be more appropriate.

---

## 📦 Deliverables

- [✔️ GitHub Repo with full source code](https://github.com/Znrain/515lab3)
- ✅ Trained dataset: `sorting_hat_large_dataset.csv` (3000 samples)
- ✅ All Arduino source code files with comments
- ✅ Documentation + technical answers (this README)
- 🎥 [Pending] Demo video showing interaction on hardware

---

*Created by Xinyu Wang for TECHIN 515 Spring 2025.*
