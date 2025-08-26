FriendSync - Schedule Coordination App
Overview
FriendSync is a real-time, responsive web application designed to help users effortlessly coordinate schedules with friends, family, or colleagues. By creating and joining groups, users can set their own availability and instantly check who is free at any given time. The application is built with a modern tech stack, featuring a Supabase backend for real-time data synchronization and authentication.

🚀 Features
Google Authentication: Secure and easy sign-in using Google accounts.

Group Management:

Create new, uniquely named groups.

Join existing groups using a group ID.

Be a member of multiple groups simultaneously.

A dedicated dashboard to view and switch between your groups.

Interactive Timetable:

A visual, grid-based schedule for all days of the week.

Custom 50-minute time slots (e.g., 08:00 - 08:50).

Click and drag to easily select multiple busy slots.

Real-Time Availability Checker:

Select a day and time to instantly see which friends in the current group are available.

The availability list updates in real-time as other users save their schedules.

Group Member List:

View a list of all members in the currently selected group.

The member list updates in real-time as users join or leave the group.

Responsive Design: A clean, modern UI that works seamlessly on desktop, tablet, and mobile devices.

🛠️ Tech Stack
Frontend:

HTML5

Tailwind CSS: For utility-first styling and responsive design.

Vanilla JavaScript (ES6 Modules): For all client-side logic and interactivity.

Backend:

Supabase:

Authentication: Manages user sign-in via Google OAuth.

Postgres Database: Stores all user, group, and schedule data.

Realtime Subscriptions: Powers the live updates for schedules and group memberships.

Row Level Security (RLS): Secures the database to ensure users can only access data they are permitted to see.

⚙️ Setup and Installation
To run this project locally or deploy it, you will need a Supabase project.

1. Supabase Project Setup
Go to supabase.com and create a new project.

Inside your project, navigate to the SQL Editor and run the following SQL commands to create the necessary tables:

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

Enable Google Authentication:

Go to Authentication -> Providers in your Supabase dashboard.

Enable the Google provider and follow the instructions to add your OAuth credentials.

Set up Row Level Security (RLS): This is a critical step for security.

Go to Authentication -> Policies for each of the tables (profiles, groups, group_memberships, schedules).

Enable RLS for each table.

Add the necessary policies to allow users to create, read, and manage their own data securely. Refer to the development history for the specific policies required for this application to function.

2. Frontend Configuration
Clone or download the index.html file.

Open the file and find the following constants at the top of the <script type="module"> tag:

const SUPABASE_URL = 'YOUR_SUPABASE_URL'; 
const SUPABASE_ANON_KEY = 'YOUR_SUPABASE_ANON_KEY';

Replace the placeholder values with your own Supabase Project URL and anon public key. You can find these in your Supabase project's Settings -> API page.

Open the index.html file in your browser to run the application.
