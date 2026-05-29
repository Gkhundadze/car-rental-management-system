````md
# DriveOps
## Car Rental Management System

საგანმანათლებლო პროექტი Vanilla JavaScript-ის, LocalStorage-ის, Authentication-ის, Authorization-ის და CRUD ოპერაციების შესასწავლად.

---

# პროექტის შესახებ

DriveOps არის სასწავლო პროექტი, რომლის მიზანია სტუდენტებმა შექმნან მანქანების გაქირავების პლატფორმის ლოგიკა სუფთა JavaScript-ის გამოყენებით.

პროექტის UI უკვე მზადაა (HTML + CSS), ხოლო სტუდენტების მთავარი ამოცანაა JavaScript-ის საშუალებით აამუშაონ:

- ავტორიზაცია
- რეგისტრაცია
- როლების მართვა
- CRUD ოპერაციები
- დინამიური UI
- LocalStorage მონაცემთა ბაზა
- Session Management
- JSON მონაცემების დამუშავება
- Classes და Methods

პროექტი სრულად მუშაობს Backend-ის გარეშე და გამოიყენებს მხოლოდ:

- localStorage
- sessionStorage
- Vanilla JavaScript
- Fetch API

---

# სასწავლო მიზნები

ამ პროექტზე მუშაობით სტუდენტები ისწავლიან:

- DOM Manipulation
- Event Handling
- Dynamic Rendering
- CRUD Operations
- Authentication
- Authorization
- Role-Based Access Control
- LocalStorage Database Simulation
- Session Management
- Classes in JavaScript
- Class Methods
- Fetch API
- JSON Parsing
- Data Modeling
- Array Methods
- Modular Architecture
- UI State Management
- Form Validation
- Conditional Rendering

---

# ტექნოლოგიური სტეკი

| ტექნოლოგია | გამოყენება |
|---|---|
| HTML5 | Semantic Markup |
| CSS3 | Layout & Styling |
| Vanilla JavaScript | Application Logic |
| LocalStorage API | Database Simulation |
| SessionStorage API | Session Management |
| Fetch API | External JSON Data |
| BEM | CSS Methodology |

---

# პროექტის როლები

აპლიკაციაში არსებობს 3 ტიპის მომხმარებელი:

---

## Guest

არ არის ავტორიზებული მომხმარებელი.

შეუძლია:

- მანქანების ნახვა
- მანქანების ძებნა
- ფილტრაცია

არ შეუძლია:

- მანქანის დამატება
- რედაქტირება
- წაშლა
- Booking

---

## User

ავტორიზებული მომხმარებელი.

შეუძლია:

- Login / Logout
- Favorite მანქანების შენახვა
- Booking Simulation
- საკუთარი პროფილის ნახვა

არ შეუძლია:

- მანქანის დამატება
- მანქანის წაშლა
- მანქანის რედაქტირება

---

## Admin

ადმინისტრატორი.

შეუძლია:

- ახალი მანქანის დამატება
- მანქანის რედაქტირება
- მანქანის წაშლა
- მანქანის სტატუსის შეცვლა
- ყველა მანქანის მართვა

---

# მთავარი დავალება

თქვენი მიზანია ააწყოთ სრულად ფუნქციონალური JavaScript ლოგიკა არსებული UI დიზაინისთვის.

---

# Initial Data Loading

პროექტის დაწყებისას localStorage ცარიელი იქნება.

თქვენი ამოცანაა:

- GitHub-ის raw JSON ლინკიდან წამოიღოთ მანქანების საწყისი მონაცემები
- მიღებული მონაცემები შეინახოთ localStorage-ში
- მონაცემები ჩაიტვირთოს მხოლოდ პირველ გაშვებაზე

---

# JSON Data Source

მოგეცემათ GitHub raw JSON URL მსგავსი ფორმატით:

