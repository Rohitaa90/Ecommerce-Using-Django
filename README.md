# Django E-Commerce Application 🛍️

A complete e-commerce web application built with Django. Users can browse products, add to cart, checkout, and make payments via PayTm integration.

---

## 🎯 Features

✅ **User Authentication** - Sign up, login, logout with Django auth  
✅ **Product Catalog** - Display products by category  
✅ **Shopping Cart** - Add/remove items from cart  
✅ **Checkout System** - Collect user shipping details  
✅ **Payment Integration** - PayTm payment gateway  
✅ **Order Tracking** - Track order status with updates  
✅ **Contact Form** - Customer support messages  
✅ **Admin Panel** - Django built-in admin for product management  
✅ **Responsive UI** - Bootstrap-based design  

---

## 🛠️ Tech Stack

- **Backend:** Django 3.0.6 (Python)
- **Frontend:** HTML, CSS, JavaScript, Bootstrap
- **Database:** SQLite
- **Payment:** PayTm Gateway
- **Libraries:** jQuery, Font Awesome, AOS (animations)

---

## 📁 Project Structure

```
ecommerce/
├── ecommerce/              # Project settings
│   ├── settings.py         # Configuration, database, apps
│   ├── urls.py             # Main URL routing
│   ├── wsgi.py             # WSGI app
│   └── asgi.py             # ASGI app
│
├── ecomapp/                # Main application
│   ├── models.py           # Database models (Product, Orders, etc)
│   ├── views.py            # Business logic
│   ├── urls.py             # App routes
│   ├── admin.py            # Admin panel setup
│   └── migrations/         # Database version control
│
├── templates/              # HTML pages
│   ├── index.html          # Homepage
│   ├── base.html           # Base template
│   ├── checkout.html       # Checkout page
│   └── ...
│
├── static/                 # CSS, JS, images
│   ├── assets/css/         # Stylesheets
│   ├── assets/js/          # JavaScript files
│   └── assets/vendor/      # Third-party libraries (Bootstrap, jQuery)
│
├── media/                  # User uploaded images
│
├── PayTm/                  # Payment integration
│   └── Checksum.py         # PayTm checksum module
│
├── .env                    # Environment variables (SECRET_KEY, etc)
├── .gitignore              # Git ignore file
├── db.sqlite3              # Database
├── manage.py               # Django CLI
└── README.md               # This file
```

---

## 🚀 Installation & Setup

### 1. Clone the Repository
```bash
git clone <your-repo-url>
cd django-e-commerce/Ecommerce-Django-Project/ecommerce
```

### 2. Install Python Packages
```bash
pip install django pillow python-dotenv pycryptodome
```

### 3. Configure Environment Variables
Create `.env` file in project root:
```
SECRET_KEY=your_secret_key_here
DEBUG=True
PAYTM_MERCHANT_KEY=your_merchant_key_here
ALLOWED_HOSTS=localhost,127.0.0.1
```

### 4. Apply Database Migrations
```bash
python manage.py migrate
```

### 5. Create Superuser (Admin)
```bash
python manage.py createsuperuser
```
Follow prompts to create username and password.

### 6. Add Products via Admin
```bash
python manage.py runserver
```
Visit: `http://localhost:8000/admin/`
- Login with superuser credentials
- Add products manually

### 7. Run Development Server
```bash
python manage.py runserver
```

Access the application:
- **Homepage:** http://localhost:8000/
- **Admin Panel:** http://localhost:8000/admin/

---

## 📊 Database Models

### Product
```python
- product_name: CharField
- category: CharField
- price: IntegerField
- desc: CharField
- image: ImageField
- pub_date: DateField
```

### Orders
```python
- order_id: AutoField
- items_json: CharField (stores cart items)
- amount: IntegerField
- name, email: CharField
- address1, address2, city, state, zip_code: CharField
- paymentstatus: CharField
- oid, amountpaid: CharField
```

