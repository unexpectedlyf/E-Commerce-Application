# Django E-commerce Application 🛍️

# 🚀 Introduction:

This is a foundational e-commerce web application built with Django and Django REST Framework. It features a robust multi-role user authentication system (distinguishing between buyers and vendors), comprehensive store and product management functionalities, a user-friendly shopping cart, product review capabilities, and a simulated external integration for real-time alerts.


# ✨ Features
User Authentication & Authorization: Secure registration and login mechanisms tailored for distinct user roles.

Flexible User Roles:

- Buyers: Seamlessly browse products, add items to their cart, view cart contents, proceed through a simulated checkout process, and contribute product reviews.
  
- Vendors: Empowered to effortlessly create, update, and remove their online stores, as well as manage their product inventory (including product images).

- Admin: Full administrative oversight and control over all application aspects via the intuitive Django Admin interface.

- Store Management: Vendors gain full control to establish and maintain their individual online storefronts.

- Product Management: Vendors can add new products, update existing details (e.g., price, stock), and delete products, ensuring accurate and up-to-date listings.

- Shopping Cart: An intuitive, session-based shopping cart provides a smooth buying experience.

- Simulated Checkout Process: Facilitates an end-to-end purchasing flow, including stock deduction and email invoice generation (output to console in development).
  
- Product Reviews: Buyers can share their feedback by submitting ratings and comments for products.
  
- Password Reset: Secure mechanism for users to request and reset forgotten passwords (email instructions printed to console in development).
  
- RESTful API: Exposes programmatic access to core e-commerce data (stores, products, reviews), supporting external integrations and single-page applications.
  
- Simulated External Integration (e.g., Twitter): Demonstrates a webhook-like functionality, automatically "tweeting" (logging to console) alerts for new store and product creations.
  
- Responsive UI: Built with Tailwind CSS for a clean, modern, and adaptive user interface across various devices.



# 🛠️ Technologies Used:

- Backend Framework: Django 5.x
  
- API Development: Django REST Framework (DRF)
  
- Authentication: Django REST Framework Simple JWT (JSON Web Tokens)
  
- Database: SQLite (default for development; easily configurable for PostgreSQL/MariaDB)
  
- Frontend Templating: Django Templates
  
- Styling: Tailwind CSS
  
- Image Processing: Pillow
  
- Email Simulation: Django's console.EmailBackend (for development/testing)


# ⚙️ Setup Instructions:
Follow these steps to get the project up and running on your local machine.

Prerequisites
Python 3.8+

pip (Python package installer)

Virtual Environment
It's highly recommended to use a virtual environment to manage project dependencies.

python3 -m venv EcommerceEnv
source EcommerceEnv/bin/activate  # On macOS/Linux
# EcommerceEnv\Scripts\activate   # On Windows (use PowerShell or Git Bash for 'source')

Install Dependencies
Navigate to your project's root directory (where manage.py is located) and install the required packages:

pip install Django djangorestframework djangorestframework-simplejwt Pillow

# Database Setup
Apply database migrations to create the necessary tables and schema.

python manage.py makemigrations
python manage.py migrate

Create Superuser
Create a superuser account to access the Django admin panel. This user will have full administrative privileges and can be used to set up initial data and user groups.

python manage.py createsuperuser

Follow the prompts in the terminal to set up your username, email, and password.

Create User Groups
The application relies on Vendors and Buyers groups for effective role-based permissions. You need to create these groups manually in the Django admin:

Run the development server (see next step).

Open your browser and navigate to http://127.0.0.1:8000/admin/.

Log in using your superuser credentials.

Under the "Authentication and Authorization" section, click on "Groups".

Click the "Add group" button (green + sign).

Enter Vendors as the name and click "Save".

Repeat steps 5-6 to create another group named Buyers.

(Optional but Recommended) Assign your superuser to the Vendors group:

Go to "Authentication and Authorization" -> "Users".

Click on your superuser's username.

In the "Groups" section, move Vendors from "Available groups" to "Chosen groups".

Click "Save".

# Run Development Server
Start the Django development server to access the application via your web browser.

python manage.py runserver

The application will be accessible at http://127.0.0.1:8000/.

# 🔑 API Endpoints (with Postman)
The RESTful API endpoints are protected using JWT (JSON Web Token) authentication. You will need to obtain an access token before making most API requests.

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

Response: Contains access and refresh tokens. For subsequent authenticated requests, include the access token in the Authorization header: Authorization: Bearer <YOUR_ACCESS_TOKEN>.

Store Management
List Stores / Create Store:

Method: GET (list all stores accessible to the user) / POST (create new store - requires vendor token)

URL: http://127.0.0.1:8000/api/stores/

POST Body (raw JSON, example):

{
    "name": "My New E-Store",
    "description": "A fantastic place for great products!",
    "logo": null  // For image upload, you'd use form-data in Postman
}

Retrieve/Update/Delete Store:

Method: GET / PUT / DELETE

URL: http://127.0.0.1:8000/api/stores/<store_id>/

Note: PUT and DELETE requests require the owning vendor's access token.

Product Management
List Products for a Store / Create Product:

Method: GET / POST (requires owning vendor's token)

URL: http://127.0.0.1:8000/api/stores/<store_id>/products/

POST Body (raw JSON, example):

{
    "store": <store_id>,
    "name": "Product X",
    "description": "An truly amazing product.",
    "price": "19.99",
    "stock": 100,
    "image": null // For image upload, use form-data in Postman
}

Retrieve/Update/Delete Product:

Method: GET / PUT / DELETE

URL: http://127.0.0.1:8000/api/products/<product_id>/

Note: PUT and DELETE requests require the owning vendor's access token.

Review Listing
List Reviews for a Product:

Method: GET

URL: http://127.0.0.1:8000/api/products/<product_id>/reviews/

# 🐦 Simulated External Integration
When you successfully create a new Store or a new Product via their respective API POST endpoints, a simulated external alert (e.g., a "tweet") will be generated. The content of this alert will be printed directly to your Django development server's console. This demonstrates a potential integration point with actual external APIs like Twitter, Slack, or other notification services.

# 🧪 Running Tests
(Currently, a specific test suite is not provided in this foundational setup. However, for robust production applications, Django's testing framework would be utilized.)

To run Django's default tests (if you implement any later):

python manage.py test

# 📞 Contact
For any questions, feedback, or collaborations, please feel free to reach out.

# 📄 License
This project is licensed under the MIT License - see the LICENSE file for details.
