# FinSafe — User Guide

Welcome to FinSafe — a personal finance assistant that uses AI to help you track spending, plan budgets, and reach savings goals. This guide explains how to use the app's features in everyday language, privacy notes, and quick troubleshooting steps.
## Who this guide is for

This is a user-facing manual for non-developers: people who will open the app, sign in, add transactions, upload receipts, ask the AI for advice, and manage budgets and goals.
## Quick start (using the web app)

1. Open the app in your browser. If hosting locally the developer may provide a URL (e.g. `http://localhost:3000`).

## Live demo

You can try the public live site at: https://finsafe-ai.netlify.app

If the site is down or you prefer to run locally, follow the Quick start steps above.
## Main features & how to use them

Dashboard — your overview
- Where to find it: Click "Dashboard" in the main navigation.
- What it shows: Monthly overview (income vs spending), net worth, recent transactions, and quick cards for budgets and goals.
- How to use: Scan the Monthly Overview to see if spending is within your budget. Click a recent transaction to edit or delete it.
SpendSpy — add expenses from receipts
- Where to find it: "SpendSpy" in navigation.
- What it does: Upload or drag-and-drop a photo of a receipt. AI extracts merchant, date, amount, and category and creates a transaction automatically.
Budgets (BudgetBot)
- Where to find it: "Budget Bot" or Budgets card on the dashboard.
- What it does: Create monthly budgets for categories (e.g., Food, Transportation). Track progress with a visual bar.
GoalGuru — savings goals
- Where to find it: "Goal Guru" or the Savings Goals card.
- What it does: Let you set savings goals (amount, deadline). Track progress and get AI tips.
AdvisorAI — ask questions and get advice
- Where to find it: Floating chat button (bottom-right) or Advisor AI page.
- What it does: Ask natural-language financial questions. AI reads your transaction and budget data (if you allow) and answers in plain language.
Crisis Guardian — emergency planning
- Where to find it: Crisis Guardian page.
- What it does: Scans for financial stress signals (e.g., sudden big expenses, overdrafts) and suggests steps to stabilize finances.
Transactions — add, edit, delete
- Where to find it: Recent Transactions card or Transactions page.
- How to add:
Settings — personalization
- Profile: Update name, preferred currency, and monthly income.
- Notifications: Turn on smart reminders or daily digest emails.
Help & Support
- Where to find it: Help & Support page.
- Contents: FAQ, contact options (email), and troubleshooting guides.
## Privacy & security (important)

- Your account: Your data (transactions, budgets, goals) is stored under your account and protected by Firebase Authentication.
## Common troubleshooting

- "I uploaded a receipt but the details are wrong": Review and correct the fields before saving. If parsing repeatedly fails, try a clearer photo or type the transaction manually.
## Tips & best practices

- Add receipts regularly to keep budgets accurate.
## Contact & feedback

If you find bugs or want to request features, use the Help & Support page to contact the team or open an issue in the project repository.

---

If you'd like this guide exported as a short PDF or printed help card for onboarding new users, I can generate that next.

## Tech Stack

