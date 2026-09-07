# 🎬 Movie Recommendation System

A **content-based movie recommendation system** that recommends movies similar to a user-selected movie using movie metadata, NLP-based feature engineering, text vectorization, and cosine similarity.

The project demonstrates an end-to-end workflow covering **data preprocessing, NLP, recommendation logic, serialization, web application development, version control, and cloud deployment**.
---

## 🌐 Live Demo

🚀 **Live Application:**
https://movies-recommendation-system-h40h.onrender.com/
---

## 🎯 Problem Statement

With thousands of movies available across different platforms, users can find it difficult to discover movies that match their interests.

The objective of this project is to build a recommendation system that:

* Accepts a movie selected by the user.
* Analyzes its content and metadata.
* Identifies movies with similar characteristics.
* Ranks movies based on similarity.
* Displays recommendations through an interactive web application.

The system uses **content-based filtering**, meaning recommendations are generated from movie characteristics rather than user ratings or collaborative user behavior.

---

## 🏗️ Technical Architecture

```text
                    ┌─────────────────────┐
                    │   Kaggle Dataset    │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │ Data Exploration &  │
                    │      Cleaning       │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │ Feature Engineering │
                    │    & Extraction     │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │ NLP Preprocessing   │
                    │ Stop Words/Stemming │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │   CountVectorizer   │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │  Cosine Similarity  │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │ Recommendation      │
                    │      Engine         │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │ Joblib Serialization│
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │  Streamlit Web App  │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │ Render Deployment   │
                    └─────────────────────┘
```

---

## 🛠️ Tech Stack

| Category         | Technologies |
| ---------------- | ------------ |
| Programming      | Python       |
| Data Processing  | Pandas       |
| Machine Learning | Scikit-learn |
| NLP              | NLTK         |
| Serialization    | Joblib       |
| Web Application  | Streamlit    |
| Version Control  | Git, GitHub  |
| Deployment       | Render       |

---

## 📊 Dataset

The movie dataset was obtained from **Kaggle**.
The dataset was explored to identify movie attributes that could contribute to content-based recommendations.
Relevant information was extracted, cleaned, transformed, and combined into a unified textual representation for each movie.

---

## 🧹 Data Preprocessing

The preprocessing pipeline includes:

* Dataset exploration and validation.
* Selection of relevant movie attributes.
* Conversion of string representations into Python lists using `ast.literal_eval`.
* Extraction of year information from date fields.
* Conversion of movie overview text into token lists.
* Removal of unnecessary spaces from selected text fields.
* Combination of relevant attributes into a single `tags` feature.
* Removal of unnecessary columns.

---

## 🧠 Feature Engineering & NLP

Relevant movie attributes are combined to create a textual representation of each movie.

The NLP pipeline follows:

```text
Movie Metadata
      ↓
Text Cleaning
      ↓
Lowercase Conversion
      ↓
Stop Word Removal
      ↓
Stemming
      ↓
Feature Combination
      ↓
Vectorization
```

### Stemming

The **Porter Stemmer** from NLTK is used to reduce words to their root forms.

```python
from nltk.stem.porter import PorterStemmer
ps = PorterStemmer()
```

The processed feature lists are converted into strings using `.join()` before vectorization.
---

## 🔢 Recommendation Approach

The system follows a **content-based filtering** approach.

### 1. Create Movie Features

Relevant movie metadata is combined into a `tags` column.

### 2. Convert Text into Vectors

`CountVectorizer` converts the textual movie features into numerical vectors.

```python
from sklearn.feature_extraction.text import CountVectorizer

cv = CountVectorizer()

vectors = cv.fit_transform(data["tags"])
vectors = vectors.toarray()
```

### 3. Calculate Similarity

Cosine similarity is calculated between the movie vectors.

```python
from sklearn.metrics.pairwise import cosine_similarity

similarity = cosine_similarity(vectors)
```

### 4. Generate Recommendations

For a selected movie, the recommendation process is:

```text
Selected Movie
      ↓
Find Movie Index
      ↓
Retrieve Similarity Scores
      ↓
Rank Movies
      ↓
Select Top Similar Movies
      ↓
Display Recommendations
```

---
## 💾 Model/Data Serialization

The precomputed similarity matrix is serialized using **Joblib**.

```python
import joblib

joblib.dump(similarity, "similarity.joblib", compress=3)
```

Serialization allows the Streamlit application to load the precomputed similarity data instead of recalculating the complete similarity matrix whenever the application starts.

### Offline vs Online Workflow

#### 🔧 Offline / Model Building

