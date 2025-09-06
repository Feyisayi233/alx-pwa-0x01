# MoviesDatabase API – Developer Documentation

## API Overview
The **MoviesDatabase API** provides complete and updated data for over **9 million titles**, including movies, series, and episodes.  

- **Weekly updates** for new titles  
- **Daily updates** for ratings and episode information  
- Rich metadata covering titles, ratings, actors, episodes, and more  
- Flexible query parameters for filtering, sorting, and customizing responses  

This API is ideal for building movie apps, TV trackers, recommendation engines, or media-based projects.

---

## Version
**v1** – latest public release.

---

## Available Endpoints

### Titles
- **`/titles`** – Returns an array of titles based on filters and sorting options.  
- **`/x/titles-by-ids`** – Fetch multiple titles by IMDb IDs.  
- **`/titles/{id}`** – Fetch a single title by IMDb ID.  
- **`/titles/{id}/ratings`** – Get rating and votes for a title.  
- **`/titles/series/{id}`** – Returns all episodes (IDs, season, and episode numbers).  
- **`/titles/seasons/{id}`** – Returns the number of seasons for a series.  
- **`/titles/series/{id}/{season}`** – Get episodes for a specific season.  
- **`/titles/episode/{id}`** – Fetch details for a specific episode.  
- **`/titles/x/upcoming`** – Upcoming movies and series.  

### Search
- **`/titles/search/keyword/{keyword}`** – Search titles by keyword.  
- **`/titles/search/title/{title}`** – Search by exact or partial title.  
- **`/titles/search/akas/{aka}`** – Search by alternative/aka titles.  

### Actors
- **`/actors`** – List actors with pagination.  
- **`/actors/{id}`** – Fetch detailed actor information.  

### Utils
- **`/title/utils/titleType`** – Get available title types.  
- **`/title/utils/genres`** – Get all genres.  
- **`/title/utils/lists`** – Get predefined title lists (e.g., top rated, most popular).  

---

## Request and Response Format

### Base URL
```

[https://moviesdatabase.example.com/](https://moviesdatabase.example.com/)

````

### Example Request
```http
GET /titles/tt0000270?info=base_info
````

### Example Response

```json
{
  "id": "tt0000270",
  "titleText": "Example Movie",
  "releaseDate": "2023-10-01",
  "genres": ["Drama"],
  "ratingsSummary": { "averageRating": 7.2, "numVotes": 1234 }
}
```

### Notes

* Every response contains a `results` key.
* Paginated endpoints also include: `page`, `next`, and `entries`.

---

## Authentication

The MoviesDatabase API may be used publicly, but some implementations require authentication:

* API Key (`?api_key=YOUR_KEY`)
* Or Bearer Token (`Authorization: Bearer <token>`)

Check your provider’s setup for specific authentication details.

---

## Error Handling

Typical error responses look like this:

```json
{
  "error": "Invalid ID",
  "status": 404
}
```

* **400** – Invalid request (wrong params).
* **401** – Unauthorized (missing/invalid credentials).
* **404** – Not found (invalid IMDb ID).
* **500** – Server error.

---

## Usage Limits and Best Practices

* Maximum **50 results per page**.
* Use **pagination** (`limit`, `page`) to handle large result sets.
* Use the `info` query parameter (`mini_info`, `base_info`) to reduce payload size.
* Cache frequent requests (e.g., genres, title types).
* Store credentials (API keys) in **environment variables**.
* Validate IMDb IDs before making calls.

---

## Example Query Parameters

* **`limit`** – Number of results (default: 10, max: 50).
* **`page`** – Page number (default: 1).
* **`titleType`** – Filter by type (movie, series, etc.).
* **`genre`** – Filter by genre (case-sensitive, e.g., `Drama`).
* **`year`**, `startYear`, `endYear` – Filter by release year or range.
* **`sort`** – Sort results (`year.incr`, `year.decr`).
* **`list`** – Predefined collections (`most_pop_movies`, `top_rated_250`).

---

## Example Models

### Rating

```json
{
  "tconst": "tt0000003",
  "averageRating": 6.5,
  "numVotes": 1631
}
```

### Light Episode

```json
{
  "tconst": "tt0020666",
  "parentTconst": "tt15180956",
  "seasonNumber": 1,
  "episodeNumber": 2
}
```

### Actor

```json
{
  "nconst": "nm0000001",
  "primaryName": "Fred Astaire",
  "birthYear": 1899,
  "deathYear": 1987,
  "primaryProfession": "soundtrack,actor,miscellaneous",
  "knownForTitles": "tt0050419,tt0053137"
}
```

---



```

---

