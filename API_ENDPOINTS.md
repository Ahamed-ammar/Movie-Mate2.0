# Letterboxd Clone - API Endpoints for Insomnia

Base URL: `http://localhost:5000/api`

---

## 🎬 TMDB Routes (Public - No Auth Required)

### 1. Search Movies/People
**GET** `/tmdb/search`
- **Query Params:**
  - `query` (string) - Search term
  - `type` (string) - 'films' or 'person' or '' (empty for multi)
  - `page` (number) - Page number
- **Example:** `http://localhost:5000/api/tmdb/search?query=inception&type=films&page=1`

### 2. Get Films by Type
**GET** `/tmdb/films`
- **Query Params:**
  - `type` (string) - 'popular', 'top_rated', 'upcoming', 'now_playing'
  - `page` (number) - Page number
- **Example:** `http://localhost:5000/api/tmdb/films?type=popular&page=1`

### 3. Get Home Page Data
**GET** `/tmdb/home_page`
- **No params required**
- **Example:** `http://localhost:5000/api/tmdb/home_page`

### 4. Get Movie Details
**GET** `/tmdb/movie_details`
- **Query Params:**
  - `id` (number) - TMDB movie ID
- **Example:** `http://localhost:5000/api/tmdb/movie_details?id=27205`

### 5. Get Person Details
**GET** `/tmdb/person_details`
- **Query Params:**
  - `id` (number) - TMDB person ID
- **Example:** `http://localhost:5000/api/tmdb/person_details?id=6193`

### 6. Get Director for Movie
**GET** `/tmdb/get_director/:id`
- **URL Params:**
  - `id` (number) - TMDB movie ID
- **Example:** `http://localhost:5000/api/tmdb/get_director/27205`

---

## 👤 User Routes

### 1. Register User
**POST** `/users/register`
- **Body (JSON):**
```json
{
  "username": "testuser",
  "email": "test@example.com",
  "password": "password123"
}
```

### 2. Login User
**POST** `/users/auth`
- **Body (JSON):**
```json
{
  "email": "test@example.com",
  "password": "password123"
}
```
- **Response:** Returns JWT token

### 3. Check Token Validity
**GET** `/users/check_token`
- **Headers:**
  - `Authorization: Bearer <token>`
- **Protected Route** ✅

### 4. Delete Profile
**DELETE** `/users/delete_profile`
- **Headers:**
  - `Authorization: Bearer <token>`
- **Protected Route** ✅

---

## 📝 Profile Routes

### Movie Management

#### 1. Add Movie to Profile
**POST** `/profile/add_movie_to_profile/:field`
- **URL Params:**
  - `field` - 'watched', 'watchlist', 'likes'
- **Headers:**
  - `Authorization: Bearer <token>`
- **Body (JSON):**
```json
{
  "movie_id": 27205,
  "title": "Inception",
  "poster_path": "/path.jpg",
  "release_date": "2010-07-16"
}
```
- **Protected Route** ✅

#### 2. Remove Movie from Profile
**DELETE** `/profile/remove_movie_from_profile/:field`
- **URL Params:**
  - `field` - 'watched', 'watchlist', 'likes'
- **Headers:**
  - `Authorization: Bearer <token>`
- **Query Params:**
  - `movie_id` (number)
- **Protected Route** ✅

#### 3. Get Movie Status
**GET** `/profile/movie_status`
- **Headers:**
  - `Authorization: Bearer <token>`
- **Query Params:**
  - `movie_id` (number)
- **Protected Route** ✅

### List Management

#### 4. Create List
**POST** `/profile/create_list`
- **Headers:**
  - `Authorization: Bearer <token>`
- **Body (JSON):**
```json
{
  "list_name": "My Favorite Movies",
  "description": "A collection of my all-time favorites",
  "ranked": true,
  "list_items": []
}
```
- **Protected Route** ✅

