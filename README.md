# 🍏 Juice Processing & Packaging System

A **full-stack application** for managing juice processing and packaging operations.  
The system streamlines everything from customer entry to final pickup — with optional integrations for industrial printers and SMS notifications.

---

## 🛠 Tech Stack

- **Backend**: Node.js + Express  
- **Frontend**: React (with Vite)  
- **Database**: AWS RDS (PostgreSQL/MySQL)  
- **Notifications**: AWS SNS (SMS)  
- **Containerization**: Docker & Docker Compose  

---

## 📊 Features & Pages

### Default login page
- Use "employee123" default password to login the system
- The password could be changed in the setting page
<img width="1465" height="888" alt="login page" src="https://github.com/user-attachments/assets/c278dc8a-91e3-4562-89fe-a500da730852" />



### 1. Dashboard
- Displays production statistics, line productivity, and recent activity.
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/9c106ee7-1a85-4208-a704-70da84d48fcf" />

### 2. Customer Info Entry
- Record customer details and apple weight.  
- Auto-calculates juice quantity, pouch count, and price (based on city).  
- Optional notes for special cases.  
- Generates **crate QR codes** based on employee input.
<img width="1470" height="913" alt="customer entry" src="https://github.com/user-attachments/assets/c8acc37b-6f8b-4735-b2d9-7a54541292ed" />


### 3. Crate Management
- Employees scan crate QR codes once apples are ready.  
- Order status updates automatically.  
- Moves to *Juice Processing* once all crates are scanned.
<img width="1470" height="956" alt="create handle" src="https://github.com/user-attachments/assets/e7f50107-2f9e-45a0-957a-ea005287c72f" />


### 4. Juice Processing
- Shows orders ready for juice extraction and pouch filling.  
- Generates **Box QR codes** and sends to printer.  
- Sends **Customer Name + Expiry Date** to the Videojet industrial printer.  
- Employees mark orders as *done* after processing, labeling, and packing.
<img width="1470" height="956" alt="juice station" src="https://github.com/user-attachments/assets/1091419a-03c9-41c6-92a3-eeb5942745bf" />


### 5. Load Boxes → Pallet
- Each pallet has its own QR code (holds up to **4 boxes**).  
- Employees scan box QR codes, then assign them to pallets.  
- Pallets can be moved to storage, even in different cities.
- If the customer origin of the box is Kuopio, then scan the shelf QR codes immediately 
<img width="1470" height="956" alt="box scan" src="https://github.com/user-attachments/assets/024251a2-3f86-4936-bffe-e11f50ccd005" />


### 6. Load Pallet → Shelf
- Each shelf has its own QR code (holds **1 pallet**).  
- Employees scan pallet → shelf.  
- System automatically sends an **SMS notification** to the customer when their order is shelved.
<img width="1470" height="956" alt="shelve scan" src="https://github.com/user-attachments/assets/6f5c116b-a2de-4878-876c-438d926e37a3" />


### 7. Pickup Coordination
- Search by **customer name** or **phone number**.  
- System shows which shelf contains the order.  
- Employees mark orders as *picked up* once collected.
<img width="1470" height="956" alt="pick up search" src="https://github.com/user-attachments/assets/6760ef0a-8bae-4fe4-bb9a-93ee2922141b" />
<img width="1470" height="956" alt="mark as done" src="https://github.com/user-attachments/assets/8a797c9c-cc4d-433b-9a76-0bca872f441f" />


### 8. Settings (Admin Only)
- Admin password ("admin123") required for every change.  
- Manage system-wide configuration securely.
- Edit SMS notification template
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/33cc01bd-bf90-4270-95d6-3eb5ae52953e" />

### 9. Customer Management
- Allows viewing, editing, and removing existing customer records.
- Use the admin password to delete any customers -> to prevent employee misbehaviors.
<img width="1468" height="462" alt="Customer management" src="https://github.com/user-attachments/assets/4feb0fc5-3fa5-497e-9f41-92c158d36a6c" />



### 10. SMS Notification
- After the boxes are scanned onto the shelf, an SMS is received by the customer to pick up the order.
![sms notice](https://github.com/user-attachments/assets/d96b67c5-42e4-4182-b782-e085ec867936)

### 11. SMS Notification
- Used Videojet 6330 printer for the Printing of pouches.
- This printer uses the Zypher communication with TCP.
![Videojet 6330](https://github.com/user-attachments/assets/197ce254-c678-4951-b188-02857051e96e)

---

## 🐳 Docker Setup

Clone the repository:

```bash
git clone https://github.com/vincentbui21/SmartJuiceSystem.git
cd SmartJuiceSystem
```
Build and start containers:

```bash
docker compose up --build
```
Access the apps:

```bash
Frontend (Vite) → http://localhost:5173
Backend (API) → http://localhost:5001
```
Stop containers:

```bash
docker compose down
```
⚙️ Environment Variables (Optional)
You can create a .env file in the backend folder to configure optional features like AWS SNS:
```env
# AWS SNS configuration
AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
SNS_TOPIC_ARN=
AWS_REGION=
DEFAULT_SMS_COUNTRY_CODE=+358
```
These are entirely optional. The system will work fully without them — SMS notifications and auto-label printing will simply be disabled.
👉 If AWS SNS or the industrial printer aren’t available, the system still works — just without SMS and auto-printing.

---
## 🔄 Workflow Summary
1. Login: Use the employee account (employee / employee123) to access the system.
2. Add a New Customer: Enter customer details → generate crate QR codes.
3. Crate Scanning: Scan crates → order moves to juice processing.
4. Juice Processing: Fill pouches → generate box QR codes → send to printer (optional).
5. Load Boxes → Pallet: Scan boxes → assign to pallets.
6. Load Pallet → Shelf: Scan pallets → assign to shelves → SMS notification sent (if configured).
7. Pickup Coordination: Search by customer → mark orders as picked up.

---
## ⚠️ Notes
The system is fully functional even without:

* Industrial printer → no auto-label printing
* AWS SNS → no SMS notifications

Alternative database setups are supported (local PostgreSQL/MySQL).

## 🗃️Database Setup

Before running the backend, the database will be automatically initialized by Docker using the files in Database/.
Optional: You can replace AWS RDS with any local PostgreSQL/MySQL instance if preferred.
