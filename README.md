# FriendSync - Schedule Coordination App

## Overview

FriendSync is a real-time, responsive web application designed to help users effortlessly coordinate schedules with friends, family, or colleagues. By creating and joining groups, users can set their own availability and instantly check who is free at any given time. The application is built with a modern tech stack, featuring a Supabase backend for real-time data synchronization and authentication.

---

## 🚀 Live Demo

You can launch the live application here:

**[FRIENDSYNC APPLICATION](https://friendsync123.netlify.app/)**

---

## ✨ Features

* **Google Authentication:** Secure and easy sign-in using Google accounts.
* **Multi-Group Management:**
    * Create new, uniquely named groups.
    * Join existing groups using a group ID.
    * Be a member of multiple groups simultaneously.
    * A dedicated dashboard to view and switch between your groups.
* **Interactive Timetable:**
    * A visual, grid-based schedule for all days of the week.
    * Custom 50-minute time slots (e.g., 08:00 - 08:50).
    * Click and drag to easily select multiple busy slots.
* **Real-Time Availability Checker:**
    * Select a day and time to instantly see which friends in the current group are available.
    * The availability list updates in real-time as other users save their schedules.
* **Live Group Member List:**
    * View a list of all members in the currently selected group.
    * The member list updates in real-time as users join or leave the group.
* **Responsive Design:** A clean, modern UI that works seamlessly on desktop, tablet, and mobile devices.

---

## 🛠️ Tech Stack

This project is built with a modern, efficient, and scalable tech stack.

### Frontend

* **HTML5:** The standard markup language for creating the structure of the web page.
* **Tailwind CSS:** A utility-first CSS framework used for rapid UI development. It allows for building a clean, responsive, and highly customizable design directly in the markup without writing custom CSS.
* **Vanilla JavaScript (ES6 Modules):** The core logic of the application is written in modern, plain JavaScript. Key features used include:
    * **DOM Manipulation:** To dynamically create and update the timetable, group lists, and availability results.
    * **Event Handling:** To manage user interactions like clicks, drags, and form submissions.
    * **Async/Await:** To handle asynchronous calls to the Supabase backend gracefully.
    * **ES6 Modules:** To organize the code into a clean and maintainable structure.

### Backend (Platform: Supabase)

Supabase provides a suite of open-source tools that act as a comprehensive backend-as-a-service.

* **Authentication:** User sign-in is handled securely through Supabase Auth, which is integrated with **Google OAuth** as a third-party provider. This means users can log in with their Google accounts without the app needing to manage passwords.
* **Postgres Database:** A powerful, open-source object-relational database. In this project, it is used to store all application data, including:
    * `profiles`: Stores user information linked to their authentication ID.
    * `groups`: Contains the list of all created groups.
    * `group_memberships`: A linking table to manage which users belong to which groups.
    * `schedules`: Stores the availability data for each user within a specific group, using the `JSONB` data type for flexible schedule structures.
* **Realtime Subscriptions:** This is a key feature of Supabase that allows the frontend to subscribe to changes in the database. When a user saves their schedule or joins a group, the database sends a message to all connected clients in that group, who then automatically update their UI without needing to refresh the page.
* **Row Level Security (RLS):** A critical security feature of Postgres that is enabled on all tables. RLS ensures that users can only access and modify data that they are explicitly permitted to. For example, a user can only view the schedules of groups they are a member of and can only update their own schedule.

---

## ⚙️ Setup and Installation

To run this project locally or deploy it, you will need a Supabase project.

### 1. Supabase Project Setup

1.  Go to [supabase.com](https://supabase.com) and create a new project.
2.  Inside your project, navigate to the **SQL Editor** and run the following SQL commands to create the necessary tables:

    ```sql
    -- Create a table for user profiles
    CREATE TABLE profiles (
      id UUID PRIMARY KEY REFERENCES auth.users(id) ON DELETE CASCADE,
      full_name TEXT
    );
    
    -- Create a table for groups
    CREATE TABLE groups (
      id TEXT PRIMARY KEY,
      created_by UUID REFERENCES auth.users(id) ON DELETE SET NULL,
      created_at TIMESTAMPTZ DEFAULT NOW()
    );
    
    -- Create a table for group memberships
    CREATE TABLE group_memberships (
      group_id TEXT REFERENCES groups(id) ON DELETE CASCADE,
      user_id UUID REFERENCES auth.users(id) ON DELETE CASCADE,
      PRIMARY KEY (group_id, user_id)
    );
    
    -- Create a table for schedules (one per user per group)
    CREATE TABLE schedules (
      user_id UUID REFERENCES auth.users(id) ON DELETE CASCADE,
      group_id TEXT REFERENCES groups(id) ON DELETE CASCADE,
      schedule JSONB,
      PRIMARY KEY (user_id, group_id)
    );
    ```

3.  **Enable Google Authentication:**
    * Go to **Authentication -> Providers** in your Supabase dashboard.
    * Enable the **Google** provider and follow the instructions to add your OAuth credentials.
4.  **Set up Row Level Security (RLS):** This is a **critical** step for security.
    * Go to **Authentication -> Policies** for each of the tables (`profiles`, `groups`, `group_memberships`, `schedules`).
    * Enable RLS for each table.
    * Add the necessary policies to allow users to create, read, and manage their own data securely. *Refer to the development history for the specific policies required for this application to function.*

### 2. Frontend Configuration

1.  Clone or download the `index.html` file.
2.  Open the file and find the following constants at the top of the `<script type="module">` tag:

    ```javascript
    const SUPABASE_URL = 'YOUR_SUPABASE_URL'; 
    const SUPABASE_ANON_KEY = 'YOUR_SUPABASE_ANON_KEY';
    ```

3.  Replace the placeholder values with your own Supabase Project URL and `anon` public key. You can find these in your Supabase project's **Settings -> API** page.
4.  Open the `index.html` file in your browser to run the application.
