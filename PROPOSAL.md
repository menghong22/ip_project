# Laboratory Equipment Lending System

## Problem
University laboratory equipment management is currently disorganized, leading to misplaced hardware, prolonged borrowing queues, and manual tracking errors that hinder students from completing practical coursework efficiently. Implementing a centralized digital lending platform resolves these bottlenecks by streamlining reservations, inventory visibility, and automated return tracking for both students and laboratory staff.

## Users and roles
* **Student**: Browses available equipment, submits loan requests, tracks approval status, and views personal borrowing history.
* **Lab Assistant**: Manages equipment inventory, reviews or approves pending loan requests, records items being returned, and oversees overdue item statuses.

## User stories
1. As a student, I want to browse available laboratory equipment by category so that I can find the hardware needed for my coursework.
   * Accepted when: The equipment list displays item availability status in real-time.
   * Accepted when: Filtering by category returns matching inventory items.
   * Accepted when: Selecting an item opens a detail view with technical specifications.
2. As a student, I want to submit a loan request for a piece of equipment so that I can reserve it for my lab practicals.
   * Accepted when: The user can select a desired start and return date.
   * Accepted when: Submitting the form creates a loan record with a pending status.
   * Accepted when: Validation prevents booking items that are already fully checked out.
3. As a lab assistant, I want to review and approve or reject pending loan requests so that departmental hardware is allocated fairly.
   * Accepted when: A dedicated dashboard displays all pending loan requests.
   * Accepted when: Clicking approve updates the loan status to active and marks the equipment as unavailable.
   * Accepted when: Clicking reject requires entering a brief reason.
4. As a student, I want to view my active and past loan history so that I can monitor my return deadlines.
5. As a lab assistant, I want to add new equipment items to the system inventory so that students can access newly acquired hardware.
6. As a lab assistant, I want to record returned equipment items so that inventory counts are accurately restored.
7. As a student, I want to receive validation feedback on form inputs so that I can correct errors before submission.
8. As a student, I want to receive automated email notifications when my loan request is approved or overdue.

## MVP scope
* **Must have**: Stories 1, 2, 3, 4, 5, 6, and 7 (User authentication with role guards, CRUD operations for equipment and loans, and client/server validation).
* **Nice to have**: Story 8 (Automated email notifications for loan status updates).

## Cut story explanation
**Which story did you cut from the MVP, and why?**
Story 8 (automated email notifications) was cut from the core MVP to keep the initial development focused strictly on the primary relational data interactions (CRUD on users, equipment, and loans) and scheduled tasks, avoiding third-party email service integrations during early milestones.

## Entities

| Entity | Main attributes | Relations |
|---|---|---|
| User | id, name, email, passwordHash, role | has many Loans |
| Equipment | id, name, category, serialNumber, status | has many Loans |
| Loan | id, borrowDate, returnDate, status | belongs to User, belongs to Equipment |

## Stretch feature
**Scheduled task**: A daily background cron job implemented via NestJS Schedule that automatically queries active loans past their return date and updates their status to overdue while flagging them for lab assistants.

## Repository
https://github.com/menghong22/ip_project.git