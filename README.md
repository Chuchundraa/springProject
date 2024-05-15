### Project Topic: "Забезпечення проведення лабораторних та практичних робіт" (Providing Conduct of Laboratory and Practical Work)

### Functional Requirements
1. **User Authentication and Authorization**
   - Users can register and log in to the system.
   - Roles: Student, Teacher, Admin.

2. **User Profile Management**
   - Users can view and update their profiles.

3. **Course Management**
   - Teachers can create, update, and delete courses.
   - Students can enroll in courses.

4. **Laboratory and Practical Work Management**
   - Teachers can create, update, and delete lab and practical work assignments.
   - Students can view and submit assignments.

5. **Submission and Grading**
   - Students can submit their lab and practical work.
   - Teachers can grade and provide feedback on submissions.

6. **Notification System**
   - Users receive notifications for new assignments, deadlines, and grades.

7. **Discussion Forum**
   - Users can post questions and comments related to lab and practical work.
   - Teachers and students can respond to posts.

8. **Resource Management**
   - Teachers can upload and manage resources (documents, links) related to lab and practical work.
   - Students can download and view resources.

9. **Scheduling and Calendar**
   - Users can view a calendar with deadlines and scheduled lab sessions.
   - Teachers can schedule lab sessions.

10. **Reporting and Analytics**
    - Admins and Teachers can generate reports on student performance.
    - Users can view their own activity logs and progress.

### Mockups
(Mockups are described below for understanding. They are typically created using tools like Figma, Adobe XD, or even drawn by hand.)

1. **Login Page**
   - Fields: Username, Password
   - Buttons: Login, Register

2. **Dashboard**
   - Sections: Courses, Notifications, Calendar
   - Links: Profile, Settings, Logout

3. **Course Page (Teacher View)**
   - Sections: Course Details, Students Enrolled, Assignments
   - Buttons: Add Assignment, Manage Resources, Schedule Lab

4. **Course Page (Student View)**
   - Sections: Course Details, Assignments, Resources
   - Buttons: Enroll/Unenroll, Submit Assignment

5. **Assignment Page (Teacher View)**
   - Fields: Assignment Title, Description, Due Date
   - Sections: Submissions, Grades
   - Buttons: Grade Submission, Provide Feedback

6. **Assignment Page (Student View)**
   - Fields: Assignment Title, Description, Due Date
   - Buttons: Submit, View Feedback

7. **Profile Page**
   - Fields: Name, Email, Role, Bio
   - Buttons: Edit Profile, Change Password

8. **Discussion Forum Page**
   - Sections: Threads, Posts
   - Buttons: New Thread, Reply

9. **Resource Management Page (Teacher View)**
   - Sections: Uploaded Resources
   - Buttons: Upload Resource, Delete Resource

10. **Reports Page (Admin View)**
    - Sections: User Activity, Performance Analytics
    - Filters: Date Range, Course

### System Behavior and REST API Endpoints

#### User Authentication and Authorization
- **POST /api/auth/register**
  - Registers a new user.
  - Request: `{ "username": "user", "password": "pass", "role": "student" }`
  - Response: `{ "message": "Registration successful" }`

- **POST /api/auth/login**
  - Authenticates a user.
  - Request: `{ "username": "user", "password": "pass" }`
  - Response: `{ "token": "jwt-token" }`

#### User Profile Management
- **GET /api/user/profile**
  - Retrieves the profile of the logged-in user.
  - Response: `{ "username": "user", "email": "user@example.com", "role": "student" }`

- **PUT /api/user/profile**
  - Updates the profile of the logged-in user.
  - Request: `{ "email": "new-email@example.com", "bio": "New bio" }`
  - Response: `{ "message": "Profile updated successfully" }`

#### Course Management
- **POST /api/courses**
  - Creates a new course (Teacher only).
  - Request: `{ "title": "Course Title", "description": "Course Description" }`
  - Response: `{ "id": "course-id", "message": "Course created successfully" }`

- **GET /api/courses**
  - Retrieves a list of all courses.
  - Response: `[ { "id": "course-id", "title": "Course Title", "description": "Course Description" } ]`

