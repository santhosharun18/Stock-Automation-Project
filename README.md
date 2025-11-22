# 📈 Automated Stock Data Pipeline using n8n + MongoDB Atlas

This project is a fully-automated data pipeline that fetches **real-time stock market data**, formats it, and stores it in a **MongoDB Atlas database** using an n8n workflow.

It runs on a schedule and continuously updates a central database with fresh market data.

---

## 🚀 Features

✔ Fetches real-time stock data from TwelveData API  
✔ Cleans & structures API data using a JavaScript function  
✔ Stores each stock record in MongoDB Atlas  
✔ Fully automated schedule trigger  
✔ Modular workflow that can be extended (email alerts, Google Sheets export, analytics, etc.)

---

## 🛠 Tech Stack

- **n8n (open-source automation platform)**
- **MongoDB Atlas**
- **TwelveData API**
- **JavaScript (for data transformation)**

---

## 📂 Workflow Diagram

```
Schedule Trigger → HTTP Request → JavaScript Function → MongoDB Insert
```

---

## 📡 Data Transformation (JS Code)

The Code node converts raw API response into clean JSON ready for DB insert:

```js
return items.map(item => {
	return {
		json: {
			symbol: item.json.symbol,
			name: item.json.name,
			currency: item.json.currency,
			exchange: item.json.exchange,
			open: item.json.open,
			high: item.json.high,
			low: item.json.low,
			close: item.json.close,
			previous_close: item.json.previous_close,
			volume: item.json.volume,
			date: new Date().toISOString()
		}
	};
});
```

---

## 🗄 Database: MongoDB Atlas

Collection used: **stocks**

Each inserted document looks like:

```json
{
  "symbol": "AAPL",
  "name": "Apple Inc.",
  "currency": "USD",
  "exchange": "NASDAQ",
  "open": 265.95,
  "high": 273.32,
  "low": 265.67,
  "close": 271.48,
  "previous_close": 266.25,
  "volume": 58784100,
  "date": "2025-11-22T10:00:00.000Z"
}
```

---

## ⚙️ How to Run the Project

### 1️⃣ Install n8n locally (if needed)
```bash
npm install n8n -g
n8n start
```

Then open:  
👉 `http://localhost:5678`

---

### 2️⃣ Clone this repository
```bash
git clone https://github.com/<your-username>/<repo-name>.git
cd <repo-name>
```

---

### 3️⃣ Import the workflow
In n8n:

```
Menu → Workflows → Import → Select workflow JSON file
```

---

### 4️⃣ Add credentials
You must configure:

#### ✔ TwelveData API (HTTP Request)
Put:
```
https://api.twelvedata.com/quote?symbol=AAPL,MSFT,...
```

#### ✔ MongoDB Atlas
Use your connection string:
```
mongodb+srv://<username>:<password>@cluster0.mongodb.net/?retryWrites=true&w=majority
```
Authentication DB must be:
```
admin
```

---

### 5️⃣ Run the workflow
Click **Execute Workflow**  
Or activate the schedule trigger for auto-run.

---

## 📌 Why This Project Is Valuable

This pipeline demonstrates:

- Real-time API integration  
- Automation design  
- Data cleaning and transformation  
- Cloud database integration  
- Production-ready workflow patterns  

Perfect for **portfolios**, **job applications**, or **data engineering practice**.

---

## 📜 License
MIT License

---

## 🤝 Contributing
Pull requests are welcome!

---

## ⭐ Support
If you like this project, give it a **star** on GitHub!
