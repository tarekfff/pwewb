# Installation Guide
Recommended IDE Setup
VSCode + Volar (and disable Vetur).

Customize configuration
See Vite Configuration Reference.
## Frontend Setup

1. use git or download here directly:
   git clone https://github.com/tarekfff/pwewb.git
   cd pwewb


Install dependencies:
npm install

The frontend will run at: http://localhost:5173/  anoter port if you are change it, you can see the port in cmd space


Backend Setup

git clone https://github.com/tarekfff/pweb-backend.git
cd pweb-backend

Database Setup
Install XAMPP or any MySQL database tool

Configure your MySQL connection in pweb-backend/index.js:

const db = mysql.createConnection({
  host: 'localhost',
  port: 3309,
  user: 'root',       // Your MySQL username
  password: '',       // Your MySQL password
  database: 'test'    // Your database name
});


Start the backend server (from pweb-backend directory):
node index.js

Start the frontend server (from pwewb directory):
npm run dev
Access the application at: http://localhost:5173/




for help use tlgram : @trkAyo
or ask chatgpt

![image](https://github.com/user-attachments/assets/c8497d21-9724-4a0a-84bd-088d1ad0d961)

![image](https://github.com/user-attachments/assets/64c2f282-98c2-4656-9821-0c329c1a9764)

