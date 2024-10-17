# Sistem Rekomendasi Film Movielens

## Project Overview
Proyek ini bertujuan untuk mengembangkan sistem rekomendasi film menggunakan metode Content-Based Filtering. Dengan banyaknya pilihan film yang tersedia, pengguna sering kesulitan dalam menemukan film yang sesuai dengan selera mereka. Oleh karena itu, sistem ini dirancang untuk membantu pengguna mendapatkan rekomendasi film berdasarkan genre yang mereka sukai. Sistem rekomendasi film yang efektif penting untuk meningkatkan pengalaman pengguna dan memaksimalkan kepuasan penonton. Menurut Ricci et al. (2015), sistem rekomendasi yang baik dapat meningkatkan retensi pengguna dan meningkatkan interaksi dengan konten yang relevan. Dengan mengimplementasikan sistem ini, diharapkan pengguna dapat dengan mudah menemukan film baru yang sesuai dengan preferensi mereka, sehingga memperkaya pengalaman menonton mereka.
#### Referensi
1. Zeshan Fayyaz, Mahsa Ebrahimian, Dina Nawara, Ahmed Ibrahim, Rasha Kashef (2020). Recommendation Systems: Algorithms, Challenges, Metrics, and Business Opportunities. *Applied Sciences*, 10(21), 7748. This paper provides an overview of recommendation systems, discussing various types, challenges, and performance metrics used in the field. [Read the paper here](https://doi.org/10.3390/app10217748).

2. Yang Zhao, Xiao Xu, Jilin Chen (2020). Recent Developments in Recommender Systems: A Survey. *arXiv preprint arXiv:2306.12680*. This survey covers the evolution of recommender systems, including collaborative filtering techniques and the impact of deep learning approaches on their performance. [Access the survey here](https://ar5iv.org/html/2306.12680).

3. Adomavicius, G., & Tuzhilin, A. (2005). Toward the Next Generation of Recommender Systems: A Survey of the State-of-the-Art and Possible Extensions. *IEEE Transactions on Knowledge and Data Engineering*, 17(6), 734-749. This foundational paper reviews various methodologies used in recommender systems and discusses their applications and limitations. [Find it here](https://ieeexplore.ieee.org/document/1430350).

## Business Understanding
### Pernyataan Masalah
Pengguna sering kali mengalami kesulitan dalam menemukan film yang sesuai dengan preferensi mereka karena banyaknya pilihan yang tersedia. Tanpa adanya rekomendasi yang relevan, pengguna mungkin melewatkan film yang sesuai dengan selera mereka, sehingga mengurangi kepuasan menonton. Oleh karena itu, diperlukan sebuah sistem yang dapat memberikan rekomendasi film yang tepat berdasarkan preferensi pengguna.

### Tujuan
Tujuan dari proyek ini adalah untuk mengembangkan sistem rekomendasi film yang dapat:
1. Mengidentifikasi genre film yang disukai pengguna berdasarkan film yang telah mereka tonton.
2. Memberikan rekomendasi film yang relevan dan serupa berdasarkan genre favorit pengguna.
3. Meningkatkan pengalaman pengguna dalam menemukan film baru yang sesuai dengan selera mereka.

### Pendekatan Solusi
Untuk mencapai tujuan tersebut, pendekatan solusi yang akan diterapkan adalah:

**Content-Based Filtering**:
   - Metode ini akan menganalisis konten film, khususnya genre, dan merekomendasikan film berdasarkan kesamaan genre dengan film yang telah ditonton pengguna sebelumnya. 
   - Pengguna akan mendapatkan rekomendasi film yang lebih relevan berdasarkan preferensi genre yang mereka sukai.

### Solution Statement
Untuk meraih tujuan di atas, sistem rekomendasi akan:
- Mengumpulkan data historis dari film yang ditonton pengguna untuk memahami pola preferensi mereka.
- Mengimplementasikan algoritma Content-Based Filtering yang dapat menganalisis dan mengkategorikan film berdasarkan genre dan elemen konten lainnya.
- Menggunakan teknik pembelajaran mesin untuk meningkatkan akurasi rekomendasi seiring dengan bertambahnya data pengguna dan interaksi dengan sistem.
- Menyediakan antarmuka pengguna yang intuitif untuk memungkinkan pengguna menavigasi rekomendasi dengan mudah dan memberikan umpan balik yang dapat digunakan untuk meningkatkan kualitas rekomendasi lebih lanjut.


## Data Understanding

### Informasi Dataset
Dataset yang digunakan dalam proyek ini terdiri dari dua file utama:
1. **movies.csv**: Mengandung informasi mengenai film, termasuk ID film, judul, dan genre.
2. **ratings.csv**: Berisi informasi mengenai rating film yang diberikan oleh pengguna, termasuk ID pengguna, ID film, rating, dan timestamp.

Tautan untuk mengunduh dataset:
- [MovieLens Dataset di Kaggle](https://www.kaggle.com/datasets/ayushimishra2809/movielens-dataset/data)

### Jumlah dan Kondisi Data
- **movies.csv**: Terdapat **10,329** data dengan **3 fitur** (movieId, title, genres).
- **ratings.csv**: Terdapat **100,000** data dengan **4 fitur** (userId, movieId, rating, timestamp).

### Pemeriksaan Data
- Dataset **movies.csv** memiliki kolom yang lengkap tanpa nilai yang hilang.
- Dataset **ratings.csv** juga tidak memiliki nilai yang hilang.

### Variabel atau Fitur pada Data
#### movies.csv
- **movieId**: ID unik untuk setiap film.
- **title**: Judul film.
- **genres**: Genre film yang dapat terdiri dari beberapa kategori, dipisahkan oleh tanda `|`.

#### ratings.csv
- **userId**: ID unik untuk setiap pengguna.
- **movieId**: ID film yang dinilai.
- **rating**: Rating yang diberikan pengguna, berkisar dari **0.5** hingga **5.0**.
- **timestamp**: Waktu saat rating diberikan.

### Visualisasi Data dan Insight
#### Distribusi Genre
Untuk memahami distribusi genre film dalam dataset, dilakukan analisis visual:
![download](https://github.com/user-attachments/assets/c07331c3-61af-4c78-aada-c99cd14210c6)
#### Distribusi Ratings
Untuk memahami distribusi ratings film dalam dataset, dilakukan analisis visual:
![download (1)](https://github.com/user-attachments/assets/3cf67c98-39ad-4b95-9161-9e33b4dd952b)

### Analisis Data Eksploratif (EDA)
Beberapa analisis yang dilakukan pada data:
- **Distribusi Rating Pengguna**: Bagaimana pengguna memberikan rating.
- **Film Teratas Berdasarkan Rating**: Film dengan rata-rata rating tertinggi.

Rata-rata rating per film:
```python
# Rata-rata rating per film
avg_rating = all_movie.groupby('title')['rating'].mean().sort_values(ascending=False).head(10)

# Visualisasi film dengan rata-rata rating tertinggi
plt.figure(figsize=(10, 6))
sns.barplot(x=avg_rating.values, y=avg_rating.index, palette='magma')
plt.title('Film Teratas Berdasarkan Rata-rata Rating')
plt.show()
```
![download (2)](https://github.com/user-attachments/assets/4d214d17-4698-413f-be45-33e74ad38afa)

Film yang paling banyak dirating:
```python
# Film dengan jumlah rating terbanyak
most_rated = all_movie['title'].value_counts().head(10)

plt.figure(figsize=(10, 6))
sns.barplot(x=most_rated.values, y=most_rated.index, palette='coolwarm')
plt.title('Film Paling Banyak Dirating')
plt.show()
```
![download (3)](https://github.com/user-attachments/assets/12e5eda4-028e-4ef7-bd04-f8a5bb0f7718)

### Insight
Dari visualisasi distribusi genre, kita dapat mengidentifikasi genre yang paling banyak tersedia dalam dataset, yang dapat membantu dalam memberikan rekomendasi film yang relevan berdasarkan preferensi pengguna. Misalnya, jika pengguna lebih menyukai genre 'Action', sistem dapat merekomendasikan lebih banyak film dari genre tersebut.


## Data Preparation

### Teknik Data Preparation
Dalam proyek ini, beberapa teknik data preparation yang diterapkan meliputi:
1. Menggabungkan dataset **movies.csv** dan **ratings.csv** berdasarkan **movieId**.
2. Menghapus duplikat dan menangani nilai yang hilang (missing values).
3. Menggunakan teknik ekstraksi fitur dengan **TF-IDF** untuk fitur genre, yang merupakan langkah penting dalam membangun model rekomendasi.

### Proses Data Preparation
#### 1. Menggabungkan Dataset
Dataset **movies** dan **ratings** digabungkan menggunakan operasi merge berdasarkan kolom **movieId**. Ini dilakukan agar setiap rating film terhubung dengan informasi filmnya, seperti judul dan genre.

```python
# Menggabungkan dataset movies dan ratings
all_movie = pd.merge(ratings, movies, on='movieId', how='left')
```

#### 2. Menghapus Duplikat dan Menangani Nilai Hilang
Setelah penggabungan, proses selanjutnya adalah menghapus data duplikat dan menangani missing values. Ini penting untuk memastikan bahwa tidak ada data yang redundant yang dapat mengganggu model rekomendasi.

```python
# Menghapus duplikat dan handling missing values
all_movie = all_movie.drop_duplicates('movieId')
all_movie = all_movie.dropna()
```

#### 3. Ekstraksi Fitur dengan TF-IDF
Setelah data bersih, kami menerapkan teknik ekstraksi fitur **TF-IDF** pada kolom genre. Langkah ini sangat penting untuk mengubah data genre menjadi representasi numerik yang dapat digunakan oleh model rekomendasi berbasis konten.

```python
from sklearn.feature_extraction.text import TfidfVectorizer

# Membuat model TF-IDF
tfidf = TfidfVectorizer()
tfidf_matrix = tfidf.fit_transform(all_movie['genres'])
```

### Alasan Data Preparation Diperlukan
Tahapan data preparation sangat penting dalam proses pengembangan sistem rekomendasi karena:
- **Kualitas Data**: Menghilangkan duplikasi dan menangani missing values membantu menjaga kualitas data, yang pada gilirannya akan meningkatkan akurasi model.
- **Keterhubungan Data**: Dengan menggabungkan dataset, kami dapat menganalisis rating bersama dengan informasi film, yang sangat penting untuk rekomendasi yang relevan.
- **Representasi Fitur**: Menggunakan TF-IDF memungkinkan model untuk mengenali pentingnya genre dalam konteks film, meningkatkan kemampuan model dalam memberikan rekomendasi yang sesuai.


## Modeling and Result

### Sistem Rekomendasi
Dalam proyek ini, kami mengembangkan sistem rekomendasi film menggunakan dua pendekatan berbeda: **Content-Based Filtering**, pendekatan ini memiliki kelebihan dan kekurangan masing-masing dalam menyelesaikan permasalahan rekomendasi film.

### Content-Based Filtering
#### Deskripsi
Pendekatan ini menggunakan informasi mengenai film, khususnya fitur genre, untuk merekomendasikan film yang mirip. Kami menggunakan **TfidfVectorizer** untuk menghitung term frequency-inverse document frequency (TF-IDF) dari fitur genre, dan **Cosine Similarity** untuk mengukur kesamaan antar film.

#### Proses Implementasi
```python
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.metrics.pairwise import cosine_similarity

# TF-IDF untuk genre film
tfidf = TfidfVectorizer(stop_words='english')
tfidf_matrix = tfidf.fit_transform(movies['genres'])

# Menghitung cosine similarity
cosine_sim = cosine_similarity(tfidf_matrix)

# Fungsi rekomendasi
def movie_recommendation(movie_title, cosine_sim=cosine_sim):
    idx = movies[movies['title'] == movie_title].index[0]
    sim_scores = list(enumerate(cosine_sim[idx]))
    sim_scores = sorted(sim_scores, key=lambda x: x[1], reverse=True)
    sim_scores = sim_scores[1:6]  # Mengambil 5 rekomendasi teratas
    movie_indices = [i[0] for i in sim_scores]
    return movies['title'].iloc[movie_indices]

# Menyajikan rekomendasi untuk film 'Jumanji (1995)'
recommended_movies = movie_recommendation('Jumanji (1995)')
print("Rekomendasi film untuk 'Jumanji (1995)':")
print(recommended_movies)
```
### Kelebihan dan Kekurangan

#### Kelebihan
- Mampu memberikan rekomendasi berdasarkan preferensi spesifik pengguna.
- Rekomendasi didasarkan pada informasi fitur yang relevan, sehingga lebih transparan.

### Kekurangan
- Mungkin tidak efektif jika film yang direkomendasikan tidak memiliki kesamaan genre yang cukup.
- Tidak mempertimbangkan preferensi pengguna yang lebih luas.


## Evaluasi Model
Untuk menguji sistem, kita bisa menggunakan film terkenal seperti *Jumanji (1995)*, kemudian menghasilkan 5 rekomendasi teratas berdasarkan kesamaan genre.

```python
# Mencari rekomendasi untuk film 'Jumanji (1995)'
recommended_movies = movie_recommendation('Jumanji (1995)')
print("Rekomendasi film untuk 'Jumanji (1995)':")
print(recommended_movies)
```

### Analisis Skor Cosine Similarity
Skor *Cosine Similarity* digunakan untuk mengukur kesamaan antara film input dan film yang direkomendasikan. Skor ini dapat divisualisasikan untuk memahami seberapa mirip film-film yang direkomendasikan.

```python
# Mendapatkan skor similarity
def get_similarities(movie_title, cosine_sim=cosine_sim):
    idx = movies[movies['title'] == movie_title].index[0]
    sim_scores = list(enumerate(cosine_sim[idx]))
    sim_scores = sorted(sim_scores, key=lambda x: x[1], reverse=True)
    sim_scores = sim_scores[1:6]
    return [(movies['title'].iloc[i[0]], i[1]) for i in sim_scores]

similarity_scores = get_similarities('Jumanji (1995)')
```

Visualisasi skor *Cosine Similarity*:
```python
similarity_scores_df = pd.DataFrame(similarity_scores, columns=['Film', 'Cosine Similarity'])
plt.figure(figsize=(10, 6))
sns.barplot(x='Cosine Similarity', y='Film', data=similarity_scores_df, palette='Blues_d')
plt.title('Cosine Similarity dari Rekomendasi Film')
plt.show()
```
![download (4)](https://github.com/user-attachments/assets/f52ed0cc-3503-4f97-a743-b2ec52acc732)




### Visualisasi Distribusi Genre
Untuk membandingkan genre dari film input dan film yang direkomendasikan, distribusi genre dapat divisualisasikan.

```python
def get_genres(movies_list):
    all_genres = []
    for movie in movies_list:
        genres = movies[movies['title'] == movie]['genres'].values[0]
        all_genres.extend(genres.split('|'))
    return all_genres

jumanji_genres = get_genres(['Jumanji (1995)'])
recommended_genres = get_genres(recommended_movies)
```

Visualisasi distribusi genre:
```python
jumanji_genre_counts = pd.Series(jumanji_genres).value_counts()
recommended_genre_counts = pd.Series(recommended_genres).value_counts()

fig, axes = plt.subplots(1, 2, figsize=(14, 7), sharey=True)

sns.barplot(x=jumanji_genre_counts.values, y=jumanji_genre_counts.index, hue=jumanji_genre_counts.index, palette='viridis', ax=axes[0], dodge=False, legend=False)
axes[0].set_title("Distribusi Genre: Jumanji (1995)")

sns.barplot(x=recommended_genre_counts.values, y=recommended_genre_counts.index, hue=recommended_genre_counts.index, palette='coolwarm', ax=axes[1], dodge=False, legend=False)
axes[1].set_title("Distribusi Genre: Film Rekomendasi")

plt.tight_layout(rect=[0, 0, 1, 0.95])
plt

.show()
```
![download (5)](https://github.com/user-attachments/assets/af392716-747b-4b81-b21d-51d85639a0a9)


## Hasil Proyek
Hasil dari proyek ini menunjukkan bahwa model dapat memberikan rekomendasi film yang relevan berdasarkan genre film yang dipilih. Model menunjukkan kesalahan prediksi yang rendah, yang mengindikasikan akurasi dalam memberikan rekomendasi. Sementara itu, Cosine Similarity membantu dalam menentukan seberapa mirip film yang direkomendasikan dengan film yang dipilih pengguna.Diketahui bahwa keseluruhan rekomendasi yang diberikan memiliki genre serupa dengan film yang dicari rekomendasinya. Artinya, presisi sistem yang dibangun sebesar 5/5 atau 100%.

## Kesimpulan
Sistem rekomendasi ini memberikan film berdasarkan kesamaan genre, di mana TF-IDF digunakan untuk menghitung kemunculan genre, dan Cosine Similarity digunakan untuk mengukur kesamaan antara film. Model ini mampu memberikan rekomendasi yang relevan dan bisa membantu pengguna menemukan film baru yang sesuai dengan preferensi mereka.




