# 🏠 Lowe's & Home Depot Marketplace Monitoring System

A comprehensive marketplace monitoring system that enables users to search, compare, and track products from Lowe's and Home Depot stores. The system uses advanced web scraping techniques to gather real-time product data based on location, search radius, and keywords.

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Python](https://img.shields.io/badge/python-3.8%2B-blue)
![Next.js](https://img.shields.io/badge/next.js-14.2.4-black)
![FastAPI](https://img.shields.io/badge/FastAPI-latest-green)

## 📋 Table of Contents

- [Features](#features)
- [Tech Stack](#tech-stack)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [API Documentation](#api-documentation)
- [Contributing](#contributing)
- [License](#license)

## ✨ Features

- 🔍 **Smart Product Search**: Search products by postal code, range, and keywords
- 🏪 **Multi-Store Support**: Compare prices and availability across Lowe's and Home Depot
- 📍 **Location-Based Search**: Find products in stores within a specified radius
- 🔐 **User Authentication**: Secure JWT-based authentication system
- 📊 **Data Export**: Export search results to CSV/Excel formats
- 📱 **Responsive Design**: Modern, mobile-friendly interface
- ⚡ **Real-Time Scraping**: Live data extraction using Selenium and BeautifulSoup
- 🗺️ **Google Maps Integration**: Accurate store location and distance calculation

## 🛠️ Tech Stack

### Backend
- **Framework**: FastAPI
- **Database**: PostgreSQL with SQLModel ORM
- **Authentication**: JWT (JSON Web Tokens)
- **Web Scraping**: 
  - Selenium WebDriver
  - BeautifulSoup4
- **Data Processing**: Pandas
- **API Integration**: Google Maps API

### Frontend
- **Framework**: Next.js 14 (React 18)
- **Language**: TypeScript
- **Styling**: TailwindCSS
- **HTTP Client**: Axios
- **Icons**: Heroicons
- **Export**: jsPDF, XLSX

## 📦 Prerequisites

Before you begin, ensure you have the following installed:

- **Python** 3.8 or higher
- **Node.js** 16.x or higher
- **PostgreSQL** 12 or higher
- **npm** or **yarn**
- **Google Chrome** (for Selenium WebDriver)
- **ChromeDriver** (matching your Chrome version)

## 🚀 Installation

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/lowes-homedepot-compare.git
cd lowes-homedepot-compare
```

### 2. Backend Setup

```bash
# Navigate to backend directory
cd backend

# Create virtual environment
python -m venv venv

# Activate virtual environment
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

### 3. Frontend Setup

```bash
# Navigate to frontend directory
cd frontend

# Install dependencies
npm install
# or
yarn install
```

### 4. Database Setup

```bash
# Create PostgreSQL database
createdb marketplace_monitoring

# The application will automatically create tables on first run
```

## ⚙️ Configuration

### Backend Environment Variables

Create a `.env` file in the `backend` directory:

```env
# Database Configuration
POSTGRES_USER=your_db_user
POSTGRES_PASSWORD=your_db_password
POSTGRES_SERVER=localhost
POSTGRES_PORT=5432
POSTGRES_DB=marketplace_monitoring

# JWT Configuration
SECRET_KEY=your-secret-key-here
ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=11520

# Google Maps API (Optional)
GOOGLE_MAPS_API_KEY=your_google_maps_api_key

# API Configuration
API_PREFIX=/api/v1
```

### Frontend Environment Variables

Create a `.env.local` file in the `frontend` directory:

```env
NEXT_PUBLIC_API_URL=http://localhost:8000/api/v1
```

## 🎯 Usage

### Starting the Backend Server

```bash
cd backend
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

The API will be available at `http://localhost:8000`
- API Documentation: `http://localhost:8000/docs`
- Alternative Docs: `http://localhost:8000/redoc`

### Starting the Frontend Development Server

```bash
cd frontend
npm run dev
# or
yarn dev
```

The application will be available at `http://localhost:3000`

### Building for Production

#### Backend
```bash
cd backend
uvicorn app.main:app --host 0.0.0.0 --port 8000
```

#### Frontend
```bash
cd frontend
npm run build
npm start
# or
yarn build
yarn start
```

## 📁 Project Structure

```
Lowes_Homedepot_Compare/
├── backend/
│   ├── app/
│   │   ├── api/
│   │   │   └── api_v1/
│   │   │       └── routes/
│   │   │           ├── products.py      # Product search endpoints
│   │   │           └── users.py         # User authentication endpoints
│   │   ├── core/
│   │   │   └── security.py              # JWT & password hashing
│   │   ├── crud/
│   │   │   ├── product.py               # Product database operations
│   │   │   └── user.py                  # User database operations
│   │   ├── models/
│   │   │   ├── product.py               # Product data models
│   │   │   └── user.py                  # User data models
│   │   ├── scrapers/
│   │   │   ├── home_depot_scraper.py    # Home Depot scraping logic
│   │   │   ├── lowes_scraper.py         # Lowe's scraping logic
│   │   │   └── google_map_api.py        # Store location services
│   │   ├── db.py                        # Database connection
│   │   ├── main.py                      # FastAPI application
│   │   ├── settings.py                  # Configuration settings
│   │   └── utils.py                     # Utility functions
│   └── requirements.txt
├── frontend/
│   ├── src/
│   │   ├── app/
│   │   │   ├── auth/
│   │   │   │   ├── login/               # Login page
│   │   │   │   └── register/            # Registration page
│   │   │   ├── dashboard/               # Main dashboard
│   │   │   └── page.tsx                 # Home page
│   │   ├── components/
│   │   │   ├── Dashboard/               # Dashboard components
│   │   │   ├── common/                  # Reusable components
│   │   │   └── Header.tsx               # Navigation header
│   │   ├── hooks/
│   │   │   ├── useAuth.ts               # Authentication hook
│   │   │   └── useData.ts               # Data fetching hook
│   │   └── context/
│   │       └── NotificationContext.tsx  # Toast notifications
│   ├── package.json
│   └── tailwind.config.ts
├── keywords.csv                          # Sample keywords file
└── README.md
```

## 📡 API Documentation

### Authentication Endpoints

#### Register User
```http
POST /api/v1/users/register
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "securepassword",
  "full_name": "John Doe"
}
```

#### Login
```http
POST /api/v1/users/login
Content-Type: application/x-www-form-urlencoded

username=user@example.com&password=securepassword
```

### Product Endpoints

#### Search Products
```http
POST /api/v1/products/search
Authorization: Bearer <token>
Content-Type: application/json

{
  "postal_code": "90210",
  "radius": 25,
  "keywords": ["hammer", "drill"],
  "stores": ["lowes", "homedepot"]
}
```

#### Get Product History
```http
GET /api/v1/products/history?user_id=1&limit=10
Authorization: Bearer <token>
```

## 🔍 How It Works

1. **User Authentication**: Users register and log in to access the platform
2. **Location Input**: Users enter a postal code and search radius
3. **Keyword Search**: Users provide product keywords to search for
4. **Store Selection**: Users select which stores to search (Lowe's, Home Depot, or both)
5. **Data Scraping**: The system uses Selenium and BeautifulSoup to scrape product data
6. **Location Matching**: Google Maps API calculates store distances and filters by radius
7. **Results Display**: Products are displayed in a sortable, filterable table
8. **Data Export**: Results can be exported to CSV or Excel formats

## 🔐 Security Features

- Password hashing using bcrypt
- JWT-based authentication
- Secure token storage
- CORS configuration for API security
- Environment-based configuration

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 Development Guidelines

- Follow PEP 8 style guide for Python code
- Use TypeScript strict mode for frontend development
- Write meaningful commit messages
- Add comments for complex logic
- Test your changes before submitting PR

## 🐛 Known Issues & Limitations

- Web scraping may be affected by website structure changes
- Rate limiting may apply for frequent scraping requests
- ChromeDriver must match your Chrome browser version
- Some products may not be available in all locations

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👥 Authors

- Your Name - Initial work

## 🙏 Acknowledgments

- FastAPI for the excellent web framework
- Next.js team for the React framework
- Selenium and BeautifulSoup for web scraping capabilities
- TailwindCSS for the utility-first CSS framework

## 📞 Support

For support, email muhammadazlan@azlan.tech or open an issue in the repository.

## 🔄 Changelog

### Version 0.1.0 (Current)
- Initial release
- Basic product search functionality
- User authentication system
- Lowe's and Home Depot scrapers
- Location-based filtering
- Data export features

---

**⭐ If you find this project useful, please consider giving it a star!**
