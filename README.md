# Expense Tracker

A comprehensive expense tracking web application built with React, Express.js, and MySQL. Features include expense management, visual analytics, reporting, and a recycle bin for deleted items.

## Features

- 📊 **Dashboard** with summary cards and interactive charts
- 💰 **Expense Management** - Add, edit, delete expenses with instant actions
- 📈 **Visual Analytics** - Charts showing spending trends (30/90 days)
- 📑 **Reports** - Payment method breakdown with CSV export
- 🗑️ **Recycle Bin** - Restore or permanently delete expenses
- 🌙 **Dark/Light Theme** - Toggle between themes with font size options
- 💱 **Indian Rupee Support** - Native currency formatting
- 📱 **Responsive Design** - Works on desktop and mobile

## Tech Stack

- **Frontend**: React, TypeScript, Tailwind CSS, Shadcn/ui
- **Backend**: Express.js, TypeScript
- **Database**: MySQL with Drizzle ORM
- **Charts**: Chart.js
- **State Management**: TanStack Query

## Prerequisites

- Node.js 18+ 
- MySQL 5.7+ or MySQL 8.0+
- npm or yarn

## Local Setup Instructions

### 1. Clone the Repository
```bash
git clone <repository-url>
cd expense-tracker
```

### 2. Install Dependencies
```bash
npm install
```

### 3. Database Setup

#### Option A: Local MySQL Installation
1. Install MySQL on your system
2. Create a new database:
```sql
CREATE DATABASE expense_tracker;
```

#### Option B: Using Docker
```bash
docker run --name mysql-expense-tracker \
  -e MYSQL_ROOT_PASSWORD=password \
  -e MYSQL_DATABASE=expense_tracker \
  -p 3306:3306 \
  -d mysql:8.0
```

### 4. Environment Configuration
1. Copy the example environment file:
```bash
cp .env.example .env
```

2. Update the `.env` file with your MySQL connection details:
```env
DATABASE_URL=mysql://username:password@localhost:3306/expense_tracker
NODE_ENV=development
PORT=5000
```

**Replace the following in your DATABASE_URL:**
- `username` - Your MySQL username (e.g., `root`)
- `password` - Your MySQL password
- `localhost:3306` - Your MySQL host and port
- `expense_tracker` - Your database name

### 5. Database Migration
Run the database migrations to create tables:
```bash
npm run db:push
```

### 6. Start the Application
```bash
npm run dev
```

The application will be available at: `http://localhost:5000`

## Production Deployment

### 1. Build the Application
```bash
npm run build
```

### 2. Set Environment Variables
```bash
export DATABASE_URL="mysql://username:password@your-mysql-host:3306/expense_tracker"
export NODE_ENV=production
export PORT=5000
```

### 3. Run Database Migrations
```bash
npm run db:push
```

### 4. Start the Server
```bash
npm start
```

## Database Schema

The application uses three main tables:

- **expenses** - Main expense records
- **deleted_expenses** - Recycle bin for deleted expenses  
- **users** - User accounts (for future authentication)

## Environment Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `DATABASE_URL` | MySQL connection string | `mysql://user:pass@localhost:3306/db` |
| `NODE_ENV` | Environment mode | `development` or `production` |
| `PORT` | Server port | `5000` |

## API Endpoints

### Expenses
- `GET /api/expenses` - Get all expenses
- `POST /api/expenses` - Create expense
- `PUT /api/expenses/:id` - Update expense
- `DELETE /api/expenses/:id` - Delete expense (moves to recycle bin)

### Analytics
- `GET /api/expenses/analytics/summary` - Get expense summary
- `GET /api/expenses/analytics/daily?days=30` - Get daily analytics

### Recycle Bin
- `GET /api/deleted-expenses` - Get deleted expenses
- `POST /api/deleted-expenses/:id/restore` - Restore expense
- `DELETE /api/deleted-expenses/:id` - Permanently delete
- `DELETE /api/deleted-expenses` - Clear recycle bin

### Export
- `GET /api/expenses/export/csv` - Export expenses as CSV

## Customization

### Changing Database Connection
To use a different MySQL database, simply update the `DATABASE_URL` in your `.env` file:

```env
DATABASE_URL=mysql://new_user:new_password@new_host:3306/new_database
```

### Adding Categories
Edit the category options in:
- `client/src/components/add-expense-modal.tsx`
- `client/src/components/edit-expense-modal.tsx`
- `client/src/pages/dashboard.tsx`

### Payment Methods
Edit payment method options in the same modal files to add or modify payment types.

## Troubleshooting

### Database Connection Issues
1. Verify MySQL is running: `mysql -u username -p`
2. Check database exists: `SHOW DATABASES;`
3. Verify connection string format
4. Check firewall settings for MySQL port (3306)

### Build Issues
1. Clear node_modules: `rm -rf node_modules && npm install`
2. Clear build cache: `npm run clean`
3. Check Node.js version: `node --version` (should be 18+)

### Migration Issues
1. Check database permissions
2. Run: `npm run db:generate` then `npm run db:push`
3. Manually create database if needed

## License

MIT License - see LICENSE file for details.