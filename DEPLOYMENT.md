# Local Deployment Guide

## Quick Setup for Local Development

### Prerequisites
- Node.js 18+
- MySQL 5.7+ or MySQL 8.0+
- Git

### Step 1: Clone and Install
```bash
git clone <your-repo-url>
cd expense-tracker
npm install
```

### Step 2: Database Setup

#### Option A: Local MySQL
```bash
# Create database
mysql -u root -p
CREATE DATABASE expense_tracker;
exit
```

#### Option B: Docker MySQL
```bash
docker run --name expense-tracker-mysql \
  -e MYSQL_ROOT_PASSWORD=password123 \
  -e MYSQL_DATABASE=expense_tracker \
  -p 3306:3306 \
  -d mysql:8.0
```

### Step 3: Environment Configuration
```bash
cp .env.example .env
```

Edit `.env` with your MySQL details:
```env
DATABASE_URL=mysql://root:password123@localhost:3306/expense_tracker
NODE_ENV=development
PORT=5000
```

### Step 4: Database Migration
```bash
npm run db:push
```

### Step 5: Start Application
```bash
npm run dev
```

Application runs at: http://localhost:5000

## Production Deployment

### Build for Production
```bash
npm run build
```

### Environment Variables for Production
```env
DATABASE_URL=mysql://user:password@production-host:3306/expense_tracker
NODE_ENV=production
PORT=5000
```

### Start Production Server
```bash
npm start
```

## Database Connection Examples

### Local Development
```env
DATABASE_URL=mysql://root:password@localhost:3306/expense_tracker
```

### Cloud MySQL (PlanetScale, AWS RDS, etc.)
```env
DATABASE_URL=mysql://user:password@host.region.rds.amazonaws.com:3306/expense_tracker
```

### With SSL
```env
DATABASE_URL=mysql://user:password@host:3306/expense_tracker?ssl=true
```

## Troubleshooting

### MySQL Connection Issues
1. Check MySQL is running: `mysql -u root -p`
2. Verify database exists: `SHOW DATABASES;`
3. Check port is open: `netstat -an | grep 3306`

### Build Issues
```bash
rm -rf node_modules package-lock.json
npm install
npm run build
```

### Database Migration Issues
```bash
npm run db:generate
npm run db:push
```

## Application Features

- **Dashboard**: Expense overview with charts
- **Expense Management**: Add, edit, delete expenses
- **Reports**: Payment method analysis with CSV export
- **Recycle Bin**: Restore deleted expenses
- **Dark Mode**: Theme switching with font size options
- **Currency**: Indian Rupee (₹) support