```txt
https://raw.githubusercontent.com/USERNAME/REPOSITORY/main/cars.json
````

---

# აუცილებელი მოთხოვნა

❗ Fetch უნდა შესრულდეს მხოლოდ მაშინ, როცა localStorage-ში cars არ არსებობს.

მაგალითი:

```js
if (!localStorage.getItem("cars")) {
  // fetch initial data
}
```

---

# Fetch API

აუცილებელია Fetch API-ის გამოყენება.

მაგალითი:

```js
const response = await fetch(url);
const data = await response.json();
```

---

# მნიშვნელოვანი წესი

❗ HTML-ის static მანქანის ბარათები არ უნდა დარჩეს.

ყველა მანქანა უნდა render-დებოდეს JavaScript-ის საშუალებით localStorage-დან წამოღებული მონაცემებით.

---

# მონაცემთა ბაზა

პროექტი გამოიყენებს browser localStorage-ს როგორც მონაცემთა ბაზას.

---

# აუცილებელი Classes

პროექტში სავალდებულოა ორი custom class-ის გამოყენება:

* User
* Car

---

# User Class

User class გამოიყენება მომხმარებლის ობიექტების შესაქმნელად.

---

## აუცილებელი Properties

* id
* name
* email
* password
* role
* favorites
* createdAt

---

## აუცილებელი Methods

### getFullInfo()

აბრუნებს მომხმარებლის სრულ ინფორმაციას string ფორმატში.

---

### addFavorite(carId)

ამატებს favorite მანქანას.

---

### removeFavorite(carId)

შლის favorite მანქანას.

---

### isAdmin()

ამოწმებს არის თუ არა admin.

---

## მაგალითი

```js
class User {
  constructor(name, email, password, role = "user") {
    this.id = crypto.randomUUID();
    this.name = name;
    this.email = email;
    this.password = password;
    this.role = role;
    this.favorites = [];
    this.createdAt = Date.now();
  }

  getFullInfo() {
    return `${this.name} (${this.email})`;
  }

  addFavorite(carId) {
    this.favorites.push(carId);
  }

  removeFavorite(carId) {
    this.favorites = this.favorites.filter(
      id => id !== carId
    );
  }

  isAdmin() {
    return this.role === "admin";
  }
}
```

---

# Car Class

Car class გამოიყენება მანქანის ობიექტების შესაქმნელად.

---

## აუცილებელი Properties

* id
* brand
* model
* pricePerDay
* image
* transmission
* fuel
* seats
* available
* featured
* createdAt

---

## აუცილებელი Methods

### toggleAvailability()

ცვლის მანქანის availability სტატუსს.

---

### toggleFeatured()

ცვლის featured სტატუსს.

---

### getDisplayName()

აბრუნებს მანქანის სრულ სახელს.

---

### applyDiscount(percent)

ფასს აკლებს მითითებული პროცენტით.

---

## მაგალითი

```js
class Car {
  constructor(
    brand,
    model,
    pricePerDay,
    image,
    transmission,
    fuel,
    seats
  ) {
    this.id = crypto.randomUUID();
    this.brand = brand;
    this.model = model;
    this.pricePerDay = pricePerDay;
    this.image = image;
    this.transmission = transmission;
    this.fuel = fuel;
    this.seats = seats;
    this.available = true;
    this.featured = false;
    this.createdAt = Date.now();
  }

  toggleAvailability() {
    this.available = !this.available;
  }

  toggleFeatured() {
    this.featured = !this.featured;
  }

  getDisplayName() {
    return `${this.brand} ${this.model}`;
  }

