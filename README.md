#  Doctorid Android application

This Android application (built in Kotlin) integrates with Firebase, PHP backend APIs, and third-party APIs to deliver a wide range of medical and health-related functionalities. The project uses XML for user interface design and leverages several external services to manage data, authentication, notifications, and more.

## Purpose

The app is designed to:
- Allow patients and doctors to interact via messaging and profile management.
- Provide functionalities such as appointment reviews, health metrics display, and disease/medicine data handling.
- Enable Firebase authentication and real-time database operations.
- Communicate with backend PHP endpoints for inserting data (diseases, medicines, family diseases, etc.).
- Fetch news articles and drug information using external APIs.

## Features

- **User Authentication and Profiles**
  - Patient/doctor signup and login with Firebase Authentication ([PatientSignUp.kt](app/src/main/java/com/project/sfmd_project/PatientSignUp.kt), [DoctorProfile.kt](app/src/main/java/com/project/sfmd_project/DoctorProfile.kt)).
  - Profile editing via [EditProfile.kt](app/src/main/java/com/project/sfmd_project/EditProfile.kt).

- **Data Submission & Sync**
  - Local data storage using SQLite with helper class `MySQLiteHelper` present in multiple activities ([Add4.kt](app/src/main/java/com/project/sfmd_project/Add4.kt), [Add5.kt](app/src/main/java/com/project/sfmd_project/Add5.kt)).
  - Online data insertion via HTTP POST requests to PHP endpoints:
    - Diseases: `http://192.168.100.44/api/insert_diseases.php`
    - Family diseases: `http://192.168.100.44/api/insert_familydiseases.php`
    - Medicines: `http://192.168.100.44/api/insert_medicines.php`

- **API Integrations**
  - **News API:** In [Articles.kt](app/src/main/java/com/project/sfmd_project/Articles.kt) the app performs searches for articles using a key with the URL: `https://newsapi.org/v2/everything`.
  - **Drug Information API:** In [PharmacySearchActivity.kt](app/src/main/java/com/project/sfmd_project/PharmacySearchActivity.kt), the app fetches drug information from RapidAPI using authentication headers.
  - **Firebase Cloud Messaging:** Notifications are generated using a custom service ([MyFirebaseMessagingService.kt](app/src/main/java/com/project/sfmd_project/MyFirebaseMessagingService.kt)) upon successful API calls or local data sync.

- **Real-time Communication and Video**
  - Live chat and messaging features through Firebase Realtime Database ([Chat.kt](app/src/main/java/com/project/sfmd_project/Chat.kt)).
  - Video setup and remote stream handling implemented in [MainActivity20.kt](app/src/main/java/com/project/sfmd_project/MainActivity20.kt).

- **Additional Functionalities**
  - Health metrics display ([HealthMetrics.kt](app/src/main/java/com/project/sfmd_project/HealthMetrics.kt)).
  - Profile reviews and doctor rating functionality ([Add2.kt](app/src/main/java/com/project/sfmd_project/Add2.kt), [Reviews.kt](app/src/main/java/com/project/sfmd_project/Reviews.kt)).
  - Instrumented tests for UI and integration test cases ([ExampleInstrumentedTest.kt](app/src/androidTest/java/com/project/sfmd_project/ExampleInstrumentedTest.kt)).

## Technologies Used

- **Kotlin:** Primary programming language used for app development.
- **Firebase:** Authentication, Realtime Database, Storage, and Cloud Messaging.
- **XML:** Layout design and UI definitions.
- **PHP:** Backend endpoints for data insertion.
- **Third-Party APIs:**
  - News API (`https://newsapi.org/v2/everything`)
  - Drug information via RapidAPI (`https://drug-info-and-price-history.p.rapidapi.com/1/druginfo`)

## Build and Run

1. **Prerequisites:**
   - Android Studio or Visual Studio Code with Android development extensions.
   - JDK 1.8 or higher.
   - An Android device (or emulator) running minSdk 26 and targetSdk 34.
   - Firebase project with the corresponding `google-services.json` integrated in [app/](app).

2. **Setup:**
   - Clone the repository.
   - Open the project in your IDE.
   - Check the Gradle settings in [gradle.properties](gradle.properties) and ensure that the JVM arguments and AndroidX settings are correct.
   - Verify the Firebase configuration in [app/build.gradle.kts](app/build.gradle.kts) where the Google Services plugin is applied.

3. **Running the Project:**
   - Execute the following command in the terminal to build the project:
     ```sh
     ./gradlew build
     ```
   - To run the app on an emulator or connected device:
     ```sh
     ./gradlew installDebug
     ```
   - Alternatively, use the Run/Debug configurations provided in your IDE.

## API Usage Details

- **Disease Insertion:**  
  Called from Retype.kt and Add4.kt, these endpoints require a POST parameter with the new data.  
  *Endpoint Example:* `http://192.168.100.44/api/insert_diseases.php`

- **Family Diseases and Medicines:**  
  Similar HTTP POST logic is implemented in Add6.kt for family diseases and in Add5.kt for medicines.

- **News and Drug Info API:**  
  Articles are fetched in Articles.kt and drug data is retrieved in PharmacySearchActivity.kt using specific headers and keys as detailed in the code.

- **Notification Generation:**  
  Both medicine and review insertions trigger notifications using the `generateNotification` function in MyFirebaseMessagingService.kt.

## Testing

- **Instrumented Tests:**  
  Basic detailed tests are available in ExampleInstrumentedTest.kt to verify app context and functionality.
- **Unit Tests:**  
  Standard JUnit tests can be found (or added) in the test source directory as configured in [build.gradle.kts](http://_vscodecontentref_/0).

## Conclusion

This project is a fully integrated Kotlin Android application leveraging both Firebase and several external API services to offer a comprehensive solution in the health and medical domain. It demonstrates usage of real-time data, push notifications, and local caching using SQLite when network connectivity is compromised.
