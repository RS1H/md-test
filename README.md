# ITNE352-Project-Group-B1

202201419 - Mohammed Alhitar

202201496 - Rayan Alharthy

---

## Project Title
Recipe Discovery System - Client/Server Project

## Project Description
A Python client-server application that allows users to browse food recipes from TheMealDB API. The server fetches reference data once at startup, caches it in memory, and serves multiple clients at the same time using multithreading. Clients can search recipes by name, filter by category, area, or ingredient, get a random recipe, or view reference lists.

## Semester
Semester 2, 2025-2026

## Group
- **Group Name:** B1
- **Course Code:** ITNE352
- **Section:** Network Programming
- **Members:**
  - 202201419 - Mohammed Alhitar
  - 202201496 - Rayan Alharthy

---

## Table of Contents
1. [Requirements](#requirements)
2. [How to Run](#how-to-run)
3. [The Scripts](#the-scripts)
4. [Hybrid Pattern Justification](#hybrid-pattern-justification)
5. [Acknowledgments](#acknowledgments)
6. [Conclusion](#conclusion)
7. [Resources](#resources)

---

## Requirements

### Software
- Python 3.8 or higher
- Internet connection (for TheMealDB API)

### Python Libraries
The project uses standard libraries that come with Python:
- `socket` - for TCP connections
- `json` - for parsing API responses
- `threading` - for handling multiple clients
- `urllib.request` - for HTTP requests to TheMealDB

### Setup Steps
1. Clone the repository:
```
git clone https://github.com/RS1H/ITNE352-Project-Group-B1.git
```
2. Open the folder in VS Code or any editor.
3. No external libraries needed - everything works with Python's standard library.

---

## How to Run

### Step 1: Run the Server
Open a terminal and run:
```
python server.py
```
You will see:
```
Loading reference cache from TheMealDB...
Categories loaded: 14
Areas loaded: 27
Ingredients loaded: 50
Saved to reference_B1.json
Reference cache ready
Server is listening on ('127.0.0.1', 50555) ...
```

### Step 2: Run the Client
Open another terminal (you can open up to 3 clients) and run:
```
python client.py
```
Enter your name when asked, and the main menu will appear.

### Step 3: Use the Menus
- **Main Menu:** Browse Recipes / Reference Lists / Quit
- **Recipes Menu:** Search by name, filter by category/area/ingredient, get a random recipe.
- **Reference Menu:** List all categories, areas, or ingredients.

---

## The Scripts

### server.py
The server script does the following:
- Loads three reference lists (categories, areas, ingredients) from TheMealDB at startup.
- Saves them to `reference_B1.json`.
- Opens a TCP socket on `127.0.0.1:50555` and listens for clients.
- Uses `threading` to handle 3 clients at the same time.
- Receives JSON requests from each client and returns JSON responses.
- Saves every recipe response to a file named `<client_name>_<option>_B1.json`.

**Main functions:**
- `fetch_list(endpoint)` - calls TheMealDB and returns JSON data.
- `load_reference_cache()` - loads and saves the three reference lists.
- `extract_brief(meal)` - extracts ID, name, and thumbnail from a meal.
- `extract_full(meal)` - extracts full details with ingredients and measures.
- `handle_request(conn, client_name, request)` - handles each action from the client.
- `connection_thread(conn, addr)` - runs in a thread for each client.

### client.py
The client script does the following:
- Asks for the user's name.
- Connects to the server using TCP.
- Shows three menus: Main, Recipes, and Reference.
- Validates user input against allowed categories and areas before sending.
- Sends JSON requests to the server and displays the JSON responses.
- Closes the connection when the user chooses Quit.

**Main functions:**
- `send_request(sock, action, value)` - sends a JSON request to the server.
- `receive_response(sock)` - receives and parses a JSON response.
- `display_brief_list(meals)` - shows a numbered list of meals.
- `display_full_details(meal)` - shows full details of one meal.

---

## Hybrid Pattern Justification

The system uses two different data-handling patterns:

**1. Startup Reference Cache**
The categories, areas, and ingredients are loaded once when the server starts. This data does not change often, so caching it saves API calls and makes responses fast.

**2. On-Demand API Fetch**
Recipe data (search, filter, random, lookup) is fetched from TheMealDB whenever a client requests it. Recipe data is too large and too dynamic to cache, so fetching on demand keeps it fresh.

This hybrid approach reduces unnecessary API calls while keeping recipe data current.

---

## Acknowledgments

We would like to thank Dr. Mohammed Almeer for providing the project guidelines, slides, and continuous support throughout the course.

We also acknowledge TheMealDB (https://www.themealdb.com) for providing a free public API used in this project.

---

## Conclusion

This project gave us hands-on experience with TCP sockets, JSON, multithreading, REST APIs, and file I/O in Python. We learned how to design a client-server system, handle multiple clients at the same time, and manage shared resources properly. Working with GitHub also taught us the importance of version control and collaboration in real software projects.

---

## Resources

- [TheMealDB API Documentation](https://www.themealdb.com/api.php)
- [Python Socket Documentation](https://docs.python.org/3/library/socket.html)
- [Python Threading Documentation](https://docs.python.org/3/library/threading.html)
- ITNE352 Course Slides (Ch1 - Ch9)