- **PUT /api/courses/{courseId}**
  - Updates an existing course (Teacher only).
  - Request: `{ "title": "Updated Title", "description": "Updated Description" }`
  - Response: `{ "message": "Course updated successfully" }`

- **DELETE /api/courses/{courseId}**
  - Deletes a course (Teacher only).
  - Response: `{ "message": "Course deleted successfully" }`

#### Laboratory and Practical Work Management
- **POST /api/courses/{courseId}/assignments**
  - Creates a new assignment (Teacher only).
  - Request: `{ "title": "Assignment Title", "description": "Assignment Description", "dueDate": "2024-06-01T23:59:59" }`
  - Response: `{ "id": "assignment-id", "message": "Assignment created successfully" }`

- **GET /api/courses/{courseId}/assignments**
  - Retrieves all assignments for a course.
  - Response: `[ { "id": "assignment-id", "title": "Assignment Title", "description": "Assignment Description", "dueDate": "2024-06-01T23:59:59" } ]`

- **PUT /api/courses/{courseId}/assignments/{assignmentId}**
  - Updates an assignment (Teacher only).
  - Request: `{ "title": "Updated Title", "description": "Updated Description", "dueDate": "2024-06-05T23:59:59" }`
  - Response: `{ "message": "Assignment updated successfully" }`

- **DELETE /api/courses/{courseId}/assignments/{assignmentId}**
  - Deletes an assignment (Teacher only).
  - Response: `{ "message": "Assignment deleted successfully" }`

#### Submission and Grading
- **POST /api/courses/{courseId}/assignments/{assignmentId}/submissions**
  - Submits an assignment (Student only).
  - Request: `{ "content": "Submission content or file" }`
  - Response: `{ "message": "Submission successful" }`

- **GET /api/courses/{courseId}/assignments/{assignmentId}/submissions**
  - Retrieves all submissions for an assignment (Teacher only).
  - Response: `[ { "id": "submission-id", "studentId": "student-id", "content": "Submission content", "grade": null } ]`

- **PUT /api/courses/{courseId}/assignments/{assignmentId}/submissions/{submissionId}/grade**
  - Grades a submission (Teacher only).
  - Request: `{ "grade": "A", "feedback": "Good work" }`
  - Response: `{ "message": "Submission graded successfully" }`

#### Notification System
- **GET /api/notifications**
  - Retrieves notifications for the logged-in user.
  - Response: `[ { "id": "notification-id", "message": "New assignment available", "date": "2024-05-15T10:00:00" } ]`

#### Discussion Forum
- **GET /api/courses/{courseId}/discussions**
  - Retrieves discussion threads for a course.
  - Response: `[ { "id": "thread-id", "title": "Discussion Title", "posts": [ { "id": "post-id", "content": "Post content", "author": "user" } ] } ]`

- **POST /api/courses/{courseId}/discussions**
  - Creates a new discussion thread.
  - Request: `{ "title": "Discussion Title", "content": "Initial post content" }`
  - Response: `{ "id": "thread-id", "message": "Discussion created successfully" }`

- **POST /api/courses/{courseId}/discussions/{threadId}/posts**
  - Adds a post to a discussion thread.
  - Request: `{ "content": "Reply content" }`
  - Response: `{ "id": "post-id", "message": "Post added successfully" }`

#### Resource Management
- **POST /api/courses/{courseId}/resources**
  - Uploads a resource (Teacher only).
  - Request: `{ "title": "Resource Title", "file": "base64encodedfilecontent" }`
  - Response: `{ "id": "resource-id", "message": "Resource uploaded successfully" }`

- **GET /api/courses/{courseId}/resources**
  - Retrieves resources for a course.
  - Response: `[ { "id": "resource-id", "title": "Resource Title", "url": "http://link-to-resource" } ]`

#### Scheduling and Calendar
- **GET /api/calendar**
  - Retrieves calendar events for the logged-in user.
  - Response: `[ { "id": "event-id", "title": "Lab Session", "date": "2024-05-20T10:00:00" } ]`

- **POST /api/courses/{courseId}/schedule**
  -
