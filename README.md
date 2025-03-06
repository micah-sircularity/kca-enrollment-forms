```markdown
# KCA Enrollment Forms

A modern, user-friendly application for handling the KCA (presumably "Kids Christian Academy") enrollment process. This application streamlines the collection of student, parent, and other relevant information through a multi-step form, and integrates with Airtable for data storage and Stripe for payment processing.

## Problem Solved

This project aims to replace traditional paper-based enrollment forms with a digital solution, reducing administrative overhead, improving data accuracy, and providing a more convenient experience for parents.  It automates the enrollment process, from initial application to payment, making it more efficient for both the school and the families.

## Technologies Used

*   **React:**  A JavaScript library for building user interfaces.
*   **Vite:** A fast and lightweight build tool for modern web development.
*   **Tailwind CSS:** A utility-first CSS framework for rapid UI development.
*   **Airtable:** A cloud-based platform for creating and sharing relational databases (used for storing enrollment data).
*   **Stripe:** A payment gateway for securely processing online payments (used for enrollment fees).

## Setup Instructions

Follow these steps to set up the KCA Enrollment Forms application:

1.  **Clone the repository:**

    ```bash
    git clone <repository_url>
    cd kca-enrollment-forms
    ```

2.  **Install dependencies:**

    ```bash
    npm install  # or yarn install or pnpm install
    ```

3.  **Environment Variables:**

    This application relies on environment variables for configuration, especially for Airtable and Stripe integration. Create a `.env` file in the root directory of the project and add the following variables:

    ```
    VITE_AIRTABLE_API_KEY=<your_airtable_api_key>
    VITE_AIRTABLE_BASE_ID=<your_airtable_base_id>
    VITE_AIRTABLE_TABLE_NAME=<your_airtable_table_name>  # e.g., "EnrollmentApplications"
    VITE_STRIPE_PUBLISHABLE_KEY=<your_stripe_publishable_key>
    VITE_STRIPE_SECRET_KEY=<your_stripe_secret_key> # Only needed for backend/server-side operations
    ```

    **Important:**

    *   Replace `<your_airtable_api_key>`, `<your_airtable_base_id>`, `<your_airtable_table_name>`, `<your_stripe_publishable_key>`, and `<your_stripe_secret_key>` with your actual Airtable API key, Airtable base ID, Airtable table name, Stripe publishable key, and Stripe secret key, respectively.
    *   **Never commit your `.env` file to version control.**  Add `.env` to your `.gitignore` file.
    *   The `VITE_STRIPE_SECRET_KEY` should only be used in a secure backend environment and never exposed directly in the client-side code.

4.  **Configure Airtable:**

    *   Create an Airtable base to store enrollment data.
    *   Create a table within the base with columns corresponding to the fields in the enrollment form (e.g., Student Name, Parent Name, Address, etc.).  Ensure the column names match the data being sent from the application.
    *   Note the Base ID and Table Name for use in the `.env` file.

5.  **Configure Stripe:**

    *   Create a Stripe account (if you don't already have one).
    *   Obtain your Stripe Publishable Key and Secret Key from the Stripe dashboard.
    *   Configure a Stripe product for the enrollment fee.  You may need to create a backend endpoint to handle the actual charge using the Stripe Secret Key.

6.  **Run the application:**

    ```bash
    npm run dev  # or yarn dev or pnpm dev
    ```

    This will start the development server.  Open your browser and navigate to the address displayed in the console (usually `http://localhost:5173`).

## Usage Examples

*   **Submitting an Enrollment Form:**  Parents can access the application through a web browser and complete the multi-step form, providing all necessary information.
*   **Making a Payment:**  After completing the form, parents can securely pay the enrollment fee using Stripe.
*   **Viewing Enrollment Data (Admin):**  Administrators can access the Airtable base to view and manage submitted enrollment applications.

## Notable Features and Components

*   **Multi-Step Form:** The application uses a multi-step form (`StudentInfoForm.jsx`, `ParentInfoForm.jsx`, `SchoolingOptionsForm.jsx`, `ReligiousInfoForm.jsx`, `MedicalInfoForm.jsx`, `AdditionalInfoForm.jsx`, `AgreementsForm.jsx`, `FinancialConsentForm.jsx`) to guide users through the enrollment process.
*   **Progress Bar:**  A `ProgressBar.jsx` component visually indicates the user's progress through the form.
*   **Form Navigation:**  `FormNavigation.jsx` provides controls for moving between form steps.
*   **Data Storage:**  Enrollment data is stored in Airtable.
*   **Payment Processing:**  `PaymentForm.jsx` handles payment processing via Stripe.
*   **Context Management:** `FormContext.jsx` likely manages the state of the form across different components.
*   **Local Storage:** `storage.js` likely handles saving form data to local storage to prevent data loss.

## Troubleshooting

*   **Airtable Integration Issues:**
    *   **Check API Key and Base ID:**  Ensure that the `VITE_AIRTABLE_API_KEY` and `VITE_AIRTABLE_BASE_ID` environment variables are correctly set.
    *   **Verify Table Name:**  Confirm that the `VITE_AIRTABLE_TABLE_NAME` environment variable matches the name of your Airtable table.
    *   **Column Names:**  Double-check that the column names in your Airtable table match the data being sent from the application.  Case sensitivity may be important.
    *   **CORS Errors:** If you encounter CORS errors, ensure that your Airtable base is configured to allow requests from your application's domain.  This is less common with client-side Airtable integrations but still possible.

*   **Stripe Integration Issues:**
    *   **Check API Keys:**  Ensure that the `VITE_STRIPE_PUBLISHABLE_KEY` environment variable is correctly set.  The `VITE_STRIPE_SECRET_KEY` should only be used on the server-side.
    *   **Stripe.js Initialization:**  Verify that Stripe.js is correctly initialized in your `PaymentForm.jsx` component.
    *   **Payment Intent Creation:**  If you are using Payment Intents, ensure that you have a backend endpoint to create them using your Stripe Secret Key.
