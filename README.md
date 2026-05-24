# 🎉 RSVP-Ease - Event Guestlist & Seating Coordinator

A professional, production-ready event management platform designed to simplify RSVP tracking, dietary restriction management, and intelligent table seating coordination.

## ✨ Features

### Guest Management
- ✅ Add, edit, and delete guests
- 📧 Email-based guest tracking
- 🏷️ RSVP status tracking (Pending, Accepted, Declined, Maybe)
- 🥗 Dietary restriction management
- 📋 Bulk import via CSV
- 📞 Contact information storage

### Table & Seating
- 🪑 Configure table numbers and capacities
- 🎯 Automatic capacity validation
- 📊 Smart seating assignments
- 🔒 Prevent overbooking with real-time capacity checks
- 💺 Seat-level assignment tracking

### Analytics & Insights
- 📈 Real-time event dashboard
- 👥 Guest RSVP statistics
- 🥘 Dietary requirement summaries
- 📊 Table occupancy analytics
- 💡 Event planning insights

### Technical Excellence
- ⚡ FastAPI backend with async support
- 🎨 Streamlit frontend with modern UI
- 🗄️ SQLite database with SQLAlchemy ORM
- 🐳 Docker containerization for easy deployment
- ✅ Comprehensive error handling
- 🔍 RESTful API with full documentation

## 📋 System Requirements

- **Python**: 3.11+
- **Docker** (optional): Latest version recommended
- **Modern Browser**: Chrome, Firefox, Safari, Edge

## 🚀 Quick Start

### Option 1: Docker (Recommended for Deployment)

```bash
# Clone or navigate to the project
cd rsvp

# Build and run with Docker Compose
docker-compose up --build

# Access the application
# Frontend: http://localhost:8501
# Backend API: http://localhost:8000
# API Documentation: http://localhost:8000/docs
```

### Option 2: Local Development Setup

#### Backend Setup

```bash
# Navigate to backend
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

# Copy and configure environment
cp .env.example .env

# Run backend server
python run.py
```

Backend will be available at: `http://localhost:8000`

#### Frontend Setup (in a new terminal)

```bash
# Navigate to frontend
cd frontend

# Create virtual environment
python -m venv venv

# Activate virtual environment
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Copy environment config
cp .env.example .env

# Run frontend
streamlit run app.py
```

Frontend will be available at: `http://localhost:8501`

## 📖 Usage Guide

### Dashboard
The home page displays real-time event metrics:
- Total guests and RSVP breakdown
- Seating progress and table capacity
- Dietary requirement summaries

### Guest Management
1. **Add Guests**: Manually add individual guests or bulk import via CSV
2. **Edit Guests**: Update RSVP status, contact info, and dietary restrictions
3. **Filter Guests**: View guests by RSVP status (Pending, Accepted, Declined)
4. **Delete Guests**: Remove guests from the event

### Table Setup
1. **Configure Tables**: Add tables with table numbers and guest capacities
2. **Edit Capacity**: Adjust table capacity as needed
3. **View Status**: See real-time occupancy and availability for each table

### Seating Assignments
1. **Assign Seats**: Assign accepted guests to specific tables
2. **Auto-validation**: System prevents overbooking beyond capacity
3. **Add Notes**: Include special seating requests or notes
4. **Modify Assignments**: Update or remove existing assignments

### Analytics
- Monitor event progress in real-time
- Track acceptance rates and dietary requirements
- Optimize table arrangements based on capacity data

## 🏗️ Project Structure

```
rsvp/
├── backend/                 # FastAPI backend
│   ├── app/
│   │   ├── __init__.py
│   │   ├── main.py         # FastAPI application
│   │   ├── models.py       # SQLAlchemy ORM models
│   │   ├── schemas.py      # Pydantic validation schemas
│   │   ├── crud.py         # CRUD operations
│   │   └── database.py     # Database configuration
│   ├── requirements.txt    # Backend dependencies
│   ├── run.py              # Entry point
│   └── .env.example        # Environment variables template
├── frontend/               # Streamlit frontend
│   ├── app.py             # Main Streamlit application
│   ├── requirements.txt   # Frontend dependencies
│   └── .env.example       # Environment variables template
├── docker-compose.yml     # Docker orchestration
├── Dockerfile.backend     # Backend container
├── Dockerfile.frontend    # Frontend container
├── .gitignore            # Git ignore file
└── README.md             # This file
```

## 🔌 API Documentation

### Access API Docs
When the backend is running, visit: `http://localhost:8000/docs`

### Key Endpoints

#### Guests
- `GET /guests` - List all guests
- `POST /guests` - Create new guest
- `GET /guests/{id}` - Get guest details
- `PUT /guests/{id}` - Update guest
- `DELETE /guests/{id}` - Delete guest

#### Tables
- `GET /tables` - List all tables
- `POST /tables` - Create table
- `GET /tables/{id}` - Get table details
- `PUT /tables/{id}` - Update table
- `DELETE /tables/{id}` - Delete table

