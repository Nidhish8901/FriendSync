# FriendSync - Coordinate Schedules with Friends

FriendSync is a real-time web application designed to make scheduling
and coordinating with friends, family, or teammates effortless. It
eliminates the back-and-forth of finding a common time to meet by
providing a shared, visual timetable. Users can create and join groups,
set their availability, and instantly see when everyone is free.

## Key Features

-   **Google Authentication**: Secure and easy sign-in using Google
    accounts, handled by Supabase Auth.
-   **Group Management**:
    -   Create & Join: Users can create new private groups with a unique
        ID or join existing ones.
    -   Dashboard: A central dashboard to view and navigate between all
        joined groups.
    -   Leave Group: Easily leave a group directly from the dashboard.
-   **Global Schedule**: Set your schedule once! Your availability is
    saved globally and applied across all the groups you are a part of.
-   **Real-Time Syncing**: Schedules and group memberships update in
    real-time for all members within a group, powered by Supabase
    Realtime subscriptions.
-   **Versatile Schedule Input**:
    -   Manual Timetable: A visual, interactive timetable where users
        can click and drag to mark their busy hours.
    -   ICS File Import/Export: Quickly import your schedule from any
        calendar app (like Google Calendar, Outlook) by uploading an
        .ics file. You can also download your FriendSync schedule as an
        .ics file.
-   **Advanced Availability Checking**:
    -   Who's Free?: Pick a specific day and time to see a list of all
        friends in the group who are available.
    -   Find Common Slots: Select multiple friends and a day to
        instantly find all the time slots when everyone selected is
        free.
-   **Responsive Design**: A mobile-first design that ensures a seamless
    experience on any device, from smartphones to desktops.
-   **Invite Friends**: A simple "Invite" button that copies a
    pre-formatted message with the group ID and a link to the app,
    making it easy to share.

## Tech Stack

-   Frontend: HTML5, CSS3, Modern JavaScript (ES Modules)
-   Backend-as-a-Service (BaaS): Supabase
-   Authentication: Manages user sign-ins via Google OAuth.
-   PostgreSQL Database: Stores user profiles, groups, and schedules.
-   Realtime Subscriptions: Provides real-time updates for schedules and
    group memberships.
-   Styling: Tailwind CSS for a utility-first, responsive design.
-   Calendar Parsing: ical.js for parsing .ics file uploads.
-   Deployment: The application is built to be deployed on any static
    hosting platform like Netlify, Vercel, or GitHub Pages.

## Getting Started

1.  **Sign In**: Open the application and sign in using your Google
    account.
2.  **Create or Join a Group**:
    -   To create a group, enter a unique Group ID in the input field
        and click "Create".
    -   To join a group, enter an existing Group ID provided by a friend
        and click "Join".
3.  **Select a Group**: Click on a group name from your dashboard to
    enter the main scheduling view.
4.  **Set Your Availability**:
    -   Click and drag on the timetable to mark your busy slots.
    -   Alternatively, upload an .ics file from your calendar.
    -   Click Save to update your schedule for all groups.
5.  **Check Schedules**: Use the tools on the right to check who is free
    at a specific time or find common free slots for multiple friends.

