# EasyBuy: Flask E-Commerce Platform

![Python](https://img.shields.io/badge/Python-3776ab?logo=python&logoColor=white&style=flat-square)
![Flask](https://img.shields.io/badge/Flask-000000?logo=flask&logoColor=white&style=flat-square)
![SQLite](https://img.shields.io/badge/SQLite-003b57?logo=sqlite&logoColor=white&style=flat-square)
![Bootstrap](https://img.shields.io/badge/Bootstrap-7952b3?logo=bootstrap&logoColor=white&style=flat-square)

A Flask e-commerce web application with a product catalog, shopping cart, order flow, user accounts and an admin dashboard. I used it as a base to study how a typical web shop is built, to add my own **flash-sales feature**, and to write a **go-to-market plan** for it.

> **Attribution.** EasyBuy is built on top of the open-source Flask shop template by [@fchavonet](https://github.com/fchavonet) ([`full_stack-flask_shop_template`](https://github.com/fchavonet/full_stack-flask_shop_template)). The core application structure (authentication, catalog, cart, admin dashboard, base design) comes from that template, and the original commit history is preserved in this repository. The additions listed below are mine.

## My contributions

| Area | What I added |
|---|---|
| **Flash sales** | New `is_flash_sale` and `flash_sale_end` fields on the `Product` model, helper methods (`is_flash_sale_active`, `flash_sale_days_remaining`), admin controls on the add/edit product forms, a flash-sale management section in the admin dashboard, and a flash-sale block on the catalog page that only shows active sales |
| **Storefront customization** | Reworked base layout, home page, carousel, legal page and product card template, plus a new product catalog and imagery |
| **Marketing plan** | A full go-to-market plan for the platform (in French): positioning, budget phases, KPIs and a 6-to-18-month roadmap. See [`easybuy-marketing-plan.md`](easybuy-marketing-plan.md), with the LaTeX source and PDF alongside |

## Features

- Product catalog with sorting, recommended and trending sections
- Product detail pages, shopping cart and simulated checkout (no real payment)
- User registration, login, profile and account deletion (Flask-Login)
- Order history per user
- Admin dashboard: add, edit and delete products, manage flash sales
- Responsive layout (Bootstrap)

## Screenshots

| Home | Catalog |
|---|---|
| ![Home](assets/images/screenshots/home.webp) | ![Catalog](assets/images/screenshots/catalog.webp) |

| Admin dashboard | Profile |
|---|---|
| ![Dashboard](assets/images/screenshots/dashboard.webp) | ![Profile](assets/images/screenshots/profile.webp) |

## Tech stack

Python · Flask 3 · Flask-SQLAlchemy · Flask-Login · SQLite · Jinja2 · Bootstrap · vanilla JavaScript

## Project structure

```
app/
  app.py          # Routes: catalog, cart, checkout, orders, admin dashboard
  auth.py         # Auth blueprint: register, login, profile, delete account
  models.py       # User, Product, CartItem, Order, OrderItem
templates/        # Jinja2 templates (shop/, admin/, auth/)
static/           # CSS, JS, images
assets/           # README screenshots
config.py         # Environment-based configuration
run.py            # Entry point
```

## Getting started

```bash
git clone https://github.com/Touhoustic/EasyBuy.git
cd EasyBuy
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt

export SECRET_KEY="a-long-random-string"   # Windows: set SECRET_KEY=...

flask --app app init-database   # creates the SQLite database
flask --app app shell           # then create an admin user:
```

```python
admin = User(username="admin", email="admin@example.com", is_admin=True)
admin.set_password("choose-a-strong-password")
db.session.add(admin)
db.session.commit()
exit()
```

```bash
python run.py                   # http://127.0.0.1:5000
```

## Security status

This is a learning project and is **not production-ready**. Known gaps I would address before any real deployment:

- No CSRF protection on forms
- Default `SECRET_KEY` fallback in `config.py` (set the environment variable)
- No rate limiting or account lockout on login
- File upload validation limited to extension and size checks
- Checkout is simulated, with no payment provider

## Roadmap

- Add CSRF protection and rate limiting
- Stripe integration for real payments
- Automated tests and CI
- Fully documented REST API

## License

The upstream template does not publish a license, so I have not added one to this repository. If you want to reuse the code, please check with the original author.
