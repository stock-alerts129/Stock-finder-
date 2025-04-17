

Sky95/
│
├── backend/
│   ├── main.py
│   ├── requirements.txt
│   └── utils.py (optional - abhi khali hai)
│
├── frontend/
│   ├── index.html
│   ├── style.css
│   └── script.js
│
└── README.md


---

# backend/main.py
from fastapi import FastAPI
from fastapi.middleware.cors import CORSMiddleware

app = FastAPI()

# Allow frontend
app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],
    allow_methods=["*"],
    allow_headers=["*"],
)

@app.get("/scan")
def scan():
    # Dummy stock data (replace with Shoonya API logic later)
    results = [
        {"symbol": "RELIANCE", "signal": "Strong Buy"},
        {"symbol": "TCS", "signal": "Strong Sell"},
        {"symbol": "INFY", "signal": "Watchlist"},
    ]
    return {"stocks": results}

# backend/requirements.txt
fastapi
uvicorn

# backend/utils.py
# Optional helper functions can be added here in the future

<!-- frontend/index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Stock Finder</title>
  <link rel="stylesheet" href="style.css" />
</head>
<body>
  <h1>Live Stock Signals</h1>
  <input type="text" id="search" placeholder="Search stock..." />
  <ul id="stock-list"></ul>
  <script src="script.js"></script>
</body>
</html>

/* frontend/style.css */
body {
  font-family: Arial, sans-serif;
  padding: 20px;
  background: #f3f3f3;
}
h1 {
  color: #333;
}
input {
  margin-bottom: 20px;
  padding: 10px;
  width: 300px;
}
ul {
  list-style: none;
  padding: 0;
}
li {
  background: white;
  margin-bottom: 10px;
  padding: 10px;
  border-radius: 8px;
}

// frontend/script.js
fetch("https://your-backend-url.com/scan")
  .then((res) => res.json())
  .then((data) => {
    const list = document.getElementById("stock-list");
    const search = document.getElementById("search");

    function render(stocks) {
      list.innerHTML = "";
      stocks.forEach((stock) => {
        const li = document.createElement("li");
        li.textContent = `${stock.symbol} - ${stock.signal}`;
        list.appendChild(li);
      });
    }

    render(data.stocks);

    search.addEventListener("input", () => {
      const filtered = data.stocks.filter((s) =>
        s.symbol.toLowerCase().includes(search.value.toLowerCase())
      );
      render(filtered);
    });
  });

# README.md

# Stock Finder (Sky95)

## How to run

### Backend:
- Host using Replit or Render
- Install requirements:

pip install -r requirements.txt

- Run:

uvicorn main:app --reload

### Frontend:
- Host using Netlify
- Build from `frontend/` folder
- Update `script.js` with your live backend URL in place of:
```js
fetch("https://your-backend-url.com/scan")

That’s it! Live scanner ready.
