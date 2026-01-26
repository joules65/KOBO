# XeniaPay - Modern Banking Platform

XeniaPay is a comprehensive financial management platform built with Next.js, enabling users to manage their bank accounts, track transactions, and make seamless payments across Africa.

## 🚀 Features

- **Multi-Bank Integration**: Connect multiple bank accounts via Plaid
- **Real-time Balance Tracking**: View account balances across all connected banks
- **Transaction Management**: Track and categorize all your transactions
- **Payment Transfers**: Send money between accounts using Dwolla
- **Secure Authentication**: Email/password authentication with Appwrite
- **Responsive Design**: Mobile-first design that works on all devices
- **Real-time Updates**: Automatic page updates with Next.js Server Components
- **Error Monitoring**: Integrated Sentry for production error tracking

## 🛠️ Tech Stack

- **Framework**: [Next.js 14.2.3](https://nextjs.org/) (App Router)
- **Language**: TypeScript
- **Styling**: Tailwind CSS
- **UI Components**: shadcn/ui
- **Authentication**: Appwrite
- **Banking Integration**: Plaid API
- **Payment Processing**: Dwolla
- **Error Tracking**: Sentry
- **Form Handling**: React Hook Form + Zod
- **Charts**: Chart.js

## 📋 Prerequisites

Before you begin, ensure you have:

- Node.js 18+ installed
- npm or yarn package manager
- Accounts created for:
  - [Appwrite Cloud](https://cloud.appwrite.io)
  - [Plaid](https://plaid.com)
  - [Dwolla](https://www.dwolla.com)
  - [Sentry](https://sentry.io) (optional, for error tracking)

## ⚙️ Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/david-ac1/XENIAPAY.git
   cd xeniaPay
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Set up environment variables**
   
   Create a `.env` file in the root directory and add the following:

   ```env
   #NEXT
   NEXT_PUBLIC_SITE_URL=http://localhost:3000

   #APPWRITE
   NEXT_PUBLIC_APPWRITE_ENDPOINT=https://cloud.appwrite.io/v1
   NEXT_PUBLIC_APPWRITE_PROJECT=your_project_id
   APPWRITE_DATABASE_ID=your_database_id
   APPWRITE_USER_COLLECTION_ID=your_user_collection_id
   APPWRITE_BANK_COLLECTION_ID=your_bank_collection_id
   APPWRITE_TRANSACTION_COLLECTION_ID=your_transaction_collection_id
   NEXT_APPWRITE_KEY=your_api_key

   #PLAID
   PLAID_CLIENT_ID=your_client_id
   PLAID_SECRET=your_secret
   PLAID_ENV=sandbox
   PLAID_PRODUCTS=auth,transactions,identity
   PLAID_COUNTRY_CODES=US,CA

   #DWOLLA
   DWOLLA_KEY=your_key
   DWOLLA_SECRET=your_secret
   DWOLLA_BASE_URL=https://api-sandbox.dwolla.com
   DWOLLA_ENV=sandbox
   ```

## 🗄️ Appwrite Setup

### 1. Create a new project in Appwrite

### 2. Create a Database with the following collections:

#### **Users Collection**
Create attributes:
- `userId` (String, Required, Size: 2000)
- `email` (Email, Required)
- `firstName` (String, Required, Size: 100)
- `lastName` (String, Required, Size: 100)
- `address1` (String, Required, Size: 100)
- `city` (String, Required, Size: 100)
- `state` (String, Required, Size: 1000)
- `postalCode` (String, Required, Size: 10)
- `dateOfBirth` (String, Required, Size: 100)
- `ssn` (String, Required, Size: 2000)
- `dwollaCustomerId` (String, Optional, Size: 2000)
- `dwollaCustomerUrl` (String, Optional, Size: 2000)

#### **Banks Collection**
Create attributes:
- `userId` (String, Required, Size: 2000)
- `bankId` (String, Required)
- `accountId` (String, Required)
- `accessToken` (String, Required)
- `fundingSourceUrl` (String, Optional)
- `shareableId` (String, Required)

#### **Transactions Collection**
Create attributes as needed for transaction tracking

### 3. Create an API Key
- Go to Settings → API Keys
- Create a new key with scopes: `databases.*`, `users.*`, `sessions.*`
- Copy the key to `NEXT_APPWRITE_KEY` in `.env`

### 4. Disable Email Verification (Optional for Development)
- Go to Auth → Settings
- Disable email verification for faster testing

## 🏃 Running the Application

### Development Mode
```bash
npm run dev
```
Visit [http://localhost:3000](http://localhost:3000)

### Production Build
```bash
npm run build
npm start
```

## 📱 Usage

1. **Sign Up**: Create a new account with your details
2. **Link Bank Account**: Use Plaid to connect your bank account
3. **View Dashboard**: See your balance and recent transactions
4. **Make Transfers**: Send money to other accounts
5. **Track Transactions**: View your complete transaction history

## 🐛 Common Issues & Troubleshooting

### "Project is archived" Error
- The Appwrite project needs to be unarchived in the Appwrite Console

### "No session" Error
- User is not logged in - redirect to sign-in page
- Session cookie may have expired

### "Invalid query: Attribute not found in schema"
- Ensure all collection attributes are created in Appwrite
- Check that attribute names match exactly

### User redirected to sign-in after successful login
- User document not created in database
- Delete the Appwrite account and sign up again
- Or manually create the user document with matching `userId`

### Build fails with Sentry error
- Ensure Sentry org name matches your token
- Update `org` in `next.config.mjs` to match your Sentry organization

## 📂 Project Structure

```
xeniaPay/
├── app/
│   ├── (auth)/              # Authentication pages
│   │   ├── sign-in/
│   │   └── sign-up/
│   ├── (root)/              # Protected routes
│   │   ├── page.tsx         # Dashboard
│   │   ├── my-banks/        # Bank accounts page
│   │   ├── payment-transfer/ # Transfer money
│   │   └── transaction-history/ # Transaction history
│   ├── api/                 # API routes
│   └── globals.css          # Global styles
├── components/              # React components
│   └── ui/                  # shadcn/ui components
├── lib/
│   ├── actions/             # Server actions
│   │   ├── user.actions.ts
│   │   ├── bank.actions.ts
│   │   ├── transaction.actions.ts
│   │   └── dwolla.actions.ts
│   ├── appwrite.ts          # Appwrite client
│   ├── plaid.ts             # Plaid client
│   └── utils.ts             # Utility functions
├── constants/               # App constants
└── types/                   # TypeScript type definitions
```

## 🔒 Security

- All API keys stored in environment variables
- HTTP-only cookies for session management
- Secure communication with banking APIs
- Data encryption for sensitive information

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👨‍💻 Author

**David**
- GitHub: [@david-ac1](https://github.com/david-ac1)

## 🙏 Acknowledgments

- Plaid for banking integration
- Dwolla for payment processing
- Appwrite for backend services
- shadcn/ui for beautiful components

---

Made with ❤️ for seamless payments across Africa