#### 5. Get List Data
**GET** `/profile/get_list_data/:id`
- **URL Params:**
  - `id` - List ID
- **Example:** `http://localhost:5000/api/profile/get_list_data/67cb3336ec0afa0e72d98942`

#### 6. Update List Data
**PUT** `/profile/update_list_data/:id`
- **URL Params:**
  - `id` - List ID
- **Headers:**
  - `Authorization: Bearer <token>`
- **Body (JSON):**
```json
{
  "list_name": "Updated Name",
  "description": "Updated description",
  "ranked": false
}
```
- **Protected Route** ✅

#### 7. Delete List
**DELETE** `/profile/delete_list/:id`
- **URL Params:**
  - `id` - List ID
- **Headers:**
  - `Authorization: Bearer <token>`
- **Protected Route** ✅

#### 8. Add Movies to Lists
**POST** `/profile/add_movies_to_lists`
- **Headers:**
  - `Authorization: Bearer <token>`
- **Body (JSON):**
```json
{
  "movie_id": 27205,
  "list_ids": ["list_id_1", "list_id_2"]
}
```
- **Protected Route** ✅

#### 9. Remove Movie from List
**DELETE** `/profile/remove_movie_from_list`
- **Headers:**
  - `Authorization: Bearer <token>`
- **Query Params:**
  - `list_id` (string)
  - `movie_id` (number)
- **Protected Route** ✅

### Diary Management

#### 10. Add Diary Entry
**POST** `/profile/add_diary_entry`
- **Headers:**
  - `Authorization: Bearer <token>`
- **Body (JSON):**
```json
{
  "movie_id": 27205,
  "watched_date": "2024-01-15",
  "rating": 5,
  "review": "Amazing movie!"
}
```
- **Protected Route** ✅

#### 11. Update Diary Entry
**PUT** `/profile/update_diary_entry/:entry_id`
- **URL Params:**
  - `entry_id` - Diary entry ID
- **Headers:**
  - `Authorization: Bearer <token>`
- **Body (JSON):**
```json
{
  "watched_date": "2024-01-16",
  "rating": 4.5
}
```
- **Protected Route** ✅

#### 12. Delete Diary Entry
**DELETE** `/profile/delete_diary_entry/:entry_id`
- **URL Params:**
  - `entry_id` - Diary entry ID
- **Headers:**
  - `Authorization: Bearer <token>`
- **Protected Route** ✅

#### 13. Get Diary Data
**GET** `/profile/get_diary_data`
- **Headers:**
  - `Authorization: Bearer <token>`
- **Protected Route** ✅

### Review Management

#### 14. Create Review
**POST** `/profile/create_review`
- **Headers:**
  - `Authorization: Bearer <token>`
- **Body (JSON):**
```json
{
  "movie_id": 27205,
  "title": "Inception",
  "poster_path": "/path.jpg",
  "release_date": "2010-07-16",
  "rating": 5,
  "review_text": "Mind-bending masterpiece!",
  "contains_spoilers": false,
  "watched_date": "2024-01-15"
}
```
- **Protected Route** ✅

#### 15. Update Review
**PUT** `/profile/update_review/:id`
- **URL Params:**
  - `id` - Review ID
- **Headers:**
  - `Authorization: Bearer <token>`
- **Body (JSON):**
```json
{
  "rating": 4.5,
  "review_text": "Updated review text"
}
```
- **Protected Route** ✅

#### 16. Delete Review
**DELETE** `/profile/delete_review/:id`
- **URL Params:**
  - `id` - Review ID
- **Headers:**
  - `Authorization: Bearer <token>`
- **Protected Route** ✅

#### 17. Get Reviews by Username
**GET** `/profile/get_reviews/:username`
- **URL Params:**
  - `username` - User's username
- **Example:** `http://localhost:5000/api/profile/get_reviews/testuser`

#### 18. Get Single Review
**GET** `/profile/get_review/:id`
- **URL Params:**
  - `id` - Review ID
