Veldoo User App Documentation
1. Introduction
The Veldoo User App is the customer-facing component of the two-part Veldoo
transportation ecosystem (User App and Driver App). Its primary function is to provide a
seamless and intuitive platform for users to book, manage, and track rides.
2. Authentication & Account Management
(Login/Signup)
This module handles user access and initial account setup.
Feature Description
Login Users can log in using their registered Phone
Number and Password.
New Account Registration A streamlined sign-up process where a user
enters their name, phone number, and desired
password. OTP (One-Time Password)
verification is required to confirm the phone
number and activate the account.
Forgot Password A recovery flow where the user provides their
registered phone number. An OTP is sent to
the phone number for verification, allowing the
user to securely set a new password.
3. Ride Module (Instant Booking & Tracking)
This is the core functionality of the app, covering the entire lifecycle of an instant ride request.
3.1. Booking Flow
1. Location Selection:
○ User selects Pickup Location (can be current GPS or manually entered/pinned on