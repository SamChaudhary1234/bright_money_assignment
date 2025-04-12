# 🌟 BrightLend: Modern Credit & Loan Management

**A Next-Gen Financial Platform**  
Powered by Django + Celery + Redis

---

## 🛠️ Quick Start Guide

### Environment Setup
```bash
# 1. Navigate to project
cd bright_credit

# 2. Initialize virtual environment
python3 -m venv venv
source venv/bin/activate

# 3. Install dependencies
pip install -r requirements.txt
Database Configuration
bash
Copy
# Run migrations
python manage.py makemigrations
python manage.py migrate

# (Optional) Load sample data
python manage.py loaddata initial_data.json
Service Initialization
bash
Copy
# Start Django server (port 8001)
python manage.py runserver 8001

# Launch Redis (macOS)
brew services start redis

# Start Celery workers
celery -A bright_credit worker --loglevel=info
⏰ Automated Billing System
Daily Cron Job Implementation
Manually trigger billing cycle:

python
Copy
from loan.tasks import process_daily_billing
process_daily_billing.delay()  # Async execution
📊 Data Integration
Transaction File Requirements
/user_transactions.csv expected in root directory:

csv
Copy
user_id,transaction_date,amount,type,description
BC-USER-001,2025-03-15,250000,CREDIT,SALARY
BC-USER-001,2025-03-18,50000,DEBIT,LOAN_EMI
🔌 API Reference
User Onboarding
Endpoint: POST /api/v1/users/register
Request:

json
Copy
{
  "aadhar_id": "888877776666",
  "name": "Rahul Sharma",
  "email": "rahul@brightlend.com",
  "annual_income": 1800000,
  "employment_type": "SALARIED"
}
Response:

json
Copy
{
  "user_id": "BC-USER-009",
  "welcome_message": "Account activated successfully",
  "initial_credit_score": 720
}
Credit Assessment
Endpoint: GET /api/v1/credit/scores?user_id=BC-USER-009
Response:

json
Copy
{
  "score": 720,
  "factors": {
    "payment_history": "EXCELLENT",
    "credit_utilization": "LOW_RISK",
    "credit_age": "GOOD"
  }
}
Loan Services
1. Application
POST /api/v1/loans/apply

json
Copy
{
  "user_id": "BC-USER-009",
  "product": "PERSONAL_LOAN",
  "amount": 500000,
  "tenure_months": 24,
  "purpose": "HOME_RENOVATION"
}
2. Payment Processing
POST /api/v1/loans/payments

json
Copy
{
  "loan_id": "LN-2025-0456",
  "amount": 24500,
  "payment_method": "UPI",
  "reference_id": "PAY-789XYZ"
}
Account Statements
Endpoint: GET /api/v1/statements?loan_id=LN-2025-0456
Response:

json
Copy
{
  "loan_summary": {
    "principal_paid": 125600,
    "interest_paid": 45600,
    "outstanding": 374400
  },
  "payment_history": [
    {
      "due_date": "2025-04-05",
      "status": "PAID",
      "breakdown": {
        "principal": 20833,
        "interest": 3667
      }
    }
  ]
}
