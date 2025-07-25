Django E-commerce Application
This is a foundational e-commerce web application built with Django and Django REST Framework, featuring user authentication (buyers and vendors), store management, product listings, a shopping cart (session-based), product reviews, and a simulated integration for tweeting new store and product alerts.

Table of Contents
Features

Technologies Used

Setup Instructions

Prerequisites

Virtual Environment

Install Dependencies

Database Setup

Create Superuser

Create User Groups

Run Development Server

API Endpoints (with Postman)

Authentication

Store Management

Product Management

Review Listing

Simulated Twitter Integration

Running Tests

Contact

1. Features
User Authentication: Secure registration and login for different user roles.

User Roles:

Buyers: Can browse products, add to cart, view cart, checkout, and submit reviews.

Vendors: Can create, edit, and delete their stores and manage products within their stores.

Admin: Full access to manage all aspects of the application via Django Admin.

Store Management: Vendors can create and manage multiple stores.

Product Management: Vendors can add, update, and delete products within their stores, including product images.

Shopping Cart: Session-based cart functionality for buyers.

Checkout Process: Simulated checkout, including stock deduction and an email invoice (sent to console in development).

Product Reviews: Buyers can submit reviews for products (currently unverified, but extensible).

Password Reset: Users can request and reset forgotten passwords via email (console output in development).

RESTful API: Provides programmatic access to store, product, and review data.

Simulated Twitter Integration: Automatically "tweets" (prints to console) when new stores or products are created via the API.

Responsive UI: Basic responsive design using Tailwind CSS.

2. Technologies Used
Backend: Django 5.x

API: Django REST Framework (DRF)

Authentication: Django REST Framework Simple JWT

Database: SQLite (default, for development)

Frontend (Templates): Django Templates with Tailwind CSS

Email Simulation: Django's console.EmailBackend

Image Handling: Pillow (Django's image processing library)

3. Setup Instructions
Follow these steps to get the project up and running on your local machine.

Prerequisites
Python 3.8+

pip (Python package installer)

Virtual Environment
It's highly recommended to use a virtual environment to manage dependencies.

python3 -m venv EcommerceEnv
source EcommerceEnv/bin/activate  # On macOS/Linux
# EcommerceEnv\Scripts\activate   # On Windows

Install Dependencies
Navigate to your project's root directory (where manage.py is located) and install the required packages:

pip install Django djangorestframework djangorestframework-simplejwt Pillow

Database Setup
Apply database migrations to create the necessary tables.

python manage.py makemigrations
python manage.py migrate

Create Superuser
Create a superuser account to access the Django admin panel and manage initial data, including creating groups.

python manage.py createsuperuser

Follow the prompts to set up your username, email, and password.

Create User Groups
The application relies on 'Vendors' and 'Buyers' groups for role-based permissions. You need to create these manually in the Django admin:

Run the development server (see next step).

Open your browser and go to http://127.0.0.1:8000/admin/.

Log in with your superuser credentials.

Under "Authentication and Authorization", click on "Groups".

Click "Add group" (the green + button).

Enter Vendors as the name and click "Save".

Repeat for a group named Buyers.

(Optional but Recommended) Assign your superuser to the Vendors group:

Go to "Authentication and Authorization" -> "Users".

Click on your superuser.

In the "Groups" section, move Vendors from "Available groups" to "Chosen groups".

Click "Save".

Run Development Server
Start the Django development server.

python manage.py runserver

The application will be accessible at http://127.0.0.1:8000/.

4. API Endpoints (with Postman)
The API endpoints are protected by JWT authentication. You'll need to obtain an access token first.

Authentication
Get Access Token:

Method: POST

URL: http://127.0.0.1:8000/api/token/

Headers: Content-Type: application/json

Body (raw JSON):

{
    "username": "your_username",
    "password": "your_password"
}

Response: Contains access and refresh tokens. Use the access token in the Authorization header for subsequent requests: Authorization: Bearer <YOUR_ACCESS_TOKEN>.

Store Management
List Stores / Create Store:

Method: GET (list all/vendor's stores) / POST (create new store - requires vendor token)

URL: http://127.0.0.1:8000/api/stores/

POST Body (raw JSON, example):

{
    "name": "My New E-Store",
    "description": "A place for great products!",
    "logo": null
}

Retrieve/Update/Delete Store:

Method: GET / PUT / DELETE

URL: http://127.0.0.1:8000/api/stores/<store_id>/

Note: PUT/DELETE require the owning vendor's token.

Product Management
List Products for a Store / Create Product:

Method: GET / POST (requires owning vendor's token)

URL: http://127.0.0.1:8000/api/stores/<store_id>/products/

POST Body (raw JSON, example):

{
    "store": <store_id>,
    "name": "Product X",
    "description": "An amazing product.",
    "price": "19.99",
    "stock": 100,
    "image": null
}

Retrieve/Update/Delete Product:

Method: GET / PUT / DELETE

URL: http://127.0.0.1:8000/api/products/<product_id>/

Note: PUT/DELETE require the owning vendor's token.

Review Listing
List Reviews for a Product:

Method: GET

URL: http://127.0.0.1:8000/api/products/<product_id>/reviews/

5. Simulated Twitter Integration
When you successfully create a new Store or a new Product via their respective API POST endpoints, a simulated tweet will be generated. This tweet's content will be printed directly to your Django development server's console. This demonstrates where you would integrate with an actual Twitter API.

6. Running Tests
(Currently, no specific test suite is provided. However, for a production application, you would typically have Django tests.)

To run Django's default tests (if you add any):

python manage.py test

7. Contact
For any questions or feedback, please reach out.
