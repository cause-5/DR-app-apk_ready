# DR-app
End-to-end app providing early screening of diabetic retinopathy (DR), fully build and designed front end, AI chatbot assistance, FAQs, etc.
The back-end shows mild, mod, and severe. But for the final app, there is only a binary classification. 


~Weights + models are not part of this repo. Contact the author if you wish to see the model~

https://dr-render.onrender.com/docs
---
Now runs on Render + EAS. expo. Go to https://dr-render.onrender.com/docs




## How to run on Mac in VS Code LOCAL

### 1. Open Terminal
cd to folder

### 2. Create virtual environment
```bash
python3 -m venv .venv
```

### 3. Activate it
```bash
source .venv/bin/activate
```

You should now see `(.venv)` in the terminal.

### 4. Install packages
```bash
pip install --upgrade pip
pip install -r requirements.txt
```

### 5. Start the backend
```bash
uvicorn app:app --reload
```
(Different for mac:  uvicorn app:app --host 0.0.0.0 --port 8000 --reload)


### 6. Open Swagger docs
In browser open:

- http://127.0.0.1:8000/docs
- http://127.0.0.1:8000/health
- http://127.0.0.1:8000/api/model/info

### 7. UI
npx expo start once cd to frontend folder at seprate terminal

---
Docs; main tests
**Expected outputs 
**


### Test 1: health
Expected output example:
```json
{"status":"ok","app":"DR Screening Backend","version":"1.0.0","model_mode":"auto","quality_weights_found":false,"dr_weights_found":false}
```

### Test 2: analyze image

If image quality is poor, it should reject the image.
If quality is usable or good, it returns a prediction JSON.
example: 
{
  "success": true,
  "can_analyze": true,
  "message": "Analysis completed.",
  "quality": {
    "quality_label": "good",
    "quality_score": 85,
    "metrics": {
      "blur_score": 81.37,
      "brightness_score": 76.73,
      "contrast_score": 43.86,
      "centering_score": 40.26,
      "width": 726,
      "height": 579
    },
    "issues": [
      "retina may not be centered properly"
    ],
    "recommendations": [],
    "source": "heuristic"
  },
  "prediction": {
    "grade": 1,
    "label": "Mild",
    "confidence": 0.854,
    "risk_level": "low",
    "summary": "Small early abnormalities may be present. Follow-up screening is recommended.",
    "details": {
      "next_steps": "Please arrange a follow-up eye exam.",
      "screening_only": true,
      "not_medical_diagnosis": true,
      "model_note": "Real regression model loaded from dr_model.pth."
    },
    "features": null,
    "source": "real:dr_model.pth",
    "score": 1.146
  },
  "debug": {
    "stage": "prediction_complete"
  }
}

