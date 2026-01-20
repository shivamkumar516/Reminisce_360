# 🗺️ Reminisce 360: Hackathon Development Roadmap

This roadmap outlines the planned development phases and key milestones for **Reminisce 360**, designed for a hackathon context focusing on rapid development and clear feature delivery. Our aim is to achieve a Minimum Viable Product (MVP) that demonstrates the core functionalities.

## 🎯 Core Goals for Hackathon MVP:

To successfully demonstrate Reminisce 360 during the hackathon, our MVP will include:

-   **Functional "Memory Anchor":** Real-time facial recognition integrated with Google Text-to-Speech for audio cues.
-   **Basic "Safe-Zone" Monitoring:** Geofencing logic that detects when a patient leaves a predefined safe area.
-   **Caregiver Notifications (MVP Level):** Alerts for geofence breaches and panic events, initially via console logging or a simple email, with WhatsApp as a stretch goal.
-   **User-Friendly Interface:** A camera-first patient interface that visually communicates key information (e.g., safe/unsafe status).

---

## 🚀 Phase 1: Foundation & Initial Setup (Day 1 - Morning)
**Goal:** Establish the project's technical base and development environment.

-   [x] **1.1 Environment Setup:** Install Python 3.x, pip, and create a virtual environment.
-   [x] **1.2 IDE Configuration:** Configure VS Code/PyCharm with relevant Python extensions.
-   [x] **1.3 Django Project Initialization:**
    -   Create Django project: `django-admin startproject reminisce360 .`
    -   Create core app: `python manage.py startapp core`
    -   Configure `settings.py` (database, installed apps).
-   [x] **1.4 Version Control:** Initialize Git repository and set up `.gitignore`.

**Milestone 1:** Basic Django project structure is runnable and version-controlled.

## ☁️ Phase 2: Google Cloud & API Integration Setup (Day 1 - Morning/Afternoon)
**Goal:** Securely connect the application to essential Google Cloud services.

-   [ ] **2.1 GCP Project Creation:** Set up a new project in the Google Cloud Console.
-   [ ] **2.2 API Enablement:** Enable **Cloud Vision API**, **Maps JavaScript API**, and **Cloud Text-to-Speech API**.
-   [ ] **2.3 Credential Management:** Generate and secure Service Account Key (JSON). Implement secure credential loading (e.g., using environment variables or `python-dotenv`).
-   [ ] **2.4 API Client Setup:** Install Google Cloud client libraries for Python (`google-cloud-vision`, `google-cloud-texttospeech`, etc.).
-   [ ] **2.5 Basic API Test:** Develop a minimal script to verify successful communication with each enabled API (e.g., a simple text-to-speech call, a dummy image vision request).

**Milestone 2:** Successful, authenticated connection to all required Google Cloud APIs.

## 🧠 Phase 3: Backend Core & Data Models (Day 1 - Afternoon)
**Goal:** Define the application's data structure and administrative interface.

