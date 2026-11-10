# Songs: Eight SQL Queries

SQL queries that answer eight questions about `songs.db`, a SQLite database of the 100 most-streamed Spotify songs of 2018. Each query lives in its own file (`1.sql` to `8.sql`).

## 1. List the names of all songs

```sql
-- List the names of all songs
SELECT name
FROM songs;
```

## 2. List the names of all songs in order of tempo, slowest first

```sql
-- List song names from slowest tempo to fastest
SELECT name
FROM songs
ORDER BY tempo ASC;
```

## 3. List the names of the five longest songs, longest first

```sql
-- List the five longest songs, longest first
SELECT name
FROM songs
ORDER BY duration_ms DESC
LIMIT 5;
```

## 4. List the names of songs that are danceable

Danceability, energy and valence all above 0.75.

```sql
-- Songs where danceability, energy and valence are all above 0.75
SELECT name
FROM songs
WHERE danceability > 0.75 AND energy > 0.75 AND valence > 0.75;
```

## 5. Print the average energy of all songs

```sql
-- Average energy of all songs
SELECT AVG(energy)
FROM songs;
```

## 6. List the names of songs by Post Malone

Uses a subquery to find the artist's id first.

```sql
-- Songs by Post Malone (subquery finds his id first)
SELECT name
FROM songs
WHERE artist_id = (
    SELECT id
    FROM artists
    WHERE name = 'Post Malone'
);
```

## 7. Print the average energy of songs by Drake

Uses a JOIN to combine the `songs` and `artists` tables.

```sql
-- Average energy of songs by Drake (JOIN version)
SELECT AVG(energy)
FROM songs
JOIN artists ON songs.artist_id = artists.id
WHERE artists.name = 'Drake';
```

## 8. List the names of songs that feature other artists

Songs that feature other artists have "feat." in the name.

```sql
-- Songs that feature other artists
SELECT name
FROM songs
WHERE name LIKE '%feat.%';
```