  applyDiscount(percent) {
    this.pricePerDay =
      this.pricePerDay -
      (this.pricePerDay * percent) / 100;
  }
}
```

---

# LocalStorage სტრუქტურა

## users

```js
[
  {
    id,
    name,
    email,
    password,
    role,
    favorites,
    createdAt
  }
]
```

---

## cars

```js
[
  {
    id,
    brand,
    model,
    pricePerDay,
    image,
    transmission,
    fuel,
    seats,
    available,
    featured,
    createdAt
  }
]
```

---

## session

```js
{
  id,
  name,
  email,
  role
}
```

---

# აუცილებელი ფუნქციონალი

## 1. Authentication System

### Register

მომხმარებელს უნდა შეეძლოს:

* რეგისტრაცია
* email uniqueness validation
* password validation

ვალიდაცია:

* ყველა ველი სავალდებულოა
* email უნდა იყოს სწორი ფორმატის
* password მინიმუმ 8 სიმბოლო
* password უნდა შეიცავდეს:

  * დიდ ასოს
  * ციფრს
  * სპეციალურ სიმბოლოს

---

### Login

მომხმარებელს უნდა შეეძლოს:

* სისტემაში შესვლა
* session-ის შექმნა sessionStorage-ში

---

### Logout

Logout უნდა:

* წაშალოს session
* დააბრუნოს მომხმარებელი guest მდგომარეობაში

---

## 2. Dynamic Car Rendering

ყველა მანქანა უნდა render-დებოდეს JavaScript-ით.

აუცილებელია:

* map()
* template literals
* dynamic DOM rendering

❌ აკრძალულია hardcoded HTML cards.

---

## 3. Add Car (Admin Only)

მხოლოდ admin-ს შეუძლია:

* ახალი მანქანის დამატება

ფორმა უნდა შეიცავდეს:

* brand
* model
* image
* price
* transmission
* fuel
* seats

submit-ის შემდეგ:

* შეიქმნას ახალი Car instance
* დაემატოს localStorage-ში
* UI ავტომატურად განახლდეს

---

## 4. Edit Car (Admin Only)

Admin-ს უნდა შეეძლოს:

* არსებული მანქანის რედაქტირება

აუცილებელია:

* ფორმის prefill
* update logic
* localStorage update
* UI refresh

---

## 5. Delete Car (Admin Only)

Admin-ს უნდა შეეძლოს მანქანის წაშლა.

აუცილებელია:

* confirm() გამოყენება
* localStorage update
* UI refresh

---

## 6. Authorization Logic

❗ მხოლოდ button-ის დამალვა საკმარისი არ არის.

ლოგიკაშიც უნდა არსებობდეს role verification.

მაგალითი:

```js
if(currentUser.role !== "admin") {
   return;
}
```

---

## 7. Conditional UI Rendering

სისტემამ უნდა მართოს:

* guest view
* user view
* admin view

UI უნდა იცვლებოდეს session-ის მიხედვით.

---

## 8. Search Functionality

მომხმარებელს უნდა შეეძლოს:

* მანქანის ძებნა brand/model-ის მიხედვით

---

## 9. Filter Functionality

აუცილებელი ფილტრები:

* transmission
* fuel
* available only

---

## 10. Favorites System

მომხმარებელს უნდა შეეძლოს:

* favorite მანქანების დამატება
* favorite მანქანების წაშლა

---

# რეკომენდებული ფაილების სტრუქტურა

```txt
driveops/
│
├── index.html
├── style.css
├── data/
│   └── cars.json
│
├── js/
│   ├── app.js
│   ├── auth.js
│   ├── cars.js
│   ├── storage.js
│   ├── ui.js
│   ├── validators.js
│   ├── User.js
│   └── Car.js
│
└── README.md
```

---

# აკრძალულია

❌ Inline onclick
❌ Inline styles
❌ Hardcoded cards
❌ ერთი დიდი app.js ფაილი
❌ Global variable chaos

---

# სავალდებულოა

✅ addEventListener()
✅ Dynamic rendering
✅ localStorage persistence
✅ sessionStorage session
✅ Fetch API
✅ JSON parsing
✅ მინიმუმ 2 class
✅ Class methods
✅ Validation
✅ Authorization checks
✅ Clean code structure

---

# Bonus Challenges

სურვილისამებრ:

* Dark Mode
* Booking System
* Activity Logs
* Session Expiry
* Toast Notifications
* Pagination
* Sort by Price
* Admin Dashboard Analytics
* Skeleton Loading
* Fake API Simulation
* Recently Viewed Cars

---

# Seed Admin Account

თუ localStorage ცარიელია, ავტომატურად შეიქმნას:

```txt
Email: admin@driveops.com
Password: Admin123!
Role: admin
```

---

# Submission Checklist

✅ JSON მონაცემები იტვირთება GitHub raw URL-დან
✅ Fetch სრულდება მხოლოდ პირველ გაშვებაზე
✅ Register მუშაობს
✅ Login მუშაობს
✅ Session ინახება
✅ Logout მუშაობს
✅ Cars render-დება JavaScript-ით
✅ Admin შეუძლია Add/Edit/Delete
✅ User ვერ შლის მანქანას
✅ Authorization მუშაობს
✅ Validation მუშაობს
✅ localStorage სწორად გამოიყენება
✅ Classes გამოყენებულია
✅ Class methods მუშაობს
✅ Console errors არ არსებობს
✅ UI refresh-ის შემდეგ მონაცემები რჩება

---

# უსაფრთხოების მნიშვნელოვანი შენიშვნა

ეს პროექტი შექმნილია მხოლოდ საგანმანათლებლო მიზნებისთვის.

რეალურ აპლიკაციაში:

* პაროლები არასოდეს ინახება plain text-ად
* localStorage არ გამოიყენება sensitive data-სთვის
* Authentication ხდება backend-ზე
* Password-ები ინახება hash-ირებულად

ეს პროექტი გასწავლით:

* application architecture
* data flow
* authentication concepts
* authorization logic
* CRUD operations

და არა production-ready security სისტემის აგებას.

```
```
