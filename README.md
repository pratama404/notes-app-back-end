
# 📒 Notes App - Deployment with Node.js & EC2

Simple Notes App project with a **Frontend** and **Backend** architecture. Backend is deployed on an AWS EC2 instance using Node.js and PM2. Frontend provided by Dicoding Academy.

---

## 🚀 Project Links

- **Frontend**: [http://notesapp-v1.dicodingacademy.com](http://notesapp-v1.dicodingacademy.com)  
- **Backend (EC2 Public IP)**: [http://18.142.227.89:5000](http://18.142.227.89:5000)  

**⚠️ Notes:** Saat mengakses frontend melalui [http://notesapp-v1.dicodingacademy.com](http://notesapp-v1.dicodingacademy.com), disarankan menggunakan browser **non-Chromium** seperti Firefox untuk mempermudah pengujian dan menghindari potensi cache atau CORS issue.

---

## 🗂️ Project Structure

### Backend
- Source Code: [https://github.com/pratama404/notes-app-back-end](https://github.com/pratama404/notes-app-back-end)
- Tech Stack:
  - [Hapi.js](https://hapi.dev/) (`@hapi/hapi` ^21.4.0)
  - [NanoID](https://github.com/ai/nanoid) (`nanoid` ^3.3.11)
  - [PM2](https://pm2.keymetrics.io/) for production process management

### Frontend
- Docker Image:
  ```bash
  docker run --rm -p 8080:8080 dicodingacademy/notes-app-frontend:v1
  ```
- Source Code (ZIP):
  [https://github.com/dicodingacademy/notes-app-frontend/archive/refs/heads/v1.zip](https://github.com/dicodingacademy/notes-app-frontend/archive/refs/heads/v1.zip)

---

## 🖥️ Backend Deployment Steps (EC2)

1. **SSH into EC2**
   ```bash
   ssh -i <your-key.pem> ubuntu@<EC2-PUBLIC-IP>
   ```

2. **Install Node.js**
   ```bash
   curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
   sudo apt install -y nodejs
   node -v
   ```

3. **Install PM2 globally**
   ```bash
   sudo npm install -g pm2
   ```

4. **Clone Backend Repo**
   ```bash
   git clone https://github.com/pratama404/notes-app-back-end.git
   cd notes-app-back-end
   npm install
   ```

5. **Run with PM2**
   ```bash
   pm2 start server.js --name notes-app
   pm2 save
   ```

6. **Allow Security Group Port (EC2)**
   - Open port `5000` in EC2 Security Groups for public access.

7. **Access Backend**
   - [http://18.142.227.89:5000](http://18.142.227.89:5000)

---

## 🌐 Frontend Quick Run (Local Machine)

1. **Run Frontend via Docker**
   ```bash
   docker run --rm -p 8080:8080 dicodingacademy/notes-app-frontend:v1
   ```

2. **Access Frontend**
   - [http://localhost:8080](http://localhost:8080)

3. **Change API Endpoint (Optional)**
   - Ensure the frontend is pointing to your deployed backend (`http://18.142.227.89:5000`) if needed.

---

## 📌 Notes

- Ensure your EC2 instance has:
  - Opened port `5000` for API access
  - SSH and HTTP permissions set in Security Groups
- PM2 keeps your Node.js server running after logout or reboot

---

## 🎯 Future Improvements

- Add domain with NGINX reverse proxy
- SSL setup with Let's Encrypt
- CI/CD pipeline for automated deployment

---

## 🙌 Credits

- Dicoding Academy - Frontend Template  
- [Hapi.js](https://hapi.dev/), [NanoID](https://github.com/ai/nanoid), [PM2](https://pm2.keymetrics.io/)
