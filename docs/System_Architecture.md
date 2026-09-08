# System Architecture & Database Schema

## Relational Entity Schema (SQLite)

### Table: `sessions`
| Column Name | Data Type | Constraint | Description |
| :--- | :--- | :--- | :--- |
| `id` | INTEGER | PRIMARY KEY AUTOINCREMENT | Unique session identifier |
| `username` | TEXT | NOT NULL | User handling the session |
| `avg_gap` | REAL | NOT NULL | Average time delay between keystrokes (ms) |
| `paste_count` | INTEGER | NOT NULL | Number of paste commands executed |
| `typing_speed`| REAL | NOT NULL | Words Per Minute / Characters Per Second |
| `confidence` | REAL | NOT NULL | Logistic probability metric |
| `result` | TEXT | NOT NULL | Final classification tag |
| `timestamp` | TEXT | NOT NULL | ISO-8601 execution time |