- **Example:** `http://localhost:5000/api/profile/get_review/67cb27d8c25238a0f6ee09c1`

### Profile Data

#### 19. Get Profile Data
**GET** `/profile/get_profile_data/:username`
- **URL Params:**
  - `username` - User's username
- **Example:** `http://localhost:5000/api/profile/get_profile_data/testuser`

#### 20. Get Profile Sub Data
**GET** `/profile/get_profile_sub_data/:username/:category`
- **URL Params:**
  - `username` - User's username
  - `category` - 'films', 'diary', 'reviews', 'lists', 'likes', 'watchlist'
- **Example:** `http://localhost:5000/api/profile/get_profile_sub_data/testuser/films`

#### 21. Update Profile
**PUT** `/profile/update_profile`
- **Headers:**
  - `Authorization: Bearer <token>`
- **Body (JSON):**
```json
{
  "username": "newusername",
  "bio": "Updated bio"
}
```
- **Protected Route** ✅

### Favorite Films

#### 22. Add Favorite Film
**POST** `/profile/add_favorite_film`
- **Headers:**
  - `Authorization: Bearer <token>`
- **Body (JSON):**
```json
{
  "movie_id": 27205,
  "title": "Inception",
  "poster_path": "/path.jpg"
}
```
- **Protected Route** ✅

#### 23. Delete Favorite Film
**DELETE** `/profile/delete_favorite_film/:id`
- **URL Params:**
  - `id` - Movie ID
- **Headers:**
  - `Authorization: Bearer <token>`
- **Protected Route** ✅

#### 24. Update Favorite Films Order
**PUT** `/profile/update_favorite_films`
- **Headers:**
  - `Authorization: Bearer <token>`
- **Body (JSON):**
```json
{
  "favorite_films": [27205, 550, 13]
}
```
- **Protected Route** ✅

#### 25. Get Pre-Display Data
**POST** `/profile/get_pre_display_data`
- **Headers:**
  - `Authorization: Bearer <token>`
- **Body (JSON):**
```json
{
  "movie_ids": [27205, 550, 13]
}
```
- **Protected Route** ✅

---

## 🔐 Authentication Notes

For **Protected Routes** (marked with ✅):
1. First, register or login to get a JWT token
2. Add the token to your request headers:
   - **Header Name:** `Authorization`
   - **Header Value:** `Bearer <your_token_here>`

### Example Insomnia Setup:
1. Create a request to `/users/auth` (login)
2. Copy the token from the response
3. In Insomnia, go to the Auth tab → Select "Bearer Token"
4. Paste your token
5. Or manually add header: `Authorization: Bearer eyJhbGc...`

---

## 📊 Quick Test Endpoints (No Auth)

These are great for testing without authentication:

1. **Home Page Data:** `GET http://localhost:5000/api/tmdb/home_page`
2. **Search Inception:** `GET http://localhost:5000/api/tmdb/search?query=inception&type=films&page=1`
3. **Popular Movies:** `GET http://localhost:5000/api/tmdb/films?type=popular&page=1`
4. **Movie Details (Inception):** `GET http://localhost:5000/api/tmdb/movie_details?id=27205`

---

## 🎯 Common Movie IDs for Testing

- Inception: `27205`
- The Dark Knight: `155`
- Interstellar: `157336`
- The Matrix: `603`
- Pulp Fiction: `680`

---

## 💡 Tips for Insomnia

1. Create an **Environment** with:
   - `base_url`: `http://localhost:5000/api`
   - `token`: `<your_jwt_token>`

2. Use environment variables in requests:
   - URL: `{{ _.base_url }}/tmdb/home_page`
   - Header: `Bearer {{ _.token }}`

3. Create a **Folder Structure**:
   - TMDB Routes
   - User Routes
   - Profile Routes
   - Lists
   - Reviews
   - Diary