- **Framework**: [Next.js](https://nextjs.org/) (App Router)
- **UI Components**: [ShadCN UI](https://ui.shadcn.com/)
- **Styling**: [Tailwind CSS](https://tailwindcss.com/)
- **Backend & Database**: [Firebase](https://firebase.google.com/) (Firestore & Authentication)
- **Generative AI**: [Genkit](https://firebase.google.com/docs/genkit) (Powered by Google's Gemini models)
- **Charts**: [Recharts](https://recharts.org/)
- **Forms**: [React Hook Form](https://react-hook-form.com/) & [Zod](https://zod.dev/)

---

## Core Features

### 1. Secure Authentication & Personalization

-   **Why it's important**: Security and personalization are the bedrock of a trustworthy financial app. FinSafe ensures that each user's sensitive data is private and that the experience is tailored to their individual needs. It supports both traditional email/password and convenient Google Sign-In.
-   **How to use it**:
    -   **Sign-Up**: New users can create an account on the "Sign Up" page. Upon their first login, FinSafe automatically creates a secure profile in the database, setting default values for their region and currency, which can be updated later.
    -   **Login**: Existing users can securely access their accounts through the "Login" page.
    -   **Onboarding**: The app creates a private and secure space for each user, ensuring all their financial data is stored securely in Firestore, accessible only by them.

### 2. The Dashboard (`/dashboard`)

-   **Why it's important**: The dashboard is the user's financial "command center," offering a comprehensive, at-a-glance overview of their financial health. It consolidates critical information, making it easy to spot trends, track progress, and make informed decisions.
-   **How it works**:
    -   **Monthly Overview Card**: This card provides a real-time snapshot of the current month's finances, including Total Income, Total Spending, Savings Rate, and Net Flow (the difference between income and spending). A dynamic bar chart visualizes spending across different categories.
    -   **Net Worth Card**: This card tracks the user's overall financial position by combining their "Current Assets" (from their profile) with the total amount saved in their goals. A smooth area chart illustrates how their net worth has trended over time.
    -   **Recent Transactions Card**: This card lists the most recent transactions for quick review. From here, users can also manually add, edit, or delete an expense.

### 3. SpendSpy (`/spend-spy`)

-   **Why it's important**: Manual expense tracking is often tedious and error-prone. SpendSpy automates this process using the power of AI, making it effortless to maintain accurate and up-to-date financial records.
-   **How to use it**:
    1.  Navigate to the **SpendSpy** page.
    2.  Simply drag and drop an image of a receipt onto the upload area, or click to browse for the file.
    3.  The `recordExpense` Genkit flow instantly sends the image to an AI model, which intelligently extracts the merchant name, date, total amount, and category.
    4.  The extracted details are used to automatically create and save a new transaction, which is immediately reflected in the "Recent Transactions" list across the app.

### 4. BudgetBot (`/budget-bot`)

-   **Why it's important**: Budgeting is the cornerstone of financial control. BudgetBot elevates this by providing AI-driven insights. It helps users create realistic, category-specific budgets that align with their income, spending habits, and long-term goals.
-   **How it works**:
    -   **Budgets Card**: Users can create, view, edit, and delete their budgets. For each budget, a progress bar provides a clear visual of how much has been spent against the defined limit for a specific category.
    -   **BudgetBot AI**: By clicking **"Generate My Budget"**, the user triggers the `getPersonalizedBudget` Genkit flow. This AI analyzes the user's income, assets, recent transactions, and savings goals to generate a recommended monthly budget, intelligently broken down by category. This provides a concrete, personalized spending plan to help the user stay on track.

### 5. GoalGuru (`/goal-guru`)

-   **Why it's important**: Long-term financial goals can often feel abstract and out of reach. GoalGuru makes these goals tangible by visualizing progress and providing AI-powered motivation and actionable advice, helping users stay focused and accelerate their journey.
-   **How it works**:
    -   **Savings Goals Card**: Users can add, view, edit, and delete their savings goals (e.g., "Vacation Fund," "New Car"). Each goal prominently displays the target amount, current amount saved, a progress bar, and the time remaining if a deadline is set.
    -   **GoalGuru AI**: By clicking **"Get Goal-Hacking Tips"**, the user triggers the `getGoalAdvice` Genkit flow. The AI analyzes the user's complete financial picture—income, expenses, and goals—to generate a list of personalized, actionable tips designed to help them cut costs and save more effectively.

### 6. AdvisorAI (Floating Chat & `/advisor-ai`)

-   **Why it's important**: Financial questions can arise at any moment. AdvisorAI serves as an on-demand financial expert, accessible from anywhere in the app via a floating chat button. It provides instant, context-aware answers based on the user's live financial data.
-   **How to use it**:
    -   Click the floating chat button in the bottom-right corner or navigate to the dedicated **AdvisorAI** page. The chat interface is optimized for both desktop and mobile, appearing as a full-screen sheet on smaller devices for a better user experience.
    -   Ask questions in plain English, such as "How much did I spend on food last week?" or "Am I on track to meet my savings goals?"
    -   The `advisorAIWeeklySummary` Genkit flow accesses the user's live transactions, budgets, and goals from Firestore to provide an instant, data-driven answer, all within the context of their chosen region and currency.

### 7. Crisis Guardian (`/crisis-guardian`)

-   **Why it's important**: Financial emergencies are stressful and can be overwhelming. Crisis Guardian acts as a proactive AI safety net, helping users identify early signs of financial distress and providing a calm, actionable plan to get back on track.
-   **How it works**:
    -   On the **Crisis Guardian** page, the user can click **"Analyze for Financial Stress"**.
    -   The `getCrisisSupport` Genkit flow analyzes recent transactions for anomalies, such as a sudden large expense or consistent overspending relative to budgets.
    -   If a stress event is detected, the AI responds with an empathetic message and a step-by-step recovery plan. This might include suggestions like temporarily pausing a savings goal or adjusting a budget.
    -   Users can also add **Emergency Contacts** on this page, creating a quick-access list of trusted individuals to call in times of need.

### 8. User Profile & Settings (`/settings`)

-   **Why it's important**: Personalization and control are paramount. The settings page empowers users to manage the data that fuels the app's powerful insights.
-   **How to use it**:
    -   Navigate to the **Settings** page via the user menu in the header.
    -   **Profile Information**: Update first name, last name, monthly income, and total assets.
    -   **Localization**: Choose a **Region** and **Currency** from a list of options. This ensures that all monetary values and AI responses throughout the app are formatted correctly for the user.
    -   **Notifications**:
        -   Enable **Smart Reminders** to receive AI-powered alerts based on spending activity.
        -   Enable the **Daily Digest** and choose a specific time of day to receive a notification with a summary of the day's financial activity and a motivational quote.
    -   All changes are saved directly to the user's document in Firestore, ensuring that every AI-driven insight is always based on the most current information.

### 9. Help & Support (`/help-support`)

-   **Why it's important**: A good support system is key to user confidence. This page acts as a central hub for assistance and information.
-   **How it works**:
    -   **FAQ**: An accordion-style list of frequently asked questions provides instant answers to common queries about using the app.
    -   **Contact Us**: A simple link allows users to send an email directly to the support team for feedback or questions.
    -   **Meet the Developers**: A section dedicated to crediting the talented individuals who built the application.