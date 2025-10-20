# **Leave Request Application – Power Apps | SharePoint | Power Automate**

### 📘 **Overview**
This project is a **Leave Request Management System** built using  
**Microsoft Power Apps**, **SharePoint**, and **Power Automate**.

It allows employees to apply for leave digitally, and managers to approve or reject requests  
and HR to monitor everything in one centralized location — eliminating manual tracking and emails.

<img width="825" height="461" alt="Screenshot 2025-10-20 104210" src="https://github.com/user-attachments/assets/ad68acf8-8b56-43ce-bb2c-f2b3c77312be" />
<img width="820" height="465" alt="Screenshot 2025-10-20 104250" src="https://github.com/user-attachments/assets/afd44ced-a146-4ef2-8d71-2e3b7c32f590" />
<img width="814" height="462" alt="Screenshot 2025-10-20 104333" src="https://github.com/user-attachments/assets/8713e73a-b89f-4a78-b5a2-c06e72d1a0eb" />



---

## 🧩 **Project Architecture**

| Layer | Technology Used | Purpose |
|:------|:----------------|:---------|
| 🖥️ **Frontend** | Power Apps | User interface for employees and managers |
| 🗂️ **Database** | SharePoint List | Stores all leave data and approval statuses |
| ⚙️ **Automation** | Power Automate | Handles workflow logic, email notifications, and approvals |

---

## 🧱 **1. SharePoint Setup**

Created a **SharePoint List** titled **`LeaveRequests`** with the following schema:

| Column Name | Type | Description |
|--------------|------|-------------|
| EmployeeName | Single line of text | Name of the employee applying for leave |
| EmployeeEmail | Single line of text | Used for email notifications |
| ManagerEmail | Person or Group | Manager responsible for approval |
| LeaveType | Choice | Sick, Casual, Earned, etc. |
| StartDate | Date | Leave start date |
| EndDate | Date | Leave end date |
| Reason | Multiple lines of text | Reason for requesting leave |
| Status | Choice | *Pending*, *Approved*, *Rejected* |
| Comments | Multiple lines of text | Manager’s remarks |

🗃️ This SharePoint list acts as the **data backbone** for the Power Apps application.

---

## 🎨 **2. Power Apps Development**

The app was developed in **Power Apps** using a **3-screen layout** and **modern UI components**.

### 🏠 **Home Screen**
- Two main buttons:
  - 📝 **Apply Leave**
  - 📄 **View Applications**
- Used `Navigate()` for smooth screen transitions with animations like `ScreenTransition.Cover`.
- Context passed between screens using `{SelectedItem: Gallery1.Selected}`.

---

### 🧾 **Apply Leave Screen**
- Connected directly to the **SharePoint `LeaveRequests` list**.
- Implemented form logic using:
  - `NewForm()` and `EditForm()` – to toggle between create/edit modes  
  - `SubmitForm()` – to submit data to SharePoint  
  - `Notify()` – to show success/error messages  
- Added input validation using `IsBlank()` to ensure all required fields are filled before enabling the **Submit** button.
- The **Submit button** triggers Power Automate to start the approval flow once a record is created.

---

### 👀 **View Applications Screen**
- Displays existing requests using a **Gallery control** bound to the SharePoint list.
- Managers can:
  - Select a record to open in edit mode.
  - Approve or reject leave requests.
- Used:
  - `Gallery.Selected` → to capture selected record.
  - `EditForm()` → to update records.
  - `Patch()` → to modify specific fields (e.g., Status or Comments).

---

## 🔁 **3. Power Automate Flow**

Created a **Power Automate Flow** triggered by new items added to the SharePoint list.

### ⚙️ **Flow Steps**
1. **Trigger:**  
   `When an item is created` in **LeaveRequests**.
2. **Condition:**  
   If *Status = Pending*, send an **approval email** to the manager.
3. **Approval Email:**  
   Sent via the Outlook connector — includes:
   - Employee details (Name, Type, Dates, Reason)
   - Quick actions: ✅ Approve / ❌ Reject
4. **Manager Action:**  
   - Updates the *Status* and *Comments* fields automatically in SharePoint.
5. **Employee Notification:**  
   - Sends an automatic email update confirming whether the request was approved or rejected.

✅ This ensures **real-time communication** and eliminates manual follow-ups.

---

## 🛠️ **Skills & Technologies**
**Power Apps** · **SharePoint Lists** · **Power Automate** · **App Design** · **Workflow Automation** · **UI/UX Design** · **Data Validation**

--

## 🎯 **Project Highlights**
- 🔹 Fully automated leave approval process  
- 🔹 Dynamic connection between Power Apps, SharePoint, and Power Automate  
- 🔹 Clean, responsive UI using modern containers and controls  
- 🔹 Real-time email notifications and centralized HR dashboard  


---

