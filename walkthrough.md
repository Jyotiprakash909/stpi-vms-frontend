# STPI VMS Project Setup & Walkthrough

The **STPI Smart Visitor Management System** has been fully implemented with a Backend (Node/Express), Web Frontend (React/Vite), and Mobile App (React Native/Expo).

## Project Structure
*   `backend/`: Node.js server with Express and MongoDB, serving the API and static photo uploads.
*   `frontend/`: React + Vite web application using Tailwind CSS for styling. It contains the Visitor Entry, Exit Portal, and Admin Dashboard.
*   `mobile-app/`: React Native Expo application for employees to approve/reject requests.

---

## 🚀 Setup & Running Instructions

### 1. Database Setup
Ensure you have **MongoDB** installed and running locally on port `27017` (`mongodb://127.0.0.1:27017`). The database name will be `stpi_vms`.

### 2. Backend API
1.  Open a terminal and navigate to the backend directory:
    ```bash
    cd backend
    ```
2.  Install dependencies (if not already done):
    ```bash
    npm install
    ```
3.  Seed the dummy employees to the database:
    ```bash
    node seed.js
    ```
4.  Start the backend server:
    ```bash
    node index.js
    ```
    *(The server will run on port 5000)*

### 3. Web Frontend (Admin & Visitor Portals)
1.  Open a new terminal and navigate to the frontend directory:
    ```bash
    cd frontend
    ```
2.  Install dependencies (if not already done):
    ```bash
    npm install
    ```
3.  Start the Vite development server:
    ```bash
    npm run dev
    ```
4.  Open the provided localhost URL (usually `http://localhost:5173`) in your browser to access the system:
    *   **Home:** `/`
    *   **Visitor Entry:** `/visitor/entry`
    *   **Exit System:** `/visitor/exit`
    *   **Admin Dashboard:** `/admin`

### 4. Mobile App (Employee)
1.  Open a new terminal and navigate to the mobile app directory:
    ```bash
    cd mobile-app
    ```
2.  **IMPORTANT:** Find your local network IP address (e.g., `192.168.1.xxx`). Open `mobile-app/App.js` and change the `API_BASE` variable at line `7` to point to your computer's IP address where the backend is running.
    ```javascript
    const API_BASE = 'http://192.168.1.xxx:5000/api';
    ```
3.  Start the Expo development server:
    ```bash
    npx expo start
    ```
4.  To test on your physical Android device, download the **Expo Go** app from the Play Store and scan the QR code generated in the terminal.

---

## 📱 Feature Walkthrough

> [!TIP]
> **End-to-End Test Flow:**
> 1. Start all 3 servers.
> 2. Open the **Web Frontend** and go to **Visitor Entry**. Fill out the form and upload a photo. The screen will say "Request Pending".
> 3. Open the **Mobile App**, select the employee you chose in the form. You will see the pending request.
> 4. In the app, tap the request, optionally type a message, and tap **Approve**.
> 5. The Web Frontend will automatically poll and update to show "Approved" with the message.
> 6. Open the **Admin Dashboard** in a new tab to see the live record.
> 7. Finally, go to the **Exit System** and enter the visitor's phone number to complete the check-out!

### Key Features Implemented
*   **Visitor Entry:** Full capture including photos (saved via Multer to local disk). Real-time auto-polling to wait for approval.
*   **Exit Portal:** One-input simple form to mark an active visit as completed by phone number.
*   **Admin Dashboard:** Real-time (auto-refreshing) view of all visitors. Clean table layout with Search and Filter capabilities.
*   **Mobile App:** Custom selection logic. Beautiful review modal with photo view, details, and message input.