### Contact
```python
- msg_id: AutoField
- name, email, phone: CharField
- desc: CharField
```

### OrderUpdate
```python
- Tracks order status updates
```

---

## 🔐 Security Notes

⚠️ **Development Only:**
- `DEBUG = True` in `.env` (turn off in production)
- `SECRET_KEY` stored in `.env` (don't expose!)
- `ALLOWED_HOSTS` configured in `.env`

✅ **Best Practices:**
- Never commit `.env` file (it's in `.gitignore`)
- Use environment variables for all secrets
- Use HTTPS in production

---

## 🎯 URL Routes

```
/                    - Homepage (product listing)
/login               - User login
/signup              - User registration
/logout              - User logout
/about               - About page
/contactus           - Contact form
/tracker             - Order tracking
/products/<id>       - Product detail page
/checkout/           - Checkout page
/handlerequest/      - Process checkout
/admin/              - Admin panel
```

---

## 💳 Payment Integration (PayTm)

To enable PayTm payments:

1. Register on [PayTm Merchant Portal](https://merchant.paytm.com/)
2. Get your `MERCHANT_KEY` and `MERCHANT_ID`
3. Add to `.env`:
```
PAYTM_MERCHANT_KEY=your_merchant_key
```
4. Update `views.py` with your `MERCHANT_ID`

---

## 📝 Key Views Explained

### home()
- Fetches all products from database
- Groups by category
- Renders homepage with product carousel

### checkout()
- Collects customer shipping info
- Creates order in database
- Initiates PayTm payment

### tracker()
- Shows order status updates
- Filters by order ID and email
- Returns updates in JSON

### productView()
- Displays single product details
- Shows price, description, image

---

## 🔧 Common Commands

```bash
# Start development server
python manage.py runserver

# Create migrations (after model changes)
python manage.py makemigrations

# Apply migrations
python manage.py migrate

# Create superuser
python manage.py createsuperuser

# Access Django shell
python manage.py shell

# Collect static files (for production)
python manage.py collectstatic
```

---

## 🚀 Deployment Checklist

Before deploying to production:

- [ ] Set `DEBUG = False` in `.env`
- [ ] Set `SECRET_KEY` to strong random value
- [ ] Configure `ALLOWED_HOSTS`
- [ ] Use PostgreSQL instead of SQLite
- [ ] Enable HTTPS
- [ ] Set up proper logging
- [ ] Configure payment gateway credentials
- [ ] Use environment variables for all secrets
- [ ] Run security checks: `python manage.py check --deploy`

---

## 🤝 Interview Talking Points

1. **Architecture:** Django MVC pattern - Models for DB, Views for logic, Templates for UI
2. **ORM:** Uses Django ORM instead of raw SQL
3. **Authentication:** Built-in user authentication system
4. **Admin Panel:** Ready-made admin interface (huge time saver)
5. **Payment:** Third-party PayTm integration
6. **Database:** SQLite for dev, can upgrade to PostgreSQL
7. **Static Files:** Bootstrap + jQuery for frontend

---

## 🐛 Troubleshooting

**Error: ModuleNotFoundError: No module named 'Crypto'**
```bash
pip install pycryptodome
```

**Error: No module named 'dotenv'**
```bash
pip install python-dotenv
```

**Error: Image upload not working**
- Ensure `MEDIA_URL` and `MEDIA_ROOT` configured in `settings.py`
- Create `media/` folder manually if not exists

---

## 📚 Learning Resources

- [Django Documentation](https://docs.djangoproject.com/)
- [Django ORM](https://docs.djangoproject.com/en/3.0/topics/db/models/)
- [Django Authentication](https://docs.djangoproject.com/en/3.0/topics/auth/)
- [PayTm Integration Guide](https://developer.paytm.com/)

---

## 📄 License

This project is open source and available for educational purposes.

---

**Happy Coding! 🚀**

For questions or issues, feel free to create an issue or contact the developer.
