# 🛒 Supermarket Shopping Advisor

A full-stack intelligent shopping platform that helps users compare supermarket prices, track budgets, predict spending, and plan first-month setup costs in the UK.

![Status](https://img.shields.io/badge/Status-In%20Development-yellow)
![Java](https://img.shields.io/badge/Java-Spring%20Boot-green)
![Angular](https://img.shields.io/badge/Frontend-Angular-red)
![Python](https://img.shields.io/badge/Data-Python-blue)
![PostgreSQL](https://img.shields.io/badge/Database-PostgreSQL-blue)

---

## 📌 Overview

The Supermarket Shopping Advisor is a data-driven web application that aggregates real-time pricing data from seven major UK supermarkets, applies machine learning models to predict prices and forecast spending, and provides personalised shopping recommendations.

A key feature is the **Migration Budgeting Module** — a dedicated tool that helps new UK residents plan and track their first-month essential setup costs, comparing prices across supermarkets and retailers to maximise savings.

---

## ✨ Features

### Core Features
- **Price Comparison** — Live price data across Tesco, Asda, Lidl, Sainsbury's, Morrisons, Waitrose, and Co-op
- **Budget Management** — Set weekly/monthly budgets and track spending in real time
- **Sales Intelligence** — Aggregates current deals and promotions across all supermarkets
- **Smart Recommendations** — Personalised shopping suggestions based on your list and budget
- **Spending Forecast** — Random Forest model predicts future spending based on history

### Migration Budgeting Module *(Core Feature)*
- First-month setup checklist (winter clothing, school essentials, home setup, household supplies)
- Cost estimates with cheapest retailer recommendations
- Budget progress tracker
- Smart shopping tips to maximise savings

---

## 🏗️ Tech Stack

| Layer | Technology |
|---|---|
| Backend | Java 21, Spring Boot, REST API, Swagger/OpenAPI |
| Frontend | Angular 17, TypeScript |
| Database | PostgreSQL |
| Data Engineering | Python, BeautifulSoup, Scrapy |
| Machine Learning | Python, Scikit-Learn (ARIMA, Random Forest) |
| DevOps | Docker, Docker Compose |

---

## 📁 Project Structure
```
supermarket-shopping-advisor/
├── backend/                    # Java Spring Boot REST API
│   └── src/main/java/com/shopping/
│       ├── controller/         # REST endpoints
│       ├── service/            # Business logic
│       ├── repository/         # Data access layer
│       ├── entity/             # JPA entities
│       ├── dto/                # Data transfer objects
│       └── config/             # Swagger + app config
│
├── frontend/                   # Angular application
│   └── src/app/
│       ├── components/         # UI components
│       ├── services/           # API service layer
│       └── models/             # TypeScript interfaces
│
├── data-engineering/           # Python scrapers & pipelines
│   ├── scrapers/               # One scraper per supermarket
│   ├── scheduler.py            # Runs scrapers daily
│   ├── data_processor.py       # Cleans scraped data
│   └── db_uploader.py          # Saves data to PostgreSQL
│
├── ml-models/                  # Python ML models
│   ├── price_prediction.py     # ARIMA price forecasting
│   ├── spending_forecast.py    # Random Forest spending forecast
│   └── recommendation_engine.py
│
└── database/
    └── schema.sql              # Full PostgreSQL schema (11 tables)
```

---

## 🗄️ Database Schema

The database includes **11 tables**:

**Core Tables**
- `users` — User accounts
- `supermarkets` — Reference data for 7 supermarkets
- `products` — Clean product reference list
- `prices` — Historical and current supermarket prices
- `budgets` — Budget configurations per user
- `shopping_list_items` — User shopping lists
- `spending` — User spending history
- `predictions` — Stored ML prediction results

**Migration Module Tables**
- `migration_setup_costs` — First-month setup cost reference data
- `user_migration_profile` — User immigration profile settings
- `migration_tracking` — Per-user purchase tracking for setup costs

---

## 🔌 API Endpoints

### Budget
| Method | Endpoint | Description |
|---|---|---|
| GET | `/budget/{userId}` | Get user budget |
| POST | `/budget` | Create/update budget |

### Price Comparison
| Method | Endpoint | Description |
|---|---|---|
| GET | `/prices/{item}` | Compare prices across supermarkets |
| GET | `/prices/history/{item}` | Price history for an item |

### Sales
| Method | Endpoint | Description |
|---|---|---|
| GET | `/sales` | Get all current deals |
| GET | `/sales/{supermarket}` | Deals by supermarket |

### Recommendations
| Method | Endpoint | Description |
|---|---|---|
| GET | `/recommendations/{userId}` | Get personalised recommendations |

### Migration Module
| Method | Endpoint | Description |
|---|---|---|
| GET | `/migration/setup-costs` | Get all setup cost estimates |
| GET | `/migration/total-first-month` | Total first-month cost summary |
| POST | `/migration/profile` | Create user migration profile |
| POST | `/migration/track-purchase` | Log a purchase against budget |
| GET | `/migration/progress/{userId}` | Get budget progress |
| GET | `/migration/guidance` | Get shopping tips and resources |

Full API documentation available via **Swagger UI** at `/swagger-ui.html` when running locally.

---

## 🤖 Machine Learning Models

### 1. ARIMA Price Prediction
- Predicts future supermarket prices based on historical data
- Helps users decide the best time to buy

### 2. Random Forest Spending Forecast
- Forecasts a user's monthly spending based on shopping history
- Identifies patterns and flags overspending risk

### 3. Recommendation Engine
- Suggests optimal supermarkets and products based on user list and budget

---

## 🚀 Getting Started

### Prerequisites
- Java 21+
- Node.js 18+ and Angular CLI
- Python 3.10+
- PostgreSQL 14+
- Docker & Docker Compose (optional)

### Run with Docker
```
git clone https://github.com/mounawasiq/supermarket-shopping-advisor.git
cd supermarket-shopping-advisor
docker-compose up --build
```

### Run Manually

**Backend:**
```
cd backend
./mvnw spring-boot:run
```

**Frontend:**
```
cd frontend
npm install
ng serve
```

**Data Engineering:**
```
cd data-engineering
pip install -r requirements.txt
python scheduler.py
```

---

## 📅 Development Roadmap

- [x] Project blueprint and architecture design
- [x] PostgreSQL schema setup (11 tables)
- [x] Java Spring Boot backend skeleton
- [x] Angular frontend skeleton
- [ ] Supermarket scrapers (7 supermarkets)
- [ ] Core API endpoints
- [ ] Migration Budgeting Module (backend + frontend)
- [ ] ARIMA price prediction model
- [ ] Random Forest spending forecast model
- [ ] Recommendation engine
- [ ] Swagger API documentation
- [ ] Docker deployment
- [ ] Full testing and polish

---

## 🛒 Supported Supermarkets

| Supermarket | Scraper Status |
|---|---|
| Tesco | 🔄 In Progress |
| Asda | 🔄 In Progress |
| Lidl | 🔄 In Progress |
| Sainsbury's | 🔄 In Progress |
| Morrisons | 🔄 In Progress |
| Waitrose | 🔄 In Progress |
| Co-op | 🔄 In Progress |

---

## 📄 License

This project is licensed under the MIT License.

---

## 👤 Author

Built as a portfolio project demonstrating full-stack development, data engineering, and machine learning skills.
