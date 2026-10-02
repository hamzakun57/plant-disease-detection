# 🌿 VOTRE_PROJET

> **Projet dérivé.** Ce dépôt est un fork personnalisé du projet open source
> [plant-disease-detection](https://github.com/AyushSharma0802/plant-disease-detection)
> d'**Ayush Sharma**, sous licence MIT. Voir la section [Credits](#-credits--attribution)
> et la section [Licence](#-licence). Le code, le modèle et les données vous appartiennent
> uniquement dans la limite des droits que la licence d'origine vous accorde.

An AI-powered web application that detects plant diseases in real-time, provides disease impact analysis, recommends treatment products, and offers 24/7 expert guidance through an AI chatbot.

## ✨ Features

- **94.5% Accuracy Disease Detection** - Real-time prediction on 23 plant disease classes
- **< 2 Second Inference** - Lightning-fast predictions on CPU
- **AI Expert Chatbot** - 24/7 guidance powered by NVIDIA NIM (Llama 3.2)
- **Smart Product Recommendations** - Automatically matched to detected diseases
- **Shopping Cart** - Browse and manage products with persistent storage
- **Responsive Design** - Works on mobile, tablet, and desktop

## 🎯 Supported Crops & Diseases

- **Apple:** Scab, Black Rot, Cedar Apple Rust
- **Corn:** Gray Leaf Spot, Common Rust, Northern Leaf Blight
- **Pepper:** Bacterial Spot
- **Potato:** Early Blight, Late Blight, Leaf Roll
- **Tomato:** Early Blight, Late Blight, Leaf Mold, Septoria Spot, Spider Mites, Mosaic Virus, Target Spot, Yellow Leaf Curl Virus

## 🚀 Live Demo

- **Frontend:** [https://VOTRE_DOMAINE](https://VOTRE_DOMAINE)
- **API Documentation:** [https://api.VOTRE_DOMAINE/api/docs](https://api.VOTRE_DOMAINE/api/docs)

> À personnaliser : remplacez `VOTRE_DOMAINE` par vos propres URLs après déploiement.

## 🛠️ Tech Stack

### Backend
- **Framework:** FastAPI
- **ML Framework:** TensorFlow 2.15, Keras
- **Model:** MobileNetV2 (Transfer Learning)
- **Language:** Python
- **API:** REST with FastAPI
- **Chat API:** NVIDIA NIM (Llama 3.2)

### Frontend
- **Framework:** React 18
- **Build Tool:** Vite
- **Styling:** Tailwind CSS
- **State Management:** React Context API
- **Icons:** Lucide React

### Deployment
- **Backend:** Railway
- **Frontend:** Vercel
- **Version Control:** Git, GitHub

## 📊 Model Performance
Training Accuracy:    94.55%
Validation Accuracy:  94.536%
Test Accuracy:        92-94%
Precision:            90-93%
Recall:               90-92%
Inference Time:       < 2 seconds
Model Size:           100 MB

## 📁 Project Structure

```
VOTRE_PROJET/
├── backend/
│   ├── app/
│   │   ├── __init__.py
│   │   ├── main.py
│   │   ├── database.py
│   │   └── routes/
│   │       ├── __init__.py
│   │       ├── predict.py
│   │       └── chat.py
│   ├── ml_model/
│   │   ├── model.h5              ← NON versionné (ignoré par Git)
│   │   └── disease_mapping.json
│   ├── data/
│   │   └── Dataset/              ← NON versionné (ignoré par Git, ~530 Mo)
│   ├── requirements.txt
│   ├── .env.example
│   ├── run.py
│   ├── train_model.py
│   ├── evaluate_model.py
│   ├── generate_mapping.py
│   └── download_dataset.py
│
├── frontend/
│   ├── src/
│   │   ├── pages/
│   │   │   ├── Home.jsx
│   │   │   ├── Scanner.jsx
│   │   │   ├── Cart.jsx
│   │   │   └── Chat.jsx
│   │   ├── styles/
│   │   ├── context/
│   │   │   └── CartContext.jsx
│   │   ├── App.jsx
│   │   └── main.jsx
│   ├── public/
│   │   └── favicon.svg
│   ├── package.json
│   ├── vite.config.js
│   └── .env.example
│
├── Dockerfile
├── .gitignore
└── README.md
```

> **Fichiers volontairement absents du dépôt** (trop lourds ou sensibles) :
> `backend/data/` (~530 Mo d'images), `backend/ml_model/model.h5` (~100 Mo),
> `backend/.env` et `frontend/.env` (secrets). Voir `.gitignore`.

## 🚀 Quick Start

### Backend Setup

```bash
cd backend

# Create virtual environment
python -m venv venv
venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Create .env from the provided template, then fill in YOUR OWN key
# (get one at https://build.nvidia.com — no key is shipped in this repo)
cp .env.example .env

# Run server
python run.py
```

Server runs on: `http://localhost:8000`
API Docs: `http://localhost:8000/api/docs`

### Frontend Setup

```bash
cd frontend

# Install dependencies
npm install

# Create .env from the provided template, then point it at YOUR backend
cp .env.example .env

# Run dev server
npm run dev
```

App runs on: `http://localhost:5173`

## 🎯 How to Use

1. **Visit the app** at the live demo link
2. **Click "Scan Plant Now"**
3. **Upload a leaf image** (JPG or PNG)
4. **Wait < 2 seconds** for diagnosis
5. **See disease details:**
   - Disease name & description
   - Severity level (critical/high/medium/none)
   - Disease impact on crops
   - Affected plant parts
   - Treatment duration
6. **Browse product recommendations** (sorted by efficacy)
7. **Chat with AI expert** for additional guidance
8. **Add products to cart** and manage shopping

## 📊 Dataset

- **Source:** Custom dataset with 54,186 images
- **Classes:** 23 disease classes across 5 crops
- **Split:** 70% training, 15% validation, 15% testing
- **Augmentation:** 4x data multiplier through rotation, zoom, flip, brightness adjustment

## 🔧 API Endpoints

### Disease Prediction

## 🎓 Machine Learning Details

### Transfer Learning
- **Base Model:** MobileNetV2 (pre-trained on ImageNet)
- **Approach:** Freeze first 150 layers, train custom head
- **Benefit:** 95% reduction in training time, better accuracy with limited data

### Data Augmentation
- Random rotation (±20°)
- Horizontal/vertical flips
- Zoom variations (0.8x-1.2x)
- Brightness/contrast adjustment
- **Result:** 4x more training variations

### Regularization Techniques
- **Dropout:** 50% (hidden) & 30% (output layer)
- **Batch Normalization:** Normalize inputs to each layer
- **Early Stopping:** Stop when validation loss plateaus
- **Learning Rate Reduction:** Lower LR when progress stalls

### Model Architecture
nput (224×224×3)
↓
MobileNetV2 Base (frozen)
↓
Global Average Pooling (7×7×1280 → 1280)
↓
Dense(256) + ReLU + Dropout(0.5)
↓
Dense(128) + ReLU + Dropout(0.3)
↓
Dense(23, softmax) - Output layer
## 🌍 Real-World Impact

- **Helps farmers identify diseases in seconds** vs days of waiting for expert
- **Reduces crop loss by 15-25%** through early detection
- **Saves ₹50,000-100,000 annually per farmer**
- **Available 24/7** with AI expert guidance
- **Completely free** for disease detection

## 📈 Scalability

- **Current:** Works on single instance (Railway free tier)
- **Production-ready:** Designed for 100K+ concurrent users
- **Optimization:** Load balancing, caching, database optimization planned
- **Model deployment:** TensorFlow Serving or ONNX Runtime ready

## 🔐 Privacy & Security

- ✅ No image storage (processed and deleted immediately)
- ✅ HTTPS encryption (TLS 1.3)
- ✅ CORS protection (frontend-only API access)
- ✅ No user tracking or personal data collection
- ✅ GDPR compliant by design

## 🚧 Future Features

- [ ] Mobile app (React Native)
- [ ] Offline detection capability
- [ ] Pest detection (expand to 50+ classes)
- [ ] Nutrient deficiency detection
- [ ] IoT sensor integration
- [ ] Real-time video detection
- [ ] Payment gateway integration
- [ ] User authentication & history
- [ ] Regional language support

## 📝 Limitations

- Currently optimized for clear, well-lit leaf images
- Limited to 23 major diseases (expanding in progress)
- Requires internet for chatbot (offline model planned)
- Regional variations not fully captured (collecting regional data)

## 💡 Key Achievements

✅ **94.5% accuracy** on 23 disease classes
✅ **< 2 second inference** time on CPU
✅ **100MB model size** (fits any device)
✅ **Zero overfitting** (94.55% train = 94.536% validation)
✅ **Full-stack implementation** (ML + Backend + Frontend)
✅ **Production-ready** (deployed to Railway & Vercel)
✅ **AI-powered** (24/7 expert guidance)
✅ **E-commerce ready** (shopping cart + recommendations)

## 🤝 Contributing

Contributions are welcome! Areas for improvement:
- Additional disease classes
- Regional dataset collection
- Mobile app development
- Performance optimization
- UI/UX improvements

## 📧 Contact & Support

*À personnaliser — remplacez les placeholders ci-dessous par vos informations.*

- **GitHub:** https://github.com/VOTRE_GITHUB/VOTRE_PROJET
- **Email:** VOTRE_EMAIL
- **LinkedIn:** https://www.linkedin.com/in/VOTRE_GITHUB/
- **Website:** https://VOTRE_DOMAINE

## 📄 License

This project is open source and available under the **MIT License**.

> ⚠️ **Note importante sur la licence.** Ce dépôt est un **fork** du projet
> [`plant-disease-detection`](https://github.com/AyushSharma0802/plant-disease-detection)
> d'Ayush Sharma. La licence MIT autorise la réutilisation, la modification et la
> redistribution, **y compris commerciale**, mais elle **impose de conserver la
> mention de copyright de l'auteur d'origine**. Cette attribution est assurée
> par la section [Credits](#-credits--attribution) ci-dessous.
>
> Le projet d'origine ne contient **pas de fichier `LICENSE`**, uniquement cette
> mention dans son README. Si vous distribuez ce code, ajoutez un fichier `LICENSE`
> MIT à la racine en conservant la ligne `Copyright (c) <année> Ayush Sharma`.
>
> Les **données** (PlantVillage) et le **modèle ML** ne sont pas couverts par la
> licence MIT du code : vérifiez leurs licences respectives avant toute
> redistribution (voir [Credits](#-credits--attribution)).

## 🙏 Credits & Attribution

### Auteur du projet d'origine

Ce projet est un **fork personnalisé**. L'intégralité de l'architecture, du code
source, du modèle d'apprentissage et de la documentation ci-dessus provient du
projet open source suivant :

- **Projet :** [plant-disease-detection](https://github.com/AyushSharma0802/plant-disease-detection)
- **Auteur original :** **Ayush Sharma**
- **Licence :** MIT (voir [Licence](#-licence))
- **Contact de l'auteur d'origine :**
  - GitHub — https://github.com/AyushSharma0802
  - Email — aayushparasar0802@gmail.com
  - LinkedIn — https://www.linkedin.com/in/ayush-sharma-7b0575256/

Merci à l'auteur d'origine pour ce travail.

### Ressources et outils tiers

- **Dataset :** PlantVillage (via Kaggle — `vipomoondal/plantvillage`) + données régionales.
  *Le dataset PlantVillage est soumis à sa **propre licence** (CC BY-SA / CC BY selon
  la version), distincte de la licence MIT du code. Toute redistribution du dataset
  doit respecter cette licence et maintenir sa citation. Le dataset n'est pas
  versionné dans ce dépôt.*
- **Modèle ML :** MobileNetV2 (pré-entraîné sur ImageNet) — transfer learning.
  *Les poids `model.h5` sont distribués par l'auteur d'origine via Hugging Face
  (`AYUSHHHH99/_plant-disease-model`) et ne sont pas versionnés dans ce dépôt.
  Vérifiez les conditions de redistribution avant de les republier.*
- **ML Framework :** TensorFlow & Keras Team
- **AI API :** NVIDIA NIM (Llama 3.2)
- **Outils de déploiement cités par le projet d'origine :** Railway & Vercel

---

**Fork personnalisé par VOTRE_NOM** — <VOTRE_EMAIL>

*Basé sur le projet original de Ayush Sharma (MIT). Voir [Credits](#-credits--attribution).*

*AI for Agriculture | Helping Farmers Save Crops | Technology for Good* 🌾