#### Seating Assignments
- `GET /seating-assignments` - List assignments
- `POST /seating-assignments` - Create assignment
- `GET /seating-assignments/{id}` - Get assignment details
- `PUT /seating-assignments/{id}` - Update assignment
- `DELETE /seating-assignments/{id}` - Delete assignment

#### Dietary Restrictions
- `GET /dietary-restrictions` - List restrictions
- `POST /dietary-restrictions` - Create restriction
- `GET /dietary-restrictions/{id}` - Get details
- `PUT /dietary-restrictions/{id}` - Update restriction
- `DELETE /dietary-restrictions/{id}` - Delete restriction

#### Analytics
- `GET /analytics/summary` - Event statistics
- `GET /health` - Health check

## 🗄️ Database Schema

### Tables

#### `guests`
- id (Primary Key)
- name (String)
- email (String, Unique)
- phone (String)
- rsvp_status (Enum: pending, accepted, declined, maybe)
- created_at (DateTime)
- updated_at (DateTime)

#### `dietary_restrictions`
- id (Primary Key)
- name (String, Unique)
- description (String)

#### `tables`
- id (Primary Key)
- table_number (Integer, Unique)
- max_capacity (Integer)
- created_at (DateTime)
- updated_at (DateTime)

#### `seating_assignments`
- id (Primary Key)
- guest_id (Foreign Key)
- table_id (Foreign Key)
- seat_number (Integer)
- notes (String)
- created_at (DateTime)
- updated_at (DateTime)

#### `guest_dietary_association`
- guest_id (Foreign Key)
- dietary_id (Foreign Key)

## 🔒 Validation & Business Logic

- **Email Uniqueness**: Each guest must have a unique email address
- **Capacity Validation**: Cannot assign more guests than table capacity
- **RSVP Validation**: Only accepted guests can be assigned to seating
- **Dietary Tracking**: Support multiple dietary restrictions per guest
- **Data Integrity**: Cascade delete for related records

## 🌍 Environment Variables

### Backend (.env)
```
DATABASE_URL=sqlite:///./rsvp.db  # Database connection string
API_TITLE=RSVP-Ease API            # API title
API_VERSION=1.0.0                  # API version
DEBUG=false                         # Debug mode
```

### Frontend (.env)
```
API_URL=http://localhost:8000     # Backend API URL
```

## 📦 Deployment

### Docker Compose (Production Ready)
```bash
docker-compose up -d
```

### AWS / Cloud Deployment

#### Prepare for Cloud
1. Update environment variables for production
2. Use managed database (RDS) instead of SQLite
3. Configure SSL certificates
4. Set up proper secret management

#### Example: AWS ECS Deployment
```bash
# Push images to ECR
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin [YOUR_ECR_URL]
docker tag rsvp-backend:latest [YOUR_ECR_URL]/rsvp-backend:latest
docker push [YOUR_ECR_URL]/rsvp-backend:latest
```

### Kubernetes Deployment

See `kubernetes/` directory for K8s manifests (optional, for advanced deployments)

## 🧪 Testing

### Backend Tests
```bash
cd backend
pytest tests/
```

### Frontend Testing
Manual testing recommended for Streamlit applications.

## 🔧 Troubleshooting

### Backend Issues

**"Cannot connect to API"**
- Ensure backend is running: `python run.py`
- Check API_URL in frontend .env
- Verify firewall allows port 8000

**"Database locked"**
- Close other connections
- Use PostgreSQL instead of SQLite for production

**"Module not found"**
- Activate virtual environment
- Install requirements: `pip install -r requirements.txt`

### Frontend Issues

**"Cannot connect to backend"**
- Verify backend is running
- Check API_URL environment variable
- Ensure CORS is enabled

**"Port already in use"**
- Kill process on port 8501: `lsof -i :8501` (macOS/Linux)
- Or change Streamlit port in .env

## 📞 Support

For issues or feature requests, please refer to the [GitHub Issues](https://github.com/your-repo/issues) page.

## 📜 License

MIT License - See LICENSE file for details

## 🙏 Acknowledgments

Built with:
- [FastAPI](https://fastapi.tiangolo.com/) - Modern Python web framework
- [Streamlit](https://streamlit.io/) - Rapid data app development
- [SQLAlchemy](https://www.sqlalchemy.org/) - SQL toolkit and ORM
- [Pydantic](https://docs.pydantic.dev/) - Data validation

## 🚀 Roadmap

- [ ] Advanced guest filtering and search
- [ ] Email invitation system
- [ ] PDF seating charts export
- [ ] QR code check-in system
- [ ] Multi-event support
- [ ] Advanced analytics and reporting
- [ ] User authentication
- [ ] Real-time notifications
- [ ] Mobile app

---

**RSVP-Ease v1.0** - Making Event Planning Effortless ✨
