# 🤖 Text-to-SQL Agent

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.104+-green.svg)](https://fastapi.tiangolo.com/)
[![LangChain](https://img.shields.io/badge/LangChain-Latest-orange.svg)](https://python.langchain.com/)
[![OpenAI](https://img.shields.io/badge/OpenAI-GPT--4-black.svg)](https://openai.com/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

An intelligent Text-to-SQL application that converts natural language questions into SQL queries using LangChain agents and OpenAI's GPT-4. Ask questions in plain English and get instant database insights, no SQL knowledge required.

## ✨ Features

- **Natural Language Querying**: Ask database questions in plain English
- **Intelligent SQL Generation**: Powered by LangChain's SQL Agent and OpenAI GPT-4
- **Real-Time Query Execution**: Instant results from your PostgreSQL database
- **Query Transparency**: View both the generated SQL and formatted results
- **Elegant UI**: Clean, responsive Bootstrap interface with tabbed output
- **Smart Formatting**: Automatic list formatting for multi-item results
- **Error Handling**: Comprehensive error management with user-friendly messages
- **API Health Monitoring**: Real-time connection status indicator
- **CORS Enabled**: Ready for cross-origin requests

## 📸 Demo Screenshots

### Main Interface
![Main Interface](screenshots/preview1.png)
*Clean and intuitive interface for natural language database queries*

### Query Processing
![Query Processing](screenshots/preview2.png)
*Real-time feedback during query generation and execution*

### SQL Query View
![Generated SQL](screenshots/preview3.png)
*Transparent view of the generated SQL query*

### Results Display
![Results Display](screenshots/preview4.png)
*Elegantly formatted query results with smart list rendering*

### API Status
![API Health](screenshots/preview5.png)
*Live API connection monitoring and status indicators*

## 🛠️ Tech Stack

### Backend
- **FastAPI** - High-performance async web framework
- **LangChain** - Agent framework for LLM applications
- **OpenAI GPT-4o Mini** - LLM for SQL generation
- **SQLAlchemy** - Database toolkit and ORM
- **PostgreSQL** - Production database (via Supabase)
- **Python-dotenv** - Environment variable management

### Frontend
- **HTML5** - Semantic markup
- **CSS3** - Modern styling with custom design
- **Bootstrap 5.3** - Responsive UI framework
- **Font Awesome** - Icon library
- **Vanilla JavaScript** - Client-side logic

### Database
- **Supabase (PostgreSQL)** - Managed PostgreSQL hosting

## 🏗️ Architecture

```
┌─────────────┐         ┌──────────────┐         ┌────────────┐
│   Frontend  │  HTTP   │   FastAPI    │  Agent  │  OpenAI    │
│  (Browser)  ├────────►│   Backend    ├────────►│  GPT-4     │
└─────────────┘         └──────┬───────┘         └────────────┘
                               │
                               │ SQL
                               ▼
                        ┌──────────────┐
                        │  PostgreSQL  │
                        │  (Supabase)  │
                        └──────────────┘
```

**Flow:**
1. User inputs natural language question
2. Frontend sends POST request to `/ask` endpoint
3. LangChain SQL Agent processes the question
4. Agent generates SQL query using GPT-4
5. Query executes against PostgreSQL database
6. Results formatted and returned to frontend
7. UI displays both SQL query and formatted answer

## 📦 Installation

### Prerequisites
- Python 3.8 or higher
- PostgreSQL database (or Supabase account)
- OpenAI API key

### Step 1: Clone the Repository
```bash
git clone https://github.com/yourusername/text-to-sql-agent.git
cd text-to-sql-agent
```

### Step 2: Create Virtual Environment
```bash
# Windows
python -m venv venv
venv\Scripts\activate

# macOS/Linux
python3 -m venv venv
source venv/bin/activate
```

### Step 3: Install Dependencies
```bash
pip install -r requirements.txt
```

### Step 4: Set Up Environment Variables
Create a `.env` file in the project root:

```env
OPENAI_API_KEY="your-openai-api-key-here"
DATABASE_URL="postgresql://username:password@host:port/database"
```

> **Note**: For Supabase, your `DATABASE_URL` format should be:
> `postgresql://postgres.[PROJECT-REF]:[PASSWORD]@aws-1-ap-south-1.pooler.supabase.com:5432/postgres`

### Step 5: Requirements File
Create `requirements.txt` with the following dependencies:

```txt
fastapi==0.104.1
uvicorn[standard]==0.24.0
python-dotenv==1.0.0
langchain==0.1.0
langchain-community==0.0.10
langchain-openai==0.0.2
openai==1.6.1
sqlalchemy==2.0.23
psycopg2-binary==2.9.9
pydantic==2.5.2
```

## ⚙️ Configuration

### Database Setup
1. Create a PostgreSQL database (or use Supabase)
2. Populate with your schema and data
3. Update `DATABASE_URL` in `.env` file

### OpenAI API Key
1. Sign up at [OpenAI Platform](https://platform.openai.com/)
2. Create an API key
3. Add to `.env` file as `OPENAI_API_KEY`

### CORS Configuration
Modify allowed origins in `main.py` if needed:

```python
origins = [
    "http://127.0.0.1:8000",
    "http://localhost:8000",
    "http://your-domain.com",  # Add your domains
]
```

## 🚀 Usage

### Starting the Server
```bash
python main.py
```

The application will be available at:
- **Frontend**: http://127.0.0.1:8000
- **API Docs**: http://127.0.0.1:8000/docs
- **ReDoc**: http://127.0.0.1:8000/redoc

### Using the Application
1. Open your browser to `http://127.0.0.1:8000`
2. Enter your question in natural language (e.g., "What are the top 5 highest-paid employees?")
3. Click "Get Database Answer"
4. View the formatted answer in the "Final Answer" tab
5. Switch to "Generated SQL" tab to see the query

### Example Questions
```
How many users registered in the last 30 days?
What is the total revenue by product category?
List all employees in the Engineering department
Show the top 10 customers by order value
What's the average rating for products in Electronics?
```

## 📁 Project Structure

```
text-to-sql-agent/
│
├── frontend/
│   ├── index.html          # Main HTML interface
│   └── styles.css          # Custom CSS styling
│
├── screenshots/            # Demo images (create this folder)
│   ├── preview1.png
│   ├── preview2.png
│   ├── preview3.png
│   ├── preview4.png
│   └── preview5.png
│
├── main.py                 # FastAPI application & LangChain agent
├── .env                    # Environment variables (not in repo)
├── requirements.txt        # Python dependencies
├── .gitignore             # Git ignore rules
└── README.md              # Project documentation
```

## 📡 API Documentation

### POST `/ask`

Converts a natural language question to SQL and returns results.

**Request Body:**
```json
{
  "question": "What is the average salary by department?"
}
```

**Response:**
```json
{
  "status": "success",
  "question": "What is the average salary by department?",
  "answer": "The average salaries by department are:\n1. Engineering: $95,000\n2. Sales: $78,000\n3. Marketing: $72,000",
  "sql_query": "SELECT department, AVG(salary) as avg_salary FROM employees GROUP BY department ORDER BY avg_salary DESC;"
}
```

**Error Response:**
```json
{
  "status": "error",
  "message": "Error description",
  "sql_query": "Error: Agent failed before executing SQL."
}
```

### Interactive API Docs
Visit `http://127.0.0.1:8000/docs` for interactive Swagger UI documentation.

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Development Guidelines
- Follow PEP 8 style guide for Python code
- Add comments for complex logic
- Test thoroughly before submitting PR
- Update documentation for new features

## 📄 License

This project is licensed under the MIT License.
## 📞 Contact

**Adeel Iqbal Memon**

- 📧 Email: [adeelmemon096@yahoo.com](mailto:adeelmemon096@yahoo.com)
- 💼 LinkedIn: [linkedin.com/in/adeeliqbalmemon](https://linkedin.com/in/adeeliqbalmemon)
- 🐙 GitHub: [github.com/adeel-iqbal/text-to-sql-agent](https://github.com/adeel-iqbal/text-to-sql-agent)

---

## 🙏 Acknowledgments

- [LangChain](https://python.langchain.com/) - Framework for LLM applications
- [OpenAI](https://openai.com/) - GPT-4 language model
- [FastAPI](https://fastapi.tiangolo.com/) - Modern web framework
- [Supabase](https://supabase.com/) - Database hosting
- [Bootstrap](https://getbootstrap.com/) - UI framework

---

<div align="center">

**⭐ If you find this project useful, please consider giving it a star!**

Made with ❤️ by Adeel Iqbal Memon

</div>
