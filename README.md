live at (https://nkpfinance.netlify.app/)
Customer Management Application
Overview
The Customer Management Application is a web-based tool designed to manage customer payment data over a 15-week period, with support for overdue payments extending up to 30 weeks. Built using HTML, CSS, JavaScript, and Firebase, it allows administrators to track customer payments, add or delete customers, manage admin accounts, and view deleted data. The application features a responsive interface with a sidebar for navigation, search functionality, and real-time data updates using Firebase Realtime Database.
Features

Authentication: Secure admin login using Firebase Authentication.
Customer Management:
Add, delete, and update customer records in "15 Weeks" and "Over Due 15 Weeks" sections.
Track payments across 16 weeks for regular customers and 30 weeks for overdue customers.
Calculate pending amounts dynamically based on net amount and weekly payments.
Move customers to "Over Due 15 Weeks" when a payment is entered for Week 16.


Deleted Data: View and clear deleted customer records for both "15 Weeks" and "Over Due 15 Weeks".
Search Functionality:
Main search bar to filter customers in the "15 Weeks" section by name.
Sidebar search to locate customers across both "15 Weeks" and "Over Due 15 Weeks" sections, with row highlighting.


Real-Time Updates: Sync data with Firebase Realtime Database for seamless updates across users.
Responsive Design: Mobile-friendly interface with a collapsible sidebar and modal confirmations.
Admin Management: Add and remove admin accounts (local list, with Firebase Authentication for user creation).

Prerequisites

Firebase Account: Required for authentication and real-time database.
Web Browser: Modern browsers like Chrome, Firefox, or Edge.
Internet Connection: For Firebase integration and CDN dependencies.
Node.js and npm (optional): For local development with a static server.

Setup Instructions

Clone the Repository:
git clone <repository-url>
cd customer-management


Configure Firebase:

Create a Firebase project at Firebase Console.
Enable Firebase Authentication (Email/Password provider) and Realtime Database.
Copy your Firebase project configuration (apiKey, authDomain, databaseURL, etc.).
Update the firebaseConfig object in index.html with your Firebase credentials:const firebaseConfig = {
    apiKey: "your-api-key",
    authDomain: "your-auth-domain",
    databaseURL: "your-database-url",
    projectId: "your-project-id",
    storageBucket: "your-storage-bucket",
    messagingSenderId: "your-messaging-sender-id",
    appId: "your-app-id"
};




Project Structure:
customer-management/
├── index.html        # Main HTML file with UI structure
├── script.js         # JavaScript logic for functionality
├── styles.css        # CSS styles for UI
└── README.md         # This file


Serve the Application:

Option 1: Local Server:Install a local server like http-server:npm install -g http-server
http-server .

Access the app at http://localhost:8080.
Option 2: Firebase Hosting:Deploy to Firebase Hosting for production:firebase init hosting
firebase deploy


Option 3: Open Directly:Open index.html in a browser (note: some features may be limited due to CORS without a server).


Firebase Database Rules:

Set up Realtime Database rules to secure data access. Example:{
  "rules": {
    ".read": "auth != null",
    ".write": "auth != null"
  }
}


Adjust rules based on your security requirements.



Usage

Login:

Enter admin email and password in the login form.
Credentials must be registered in Firebase Authentication.


Navigation:

Use the sidebar (toggle via hamburger menu) to switch between:
Manage Admins: Add or delete admin accounts.
15 Weeks: View and manage customer payments for 16 weeks.
Over Due 15 Weeks: Manage overdue customers (weeks 17–30).
Deleted Data: View or clear deleted customer records.
Add Customer: Form to add new customers to the "15 Weeks" section.
Search Customers: Search and highlight customers across sections.




Customer Management:

Add Customer: Fill the form in the "Add Customer" section (Start Date, City, Name, Net Amount, Return Amount).
Edit Payments: Click on Net Amount or Week cells to edit (confirm overwrites via modal).
Delete Customer: Click the "Delete" button in the action column to move to deleted data.
Week 16 Action: Entering a Week 16 amount prompts moving the customer to "Over Due 15 Weeks".
Search: Use the main search bar for "15 Weeks" customers or sidebar search for all customers.


Deleted Data:

View deleted customers in "15 Weeks Deleted Data" or "Over Due 15 Weeks Deleted Data".
Use "Delete All" buttons to permanently clear deleted data.


Logout: Click the logout option to return to the login screen.


Table Structure

15 Weeks Table (22 columns):

#, Start Date, City, Name, Net Amount, Return Amount, Weeks 1–16, Pending Amount, Action (Delete).
Editable: Net Amount, Weeks 1–16.
Pending Amount: Net Amount - Sum(Weeks 1–15).


Over Due 15 Weeks Table (36 columns):

#, Start Date, City, Name, Net Amount, Return Amount, Weeks 1–16 (disabled), Weeks 17–30 (editable), Pending Amount, Action (Delete).
Editable: Net Amount, Weeks 17–30.
Pending Amount: Net Amount - Sum(Weeks 1–16).


Deleted 15 Weeks Table (21 columns):

#, Start Date, City, Name, Net Amount, Return Amount, Weeks 1–16, Pending Amount.
Read-only.


Deleted Over Due 15 Weeks Table (35 columns):

#, Start Date, City, Name, Net Amount, Return Amount, Weeks 1–30, Pending Amount.
Read-only.



Dependencies

Firebase SDK (v10.12.2):
Firebase App: Core initialization.
Firebase Authentication: User login and admin creation.
Firebase Realtime Database: Real-time data storage and updates.


Loaded via CDN in index.html.

Notes

Firebase Configuration: Replace placeholder firebaseConfig values with your actual Firebase project details.
Security: Ensure Firebase Authentication and Database rules are configured to prevent unauthorized access.
Browser Compatibility: Tested on modern browsers. Use a local server for full functionality.
Limitations:
Admin deletion is local-only (Firebase user deletion requires additional API setup).
No data validation beyond sanitization; add client-side validation if needed.


Responsive Design: Sidebar collapses on mobile; use hamburger menu to toggle.

Troubleshooting

Login Errors:
"Invalid email or password": Check Firebase Authentication credentials.
"Firebase not initialized": Verify firebaseConfig in index.html.


Table Display Issues:
Misaligned columns: Ensure index.html table headers match script.js column counts.
Action column missing: Check CSS (styles.css) for display: none on table cells.


Data Not Updating:
Verify Firebase Realtime Database rules allow read/write for authenticated users.
Check browser console for Firebase errors.



Contributing
Contributions are welcome! Please:

Fork the repository.
Create a feature branch (git checkout -b feature/your-feature).
Commit changes (git commit -m "Add your feature").
Push to the branch (git push origin feature/your-feature).
Open a pull request.

License
This project is licensed under the MIT License.