-   [ ] **3.1 Database Schema Design:** Create Django models for:
    -   `Patient` (linking to Django's built-in User model if needed).
    -   `Caregiver` (linking to Django's built-in User model).
    -   `TrustedPerson` (stores photos, names, relationship to patient).
    -   `SafeZone` (stores home coordinates, radius for geofencing).
-   [ ] **3.2 Django Admin Integration:** Register models in `admin.py` and customize the Django Admin interface to allow caregivers to easily manage trusted persons (upload photos) and define safe zones.
-   [ ] **3.3 User Authentication:** Implement basic caregiver login/logout functionality.

**Milestone 3:** Functional Django Admin for data entry and basic caregiver authentication in place.

## 👁️ Phase 4: "Memory Anchor" & "Panic Detection" Logic (Day 1 - Evening)
**Goal:** Implement the core AI-driven patient interaction features.

-   [ ] **4.1 Image Capture/Processing:** Develop a method to feed image frames (e.g., from a webcam via OpenCV or simulated from static images) to the backend.
-   [ ] **4.2 Facial Recognition:**
    -   Send processed frames to the **Google Vision API** for face detection.
    -   Implement logic to compare detected faces against the `TrustedPerson` database.
-   [ ] **4.3 Text-to-Speech Integration:**
    -   Upon successful face recognition, generate dynamic text (e.g., "This is [Person's Name]").
    -   Use the **Google Text-to-Speech API** to convert this text into an audio file.
    -   Implement playback of the audio cue.
-   [ ] **4.4 Sentiment Analysis:**
    -   Extract emotional likelihoods from **Google Vision API** face annotations.
    -   Implement a basic "panic" detection logic (e.g., if `Likelihood.VERY_LIKELY` for fear/sorrow is detected).

**Milestone 4:** The system can recognize a familiar face, speak the person's name, and detect a state of panic (though alerts are not yet integrated).

## 📍 Phase 5: Geofencing & Location Services (Day 2 - Morning)
**Goal:** Develop the location-based safety monitoring.

-   [ ] **5.1 GPS Data Integration:** Implement a mechanism to feed patient's location data to the backend (e.g., simulated GPS coordinates, or using a device's Geolocation API if a frontend exists).
-   [ ] **5.2 Distance Calculation:** Implement geographical distance calculation (e.g., using Haversine formula or a utility from Google Maps libraries) between the patient's current location and the defined `SafeZone` center.
-   [ ] **5.3 Threshold Logic:**
    -   Define logic to determine if the patient has breached the `SafeZone` perimeter (e.g., `distance > 500m`).
    -   Set an internal flag or status for "Unsafe" state.

**Milestone 5:** The system can accurately track a patient's position relative to a safe zone and identify breaches.

## 📢 Phase 6: Alerting System (Day 2 - Morning/Afternoon)
**Goal:** Notify caregivers of critical events.

-   [ ] **6.1 Basic Alert Mechanism (MVP):**
    -   Implement logging to console or a simple email notification for "Panic Detected" and "Safe-Zone Breach" events.
    -   The alert message should include the event type and relevant details (e.g., patient's last known location).
-   [ ] **6.2 (Stretch Goal) WhatsApp Integration:**
    -   Integrate with a messaging API (e.g., Twilio for WhatsApp) to send real-time alerts.
    -   Craft rich alert messages including direct links to Google Maps for the patient's location.

**Milestone 6:** Caregivers receive notifications (at least via console/email) for critical safety events.

## 🎨 Phase 7: Minimalist Frontend & UI/UX (Day 2 - Afternoon)
**Goal:** Create an intuitive interface for both patients and caregivers.

-   [ ] **7.1 Patient View (Camera-first GUI):**
    -   Develop a simple web interface (using HTML/CSS/JS, potentially within a Django template) that displays a live camera feed (if feasible) or a static image placeholder.
    -   Visually communicate "Safe Zone" status (e.g., green for safe, red for breach) and recognized names.
    -   Ensure minimal interactivity for ease of use by patients.
-   [ ] **7.2 Caregiver Dashboard:**
    -   A basic Django template-based dashboard allowing caregivers to view event history, manage `TrustedPerson` entries, and update `SafeZone` settings.

**Milestone 7:** A functional, intuitive web UI is available for both patient (camera view) and caregiver (dashboard).

## 🧪 Phase 8: Testing, Refinement & Presentation Prep (Day 2 - Evening)
**Goal:** Ensure the MVP is robust and ready for demonstration.

-   [ ] **8.1 End-to-End Testing:** Conduct comprehensive testing of all integrated features (face recognition, geofencing, alerts).
-   [ ] **8.2 Bug Fixing:** Address any critical bugs or performance issues.
-   [ ] **8.3 UI/UX Polish:** Small aesthetic and usability improvements.
-   [ ] **8.4 Presentation Preparation:** Create a compelling demo script and ensure all components are ready for showcasing.

**Milestone 8:** A stable, demonstratable MVP of Reminisce 360 is ready for the hackathon presentation.
