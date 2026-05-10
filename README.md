# 🎓 ClassLink - Ցուցակային Համակարգ

A comprehensive web-based attendance management system with Python utilities for data analysis and export.

## 📋 Features

### Web Application (HTML/JavaScript)
- **Student Portal**
  - Sign up and login (restricted to school area)
  - Mark attendance (Present/Absent)
  - View attendance history
  - See class schedule with time periods
  - Display classroom information (e.g., 10-A, 11-B)
  - Geolocation-based access and attendance (500m school radius)

- **Teacher Portal**
  - Sign up and login (requires admin approval)
  - View student attendance records
  - Manage multiple classes
  - View teaching subject information
  - Access reports and statistics

- **Admin Panel**
  - Secret 3-click access (click 🔐 icon)
  - Password protected (`admin123`)
  - Student and teacher management
  - Attendance overview
  - Data export (CSV with UTF-8 encoding)
  - System statistics and controls

### Python Utilities

#### 1. **classlink_export.py** - Data Export Tool
Export ClassLink data to CSV files with proper UTF-8 encoding (no weird characters)

```bash
python classlink_export.py
```

**Exports:**
- Students list (Name, Email, Grade, Classroom, Created Date)
- Teachers list (Name, Email, Subject, Approval Status)
- Attendance records (Student, Email, Date, Time, Status, Grade)

#### 2. **classlink_analysis.py** - Data Analysis & Visualization
Analyze attendance data using pandas and create matplotlib visualizations

```bash
python classlink_analysis.py
```

**Generates:**
- Summary statistics (total students, teachers, attendance rate)
- Attendance by grade analysis
- Student attendance percentages
- 3 visualization charts:
  - Overall attendance pie chart
  - Attendance by grade bar chart
  - Individual student attendance bar chart
- CSV analysis report

#### 3. **classlink_manager.py** - Database Management Utility
Interactive CLI tool for managing the ClassLink database

```bash
python classlink_manager.py
```

**Features:**
- View statistics
- List/add/delete students
- List/add/delete/approve teachers
- View attendance records
- Clear database (with confirmation)

---

## 🚀 How to Use

### Web Application
1. Open `classlink.html` in a web browser
2. Choose your role (Student/Teacher)
3. Sign up or login
4. **For Students:**
   - Select your grade and classroom
   - Allow location access for geolocation-based attendance
   - Mark attendance within school radius (500m)
   - View attendance history and schedule
5. **For Teachers:**
   - Provide your subject
   - (Requires admin approval)
   - View your class attendance records
6. **For Admin:**
   - Click 🔐 icon 3 times
   - Enter password: `admin123`
   - Manage all system functions

### Python Scripts

#### Export Data to CSV
```bash
python classlink_export.py
```
Creates a `classlink_exports/` folder with timestamped CSV files

#### Analyze Data & Create Charts
```bash
python classlink_analysis.py
```
Creates a `classlink_analysis/` folder with:
- `attendance_pie_chart.png`
- `attendance_by_grade.png`
- `student_attendance_chart.png`
- `analysis_report_*.csv`

#### Manage Database
```bash
python classlink_manager.py
```
Interactive menu to manage students, teachers, and records

---

## 📊 Time Periods

The system uses the following class schedule:
- **1st Period:** 08:15 - 09:00
- **2nd Period:** 09:05 - 09:50
- **3rd Period:** 09:55 - 10:40
- **4th Period:** 10:50 - 11:35

Students can mark attendance during any period they're present.

---

## 🔐 Security

### Passwords
- **Admin Password:** `admin123` (change in code if needed)
- **Student/Teacher Passwords:** User-defined (minimum 6 characters)
- All passwords stored in browser's localStorage

### Geolocation
- Students can only mark attendance within 500m of school
- School coordinates: `40.164191260202706, 44.445792211026216`
- Must enable browser location services

### Hidden Admin Access
- No admin button on home page
- Click the 🔐 icon in top-right corner 3 times
- Password required for access

---

## 📁 Data Structure

```json
{
  "students": [
    {
      "name": "Student Name",
      "email": "student@example.com",
      "password": "password123",
      "grade": "10",
      "classRoom": "10-A",
      "createdAt": "2024-01-01T10:00:00.000Z"
    }
  ],
  "teachers": [
    {
      "name": "Teacher Name",
      "email": "teacher@example.com",
      "password": "password123",
      "subject": "Mathematics",
      "approved": false,
      "createdAt": "2024-01-01T10:00:00.000Z"
    }
  ],
  "attendance": [
    {
      "student": "student@example.com",
      "date": "01/01/2024",
      "time": "08:30:45 AM",
      "status": "PRESENT",
      "grade": "10"
    }
  ]
}
```

---

## 🛠️ Configuration

### Change School Location
Edit `classlink.html` and find:
```javascript
SCHOOL_LOCATION: { lat: 40.164191260202706, lng: 44.445792211026216 },
ALLOWED_RADIUS: 500 // meters
```

### Change Admin Password
Edit `classlink.html` and find:
```javascript
ADMIN_PASSWORD: 'admin123'
```

### Change Teacher Password (for login verification)
Edit `classlink.html` and find:
```javascript
TEACHER_PASSWORD: 'teacher123'
```

---

## 📋 CSV Export Format

All CSV files are exported with:
- ✓ UTF-8 encoding (no weird characters)
- ✓ UTF-8 BOM for Excel compatibility
- ✓ Armenian text support
- ✓ Proper field escaping for special characters

### Student CSV
| Անուն | Էլ. փոստ | Դասարան | Դասասենյակ | Ստեղծման ամսաթիվ |
|-------|---------|---------|-----------|-----------------|

### Teacher CSV
| Անուն | Էլ. փոստ | Առարկա | Հաստատված | Ստեղծման ամսաթիվ |
|-------|---------|--------|----------|-----------------|

### Attendance CSV
| Աշակերտ | Էլ. փոստ | Ամսաթիվ | Ժամանակ | Կարգավիճակ | Դասարան |
|--------|---------|--------|---------|-----------|----------|

---

## 📊 Python Dependencies

Install required packages:
```bash
pip install pandas matplotlib
```

---

## 🐛 Troubleshooting

### CSV Files Have Weird Characters
- ✓ Fixed in Python scripts with UTF-8 encoding and BOM
- ✓ Use the Python export scripts instead of the web interface

### Attendance Won't Mark
- Check if you're within school location radius
- Enable location services in browser
- Try with a different browser

### Charts Not Generating
- Ensure matplotlib and pandas are installed
- Check that `classlink_data.json` file exists
- Run with Python 3.6+

### Admin Panel Won't Open
- Click the 🔐 icon exactly 3 times
- Wait for the password modal
- Default password is `admin123`

---

## 📝 Notes

- All data is stored in browser's localStorage (web app) or JSON files (Python)
- Data persists even after closing the browser
- Admin can export and backup data regularly
- Python scripts can be scheduled with cron/Task Scheduler for automated analysis

---

## 📄 License

ClassLink - Educational Attendance Management System
Created for school attendance tracking and analysis.

---

## 📞 Support

For issues or questions, refer to the code comments or modify settings as needed.

**Last Updated:** 2024
e comments or modify settings as needed.

**Last Updated:** 2024