```text
Dataset
   ↓
Preprocessing
   ↓
Feature Engineering
   ↓
Vectorization
   ↓
Similarity Calculation
   ↓
similarity.joblib
```

#### 🌐 Online / Application

```text
User Selects Movie
   ↓
Load Serialized Data
   ↓
Retrieve Similarity Scores
   ↓
Rank Recommendations
   ↓
Display Results
```

---

## 🖥️ Streamlit Application

The recommendation engine is integrated into an interactive **Streamlit web application**.

Users can:

1. Select a movie.
2. Submit their selection.
3. Retrieve similar movies.
4. View generated recommendations through the web interface.

The Streamlit application serves as the user-facing layer of the recommendation engine.

---

### 4. Install Dependencies

```bash
pip install -r requirements.txt
```

### 5. Run the Application
bash
streamlit run app.py
```
The application will start locally and can be accessed through the URL displayed by Streamlit.
---

## ☁️ Deployment

The application was deployed using **Render**.

Deployment workflow:

```text
GitHub Repository
       ↓
Render
       ↓
Install Dependencies
       ↓
Start Streamlit Application
       ↓
Public Web Application
```

### 🚀 Live Application

https://movies-recommendation-system-h40h.onrender.com/

---

## 📈 Results & Performance

The system successfully generates movie recommendations based on content similarity.

The recommendation process:

* Retrieves similarity scores for the selected movie.
* Ranks movies according to similarity.
* Selects the highest-ranked recommendations.
* Serves the recommendations through the deployed web application.

### Evaluation Metrics

Traditional classification metrics such as **accuracy, precision, and recall** are not directly applicable to this recommendation system unless an appropriate labeled evaluation dataset is defined.

For future evaluation, recommendation-specific metrics such as:
* **Precision@K**
* **Recall@K**
* **NDCG@K**

can be used to measure recommendation quality.
> No fabricated accuracy or performance numbers are included.
---

## ⚠️ Limitations

The current implementation has several limitations:

* Recommendations depend heavily on the quality and completeness of movie metadata.
* The system does not currently model individual user preferences.
* User ratings and historical viewing behavior are not used.
* New movies with limited metadata may receive weaker recommendations.
* `CountVectorizer` primarily captures word occurrence and does not understand deeper semantic relationships.
* A full similarity matrix can become memory-intensive as the dataset grows.

---

## 🚀 Future Improvements

Potential improvements include:

* Replace `CountVectorizer` with **TF-IDF**.
* Use transformer-based embeddings for semantic similarity.
* Implement **Sentence Transformers** for richer text representations.
* Introduce collaborative filtering using user interaction data.
* Develop a hybrid recommendation system combining content-based and collaborative approaches.
* Integrate movie posters and additional metadata through an API.
* Improve ranking using multiple recommendation signals.
* Add automated unit and integration tests.
* Containerize the application using Docker.
* Implement CI/CD using GitHub Actions.
* Add logging and monitoring for the deployed application.
* Optimize similarity search for larger datasets.

---

## 💡 Why This Project?

This project demonstrates the complete journey from **raw data to a deployed machine learning application**.
Rather than stopping at exploratory data analysis or model experimentation, the project covers:

```text
Data
 ↓
Preprocessing
 ↓
Feature Engineering
 ↓
NLP
 ↓
Machine Learning Technique
 ↓
Serialization
 ↓
Application Development
 ↓
Deployment
```

This demonstrates practical understanding of how a machine-learning-based solution can be transformed into a usable application.
---

## 🧰 Key Skills Demonstrated

### Programming & Data

* Python
* Pandas
* Data Cleaning
* Data Transformation

### Machine Learning

* Feature Engineering
* Vectorization
* Cosine Similarity
* Recommendation Systems
* Content-Based Filtering

### NLP

* Text Preprocessing
* Stop Word Removal
* Stemming
* NLTK

### Application Development

* Streamlit
* Model/Data Serialization
* Interactive User Interface

### Software Engineering & Deployment

* Git
* GitHub
* Dependency Management
* Cloud Deployment
* Render

---

## 📌 Project Highlights

* Built an end-to-end **content-based movie recommendation system**.
* Applied **NLP and feature engineering** to movie metadata.
* Converted textual features into numerical representations using **CountVectorizer**.
* Implemented **cosine similarity** for movie ranking.
* Serialized precomputed recommendation data using **Joblib**.
* Developed an interactive **Streamlit web application**.
* Deployed the application using **Render**.
* Used **Git/GitHub** for source-code management.

---

## 👨‍💻 Author

**Bhagwati Ahirwar**

If you found this project useful, feel free to explore the repository and connect with me.
