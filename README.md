<div align="center">
  
# 👋 Salut, je suis Naim Fertas

### 🚀 Data Engineer | Cloud & AI Enthusiast

[![Typing SVG](https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=28&pause=1000&color=2E9EF7&center=true&vCenter=true&width=700&lines=Data+Engineer+%E2%80%A2+AI+Enthusiast+%E2%9C%A8;Building+Scalable+Pipelines;Cloud+%26+ML+Engineering)](https://git.io/typing-svg)

[![Profile Views](https://komarev.com/ghpvc/?username=ni3ma-fer&label=Profile%20Views&color=0e75b6&style=flat)](https://github.com/ni3ma-fer)
[![GitHub followers](https://img.shields.io/github/followers/ni3ma-fer?label=Followers&style=social)](https://github.com/ni3ma-fer?tab=followers)

</div>

---

## 🚀 À propos de moi

Je suis Naim, Data Engineer passionné par les architectures cloud et les solutions ML/AI reproductibles. J’aime construire des pipelines fiables, automatiser l’ingestion et rendre les modèles exploitables en production.

- 🔭 Actuellement : projets Data & AI
- 🌱 En apprentissage : AWS, Azure, Apache Spark
- 🎯 Objectif : Devenir Data Engineer / AI Specialist de référence
- 📄 CV : https://flowcv.com/resume/0s5t9jf1l6lt

---

## 🧰 Stack technique (ciblée pour Data & AI)

- Langages : Python, SQL
- Cloud & Infra : AWS (S3, Lambda, IAM), Azure (bases), Docker
- Traitement & Big Data : Apache Spark, pandas, NumPy
- Bases de données : PostgreSQL, MongoDB
- Machine Learning : scikit-learn, pipelines d’évaluation
- Outils : Git, GitHub, VS Code, Jupyter

> Note : La liste est concentrée sur ce qui sert les projets data/IA en production. Si tu veux, on peut ajouter des badges ou des "skill bars" SVG.

---

## 📚 Expérience & Compétences

J’ai restructuré la section pour la rendre lisible et orientée produit. Chaque bloc indique l’usage typique et les compétences clés.

### Ingénierie des données
- Conception et exécution de pipelines ETL/ELT (batch & micro-batch)
- Traitements distribué avec Apache Spark
- Modélisation SQL pour analytics et data warehousing

### Cloud & Déploiement
- AWS : stockage (S3), compute serverless (Lambda), gestion d’identités (IAM)
- Docker : conteneurisation et reproductibilité
- CI/CD basique : GitHub Actions pour automatiser tests et déploiement

### Machine Learning & IA
- Pré-traitement et feature engineering avec pandas & NumPy
- Pipelines d'entraînement et d'évaluation (scikit-learn)
- Notebooks reproductibles (Jupyter) et visualisations simples

### Qualité & Observabilité
- Tests unitaires pour transformations de données
- Logging et monitoring basique des jobs
- Validation de schéma et checks de qualité des données

---

## 🔥 Projets sélectionnés

- AI-model-evaluator — Plateforme d’évaluation et comparaison de modèles ML (Python, visualisations)  
  https://github.com/ni3ma-fer/AI-model-evaluator

- NO_sql / NoSQL Restaurant Manager — Gestion NoSQL pour une application de restauration (MongoDB, Node.js)  
  https://github.com/ni3ma-fer/NO_sql

> Astuce : ajoute un petit "How to run" et un dataset d’exemple dans chaque repo pour faciliter la prise en main.

---

## 🧩 Exemple rapide d'utilisation

```python
# Exemple : job Spark local pour pré-traitement
from pyspark.sql import SparkSession

spark = SparkSession.builder.appName("preprocess").getOrCreate()
df = spark.read.json("data/input.json")
# ...transformations...
df.write.parquet("data/output")
