Workspace Room Booking System

   -This project is a Django-based room booking system that supports:

   -Private, Shared, and Conference rooms
 
   -Team and individual bookings

   -Redis-backed slot availability

   -Admin and user management APIs

   -JWT authentication

  -Dockerized setup with Redis

Structure 
workspace_booking
├── booking                    
│   ├── migrations           
│   ├── models.py             
│   ├── views.py              
│   ├── urls.py                   
│   ├── orm_manager           
│   ├── services/redis_booking_service.py/redis_setup.py    
│   ├── management/commands/init_redis_availability.py

├── workspace_booking     
├── Dockerfile                 
├── docker-compose.yml         
├── manage.py                  
├── requirements.txt           
└── README.md                  


Technologies Used
	Django + Django REST Framework
	PostgreSQL (or SQLite for dev)
	Redis
	Docker & Docker Compose
	JWT Authentication
	Cron (via python-crontab)


Features 

  - JWT-based authentication
  
  - Admin roles
      - (View All Bookingd, Add User, Add/Update Team with team members)
	  
  - User roles
      - (Check Availability, Room Booking, BookingHistory, Cancel Booking)
	  
  - Weekly slot availability
  
  - Shared, Private, Conference room types
  
  - Redis caching for room availability
  
  - Dockerized setup
  
  - REST APIs with pagination & error handling
  
  - Child booking restrictions & team bookings
  
  - Cron setup to reset availability weekly

Setup Instructions
  Clone the Repository
  
    git clone https://github.com/BhargaviLenka/event_booking_web_application.git
    cd room-booking/workspace_booking
	
Docker Setup (Recommended)
  1. Make sure Docker is installed
	You should have Docker Engine ≥ 24

	Check:
	docker --version
	docker compose version
 
  2: Build & Run the Containers
  
	docker compose up --build
	The server will be available at: http://localhost:8000

Running Locally without Docker
  1. Set up a virtual environment:
 
	python3 -m venv venv
	source venv/bin/activate
  	
  2. Install Dependices:

	pip install --upgrade pip
	pip install -r requirements.txt
 
  3. Start Redis (if not using Docker):

	redis-server
 
  4. Run migrations and server:
 
	python manage.py migrate
	python manage.py runserver

API Documentation

Authentication
  
	/api/login/ → Get access and refresh token
	/api/token/refresh/ → Refresh the access token
  Pass the access token in headers:
  
	Authorization: Bearer <access_token>

User Management (Admin)

	POST /api/users/add/ — Create user

Team Management (Admin)

	POST /api/teams/add/ — Create a team
	POST /api/add-user/ — Add user to team
	POST /api/remove-user/ — Remove user from team

Booking APIs

	GET /api/bookings-available/?date=YYYY-MM-DD — View available slots
	POST /api/book-room/ — Create a booking
	POST /api/cancel/<int:booking_id>/ — Cancel a booking
	GET /api/bookings/history/ — Get your past bookings (paginated)
	GET /api/bookings/all/ — Admin: Get all bookings

Contributions

  - Designed and implemented full Django backend with REST APIs

  - Used Redis to manage and cache availability per time slot
	
  - Ensured concurrency safety with atomic booking logic
	
  - Developed role-based user and team management features
	
  - Built clean React frontend with protected routes and toast notifications

 
Notes

 - Booking availability is cached in Redis for performance

 - Redis keys are initialized via migration and weekly job

 - Admins can manage users, teams, and monitor bookings

 - Prevents children under 10 from booking solo

 - Teams can only book conference rooms (min 3 members)

Contact

  Bhargavi Lenka
  
  lenkabhargavi2204@gmail.com
  
  https://www.linkedin.com/in/lenka-bhargavi-profile/
  
  https://github.com/BhargaviLenka/