### Test 3: Chatbot Qs
{
  "answer": "**Where to check your eye health for diabetes**\n\n| Option | What it offers | Where it’s located | How to get started |\n|--------|----------------|--------------------|--------------------|\n| **Waterloo Eye Institute (University of Waterloo)** | Dilated retinal exams, advanced imaging (OCT, wide‑field photography), and specialized treatments (laser, anti‑VEGF) | Waterloo & Kitchener clinics | Ask your family doctor for a referral or book an appointment directly through the Institute’s website. |\n| **Waterloo Regional Eye Program** (St. Mary’s General Hospital & satellite sites) | Comprehensive medical & surgical eye care, including local retinal surgery | Kitchener, Waterloo, Cambridge | Contact the program’s intake line; you can often be seen by an ophthalmologist with a referral from an optometrist. |\n| **Local optometry clinics** – e.g., Innovation Eye Clinic, G&G Eye Doctors, Waterloo Vision Care | Routine diabetic eye exams with retinal imaging; OHIP‑covered for diabetics | Waterloo, Kitchener, Cambridge | Call the clinic, mention you’re a diabetes patient, and request a dilated exam. |\n| **Waterloo Wellington Diabetes Regional Coordination Centre** (Cambridge) | Coordinates overall diabetes care, which improves eye health | Cambridge | Book a diabetes review; your coordinator can connect you with eye‑care specialists. |\n\n### Quick steps to get checked\n\n1. **Start with your family doctor** – they can confirm your diabetes status and give you a referral to an optometrist or ophthalmologist.  \n2. **Book a dilated eye exam** – an optometrist can capture retinal images; if abnormalities are noted, the images are sent to an ophthalmologist for review.  \n3. **Discuss AI screening tools** – some clinics use AI‑assisted retinal screening as an adjunct. It’s helpful but not a replacement for a full dilated exam.  \n4. **Follow up** – if any changes are detected, your provider will outline next steps (laser therapy, anti‑VEGF injections, or surgical options).  \n\nEarly detection and proactive management can preserve vision, so consider scheduling an exam soon. If you have any concerns, bring them up during your appointment—your eye care team is there to support you.",
  "sources": [
    "handle diabetic retinopathy, with education and coordinated care. - **Waterloo Eye Institute (University of Waterloo)**: Offers specialized ocular disease services, imaging (including for diabetic retinopathy), and urgent care at their Waterloo and Kitchener clinics. Great for monitoring and management. - **Local optometry clinics** (e.g., Innovation Eye Clinic, G&G Eye Doctors, Waterloo Vision Care): Provide diabetic eye exams with advanced retinal imaging. Many are OHIP-covered for diabetics and can refer to specialists.- **Waterloo Wellington Diabetes Regional Coordination Centre** (Cambridge): Supports overall diabetes care, which indirectly helps eye health through better management. For advanced treatments like anti-VEGF injections, laser therapy, or vitrectomy, you'll likely be referred through the regional program or to nearby specialists in Hamilton if needed. Start with your family doctor or optometrist for a referral. Check wait times for cataract or retinal procedures via the regional program. Early detection and proactive management make a huge difference — many people maintain good vision with proper care. If you're concerned, book that eye exam soon and discuss AI tools with your provider. Stay informed and in control! Consult a healthcare professional for personalized advice, as this is general information.",
    "(This model was trained using CNN, not always true): - CNN-based models aren't perfect — they can miss subtle or early changes, produce false positives/negatives, or struggle with image quality, lighting, or unusual cases. Accuracy might drop in real-world settings compared to controlled studies (e.g., lower sensitivity for mild DR). - They don't replace a full dilated exam by an ophthalmologist, which checks for other issues like glaucoma, cataracts, or macular details via OCT. - AI might not catch diabetic macular edema as reliably without additional tools, and it lacks the holistic view of your overall health. - Always confirm results with a real doctor — I've learned not to rely solely on the app for peace of mind. It's a helpful screening tool, not a diagnosis. Overall, it's motivated me to stay on top of my health, but it's one piece of the puzzle. ### Good places for treatment in the Kitchener-Waterloo-Cambridge region In the Waterloo Region (Ontario, Canada), several options exist for diabetic eye care, screening, and treatment: - **Waterloo Regional Eye Program** (at St. Mary’s General Hospital and other sites in Kitchener/Waterloo/Cambridge): Comprehensive medical and surgical eye care, including retinal surgeries (now available locally, reducing need to travel). They handle diabetic retinopathy, with education and coordinated care. - **Waterloo Eye Institute (University of Waterloo)**: Offers specialized ocular disease services, imaging (including for diabetic",
    "in type 2 at diagnosis due to undetected years). - Poor glycemic control (high HbA1c). - High blood pressure and high cholesterol. - Kidney disease (nephropathy). - Pregnancy. - Ethnicity (higher in Black, Hispanic, Native American populations). - Smoking, obesity, sedentary lifestyle, and poor diet. Lifestyle factors like inconsistent blood sugar management, high-fat/sugar diets, lack of exercise, and ignoring comorbidities greatly elevate risk. Genetics and family history also play a role. ### Prevention techniques Prevention centers on **tight control of diabetes and related conditions**: - Maintain target blood glucose, blood pressure, and cholesterol levels (e.g., HbA1c <7% if safe). - Eat a balanced diet rich in leafy greens, colorful vegetables, and whole foods; limit processed sugars and saturated fats. - Exercise regularly (aim for 150 minutes/week of moderate activity). - Quit smoking. - Take medications as prescribed and attend regular diabetes check-ups. - Annual (or more frequent) dilated eye exams for early detection. Good control can slow, stop, or even reverse some early changes. ### What frequency should you get tested? Guidelines generally recommend: - **Type 1 diabetes**: First dilated exam 3–5 years after diagnosis, then annually (or more if retinopathy present). - **Type 2 diabetes**: Exam at diagnosis, then annually. - If retinopathy is present, frequency increases: every 6–12 months for mild/moderate NPDR; every 3–4 months for severe or proliferative"
  ]
}

---

## What the endpoints do

### `GET /health`
Basic health check.

### `GET /api/model/info`
Shows whether real model weights are present.

### `POST /api/analyze`
Main endpoint.
- input: retinal image
- output: quality result + DR prediction

### `POST /api/chat/index-pdf`
Upload a PDF and index it for the later chatbot step. NOT for users. 

### `GET /api/chat/ask?question=...`
Ask a question against the indexed PDF.


Laisha Soni ©2026
