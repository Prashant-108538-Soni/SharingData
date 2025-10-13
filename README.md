3. Ride Module (Instant Booking & Tracking)
This is the core functionality of the app, covering the entire lifecycle of an instant ride request.
3.1. Booking Flow
1. Location Selection:
○ User selects Pickup Location (can be current GPS or manually entered/pinned on 2. Service Selection:
○ The app displays available Service Providers (e.g., Economy, Premium, SUV)
based on the distance, and provides an estimated fare for each option.
○ The user selects their desired service.
3. Ride Request:
○ User confirms the request.
○ The system broadcasts the request to nearby eligible drivers via the Veldoo
Driver App.
3.2. Real-Time Tracking & Updates (Post-Acceptance)
This is a critical component requiring real-time data synchronization.
Status Update User Interface Display Data Requirements
Driver Accepted Notification and screen update
showing: Driver Details
(Name, Photo, Rating, Vehicle
Type, License Plate).
Driver ID, Vehicle Details,
Acceptance Timestamp.
Driver En Route The home screen map displays
the Driver's Live Location as
an icon, continuously updating
its position towards the pickup
point.
Real-time GPS coordinates of
the Driver.
Driver Arrived Notification that the driver has
arrived.
Status update and arrival
timestamp.
Ride Started Notification and screen
update. The map now tracks
both the Driver's (with
passenger) and the User's
intended route towards the
drop-off.
Status update, Start time,
Calculated Route (Optional).
Ride Completed Notification. Transition to the
Fare Summary/Rating
Screen.
Final Bill details, Distance,
Duration, End Location.
Ride Canceled Notification detailing if the
driver or user canceled the
ride.
Cancellation reason,
Cancellation fee (if applicable).