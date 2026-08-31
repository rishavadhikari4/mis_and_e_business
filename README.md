# 🛒 MERN E-Commerce Application

A full-featured, production-ready e-commerce web application built with the MERN stack (MongoDB, Express.js, React.js, Node.js). This application provides a complete shopping experience with user authentication, product management, shopping cart functionality, and order processing.

![E-Commerce App](https://images.pexels.com/photos/3965548/pexels-photo-3965548.jpeg)

## ✨ Features

### 👤 User Features

- **Authentication**: Secure user registration and login with JWT
- **Product Browsing**: View products with advanced search, filters, and categories
- **Shopping Cart**: Add, remove, and update product quantities
- **Checkout Process**: Complete order placement with shipping details
- **Order History**: View past orders and track order status
- **Responsive Design**: Optimized for desktop, tablet, and mobile devices

### 🔐 Admin Features

- **Admin Dashboard**: Comprehensive analytics and management interface
- **Product Management**: Full CRUD operations for products
- **Order Management**: View and update order statuses
- **Category Management**: View, Add and update categories
- **User Management**: View registered users and their details
- **Analytics**: Sales reports, top products, and revenue tracking

## 🛠 Tech Stack

### Frontend

- **React.js** - UI library for building user interfaces
- **Redux Toolkit** - State management
- **React Router** - Client-side routing
- **Tailwind CSS** - Utility-first CSS framework
- **Axios** - HTTP client for API requests
- **React Hot Toast** - Toast notifications
- **Lucide React** - Beautiful icons

### Backend

- **Node.js** - JavaScript runtime
- **Express.js** - Web application framework
- **MongoDB** - Database (for local development)
- **JWT** - JSON Web Tokens for authentication
- **bcryptjs** - Password hashing
- **Helmet** - Security middleware
- **CORS** - Cross-origin resource sharing

## 📁 Project Structure (NOT FULL)

```
mern-ecommerce-app/
├── client/                # React frontend (src/)
│   ├── package.json       # Dependencies and scripts
│   ├── components/        # Reusable UI components
│   │   ├── Layout/        # Header, Footer, Layout components
│   │   └── Products/      # Product-related components
│   ├── pages/             # Page components
│   │   ├── Auth/          # Login, Register pages
│   │   └── ...            # Other pages
│   ├── store/             # Redux store and slices
│   └── utils/             # Utility functions and API setup
├── server/                # Node.js backend
│   ├── models/            # Database configuration
│   ├── middleware/        # Authentication and other middleware
│   ├── routes/            # API routes
│   ├── package.json       # Dependencies and scripts
│   └── seeders/           # Database seeding scripts
├── images/                # Screeenshot of UI
└── README.md              # Project documentation
```

## 🚀 Getting Started

### Prerequisites

- Node.js (v18 or higher)
- npm
- MongoDB running locally (`brew services start mongodb-community` on macOS)

### Installation

> There is no root `package.json`. `client/` and `server/` are two separate npm
> projects, so every command below runs inside one of those folders.

1. **Clone the repository**

   ```bash
   git clone <repository-url>
   cd <folder-name>
   ```

2. **Install dependencies** (both projects)

   ```bash
   cd server && npm install
   cd ../client && npm install
   ```

3. **Environment Setup**

   ```bash
   cp server/.env.example server/.env
   cp client/.env.example client/.env
   ```

   `server/.env`:

   ```env
   PORT=5001
   MONGODB_URI=mongodb://localhost:27017/ecommerce
   CLIENT_URL=http://localhost:3000
   NODE_ENV=development
   JWT_SECRET=change-this-to-a-long-random-string
   KHALTI_TEST_SECRET_KEY=
   ```

   Generate a real secret with `openssl rand -hex 32`. Leave
   `KHALTI_TEST_SECRET_KEY` blank unless you are testing Khalti checkout — get a
   sandbox key from [test-admin.khalti.com](https://test-admin.khalti.com).
   Cash on Delivery works without it.

   `client/.env` (must match the server's port):

   ```env
   VITE_API_URL=http://localhost:5001/api
   VITE_WEBSITE_URL=http://localhost:3000
   ```

   > **Why 5001 and not 5000?** On macOS, port 5000 is taken by the AirPlay
   > Receiver, which answers requests with `403 Forbidden` from `AirTunes`. Use
   > 5001, or turn off AirPlay Receiver in System Settings → General → AirDrop
   > & Handoff. Vite only reads `.env` at startup, so restart it after changes.

4. **Seed the database**

   ```bash
   cd server && npm run seed
   ```

5. **Start the backend** (in one terminal)

   ```bash
   cd server && npm run dev
   ```

6. **Start the frontend** (in a second terminal)

   ```bash
   cd client && npm run dev
   ```

The application will be available at:

- **Frontend**: http://localhost:3000
- **Backend API**: http://localhost:5001/api

Log in with `admin@gmail.com / admin123` or `user@gmail.com / user123`.

## 🔧 Available Scripts

Run from `server/`:

- `npm run dev` - Start the API server
- `npm start` - Same as `dev`
- `npm run seed` - Reset and seed the database with sample data

Run from `client/`:

- `npm run dev` - Start the Vite dev server on port 3000
- `npm run build` - Build the frontend into `client/dist`
- `npm run preview` - Serve the production build locally

## 🖥️ Frontend Details

### State Management

The application uses Redux Toolkit for state management with the following slices:

- **authSlice**: User authentication and profile management
- **productSlice**: Product catalog and filtering
- **cartSlice**: Shopping cart functionality
- **orderSlice**: My order page functionality for orders
- **ordersSlice**: Order management for Admin
- **usersSlice**: Get user Update User
- **categoriesSlice**: Get, Update, Create, Delete Categories
- **adminSlice**: Management of Admin

### API Integration

- Centralized API configuration using Axios
- Automatic token attachment for authenticated requests
- Global error handling and toast notifications
- Request/response interceptors for enhanced UX

### Responsive Design

- Mobile-first approach using Tailwind CSS
- Breakpoints: Mobile (<768px), Tablet (768-1024px), Desktop (>1024px)
- Optimized layouts for all screen sizes

## ⚙️ Backend Details

### Database Schema

The application uses MongoDB for local development with the following main tables inside models:

- **users**: User accounts and profiles
- **categories**: Product categories
- **products**: Product catalog
- **orders**: Customer orders
- **order_items**: Individual order items
- **cart_items**: Shopping cart contents

### API Endpoints

#### Authentication

- `POST /api/auth/register` - User registration
- `POST /api/auth/login` - User login
- `GET /api/auth/me` - Get current user

#### Products

- `GET /api/products` - Get products with filtering and pagination
- `GET /api/products/:id` - Get single product
- `GET /api/products/categories/all` - Get all categories

#### Cart & Orders

- `GET /api/users/cart` - Get user's cart
- `POST /api/users/cart` - Add item to cart
- `PUT /api/users/cart/:productId` - Update cart item
- `DELETE /api/users/cart/:productId` - Remove from cart
- `POST /api/orders` - Create new order
- `GET /api/orders` - Get user's orders
- `More`

#### Admin (Protected)

- `GET /api/admin/stats` - Dashboard statistics
- `GET /api/admin/products` - Manage products
- `POST /api/admin/products` - Create product
- `PUT /api/admin/products/:id` - Update product
- `DELETE /api/admin/products/:id` - Delete product
- `More`

### Security Features

- JWT-based authentication
- Password hashing with bcryptjs
- Rate limiting (`express-rate-limit` is wired up but currently commented out in `server/index.js`)
- CORS configuration
- Helmet for security headers
- Input validation and sanitization

### Payment Integration

- Khalti Wallet Checkout
- Cash on Delivery

## 💾 Database Seeding

The application includes a comprehensive seeding script that populates the database with:

- **Sample Categories**: Electronics, Clothing, Home & Garden, Sports, Books
- **Sample Products**: 8 featured products with images and descriptions
- **Admin User**: Email: `admin@gmail.com`, Password: `admin123`
- **Test User**: Email: `user@gmail.com`, Password: `user123`

Run the seeder from the `server/` folder. It **clears existing data** first:

```bash
cd server && npm run seed
```

## 🌐 Deployment Guide (NOTE: NOT YET DEPLOYED)

### Frontend Deployment (Vercel)

1. Build the project: `cd client && npm run build`
2. Deploy the `dist` folder to Vercel
3. Set environment variables in Vercel dashboard

### Backend Deployment (Railway/Render)

1. Create a new service on Railway or Render
2. Connect your GitHub repository
3. Set environment variables:
   - `NODE_ENV=production`
   - `JWT_SECRET=your-production-secret`
   - `CLIENT_URL=your-frontend-url`
4. The service will automatically deploy

## 🧪 Testing

### Manual Testing Checklist

- [ ] User registration and login
- [ ] Product browsing and filtering
- [ ] Add/remove items from cart
- [ ] Checkout process
- [ ] Order placement and history
- [ ] Admin dashboard functionality

### API Testing

Use tools like Postman or Insomnia to test API endpoints:

```bash
# Example: Get products
GET http://localhost:5001/api/products

# Example: Login
POST http://localhost:5001/api/auth/login
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "user123"
}
```

## 🧹 Troubleshooting

### Common Issues

**Port already in use**

```bash
# Kill process on port 5001
npx kill-port 5001
```

On macOS, port 5000 is held by the AirPlay Receiver, not by a stale process —
`kill-port` will not free it. Use a different port or disable AirPlay Receiver
in System Settings → General → AirDrop & Handoff.

**Database connection issues**

- Ensure MongoDB is running: `brew services list` (or `pgrep mongod`)
- Verify `MONGODB_URI` in `server/.env` is reachable
- The server exits on a failed connection — check its log output

**CORS errors**

- Ensure `CLIENT_URL` in `.env` matches your frontend URL
- Check CORS configuration in `server/index.js`

**Authentication issues**

- Verify JWT secret is set in environment variables
- Check token expiration settings
- Ensure proper token storage in localStorage

### Performance Optimization

- Enable gzip compression in production
- Implement image optimization and lazy loading
- Use Redis for session storage in production
- Add database indexing for frequently queried fields

## 📸 Screenshots

### Homepage

![Homepage](images/Home-Page.png)

### Product Page

![Products](images/product-page.png)

### Order Page

![Cart](images/myorder-page.png)

### Login Page

![Cart](images/Login-Page.png)

### Register Page

![Cart](images/Register-Page.png)

### Admin Panel

![Cart](images/Admin-Panel.png)

### Orders Management

![Cart](images/order-management.png)

### Product Management

![Cart](images/Product-Management.png)


## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📞 Support

For support and questions:

- Create an issue in the GitHub repository
- Email: luitelsaurav627@gmail.com
- Documentation: [Project Wiki](link-to-wiki)

## 🙏 Acknowledgments

- [Pexels](https://pexels.com) for providing high-quality stock images
- [Lucide](https://lucide.dev) for beautiful icons
- [Tailwind CSS](https://tailwindcss.com) for the utility-first CSS framework
- The open-source community for amazing tools and libraries

---

**Built with ❤️ by Saurav**

_This is a demonstration project showcasing modern web development practices with the MERN stack._
