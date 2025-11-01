# 🍔 Full-Stack Fast Food App (React Native, Expo, Appwrite)

This is a full-stack, cross-platform mobile application for ordering fast food, built with **React Native** and **Expo**.

It features a complete, end-to-end user experience, from user authentication to browsing a product catalog, customizing items with toppings, managing a shopping cart, and updating a user profile. The entire backend is powered by **Appwrite**, demonstrating a modern, Backend-as-a-Service (BaaS) architecture.

## Core Features

* **Full User Authentication:** Secure sign-up and sign-in flows connected directly to the Appwrite authentication service [cite: `app/(auth)/sign-in.tsx`, `app/(auth)/sign-up.tsx`, `lib/auth.appwrite.ts`].
* **File-Based Routing:** Uses **Expo Router** for all navigation, including protected routes, tabbed navigation, modal screens, and dynamic item detail pages [cite: `app/_layout.tsx`, `app/(tabs)/_layout.tsx`, `app/details/[id].tsx`].
* **Product Catalog & Filtering:** The home screen fetches and displays a list of food items from the Appwrite database. Includes a horizontal `FlatList` to filter by category (e.g., "Burgers", "Pizza") [cite: `app/(tabs)/index.tsx`, `components/Filter.tsx`].
* **Item Details & Customization:** Tapping a product navigates to a dynamic details page (`app/details/[id].tsx`) which fetches that specific item. Users can select from a list of available toppings to customize their order [cite: `app/details/[id].tsx`, `components/ToppingCard.tsx`].
* **Global Cart Management:** A fully persistent shopping cart managed with **Zustand**. Users can add/remove items, and the cart state is globally accessible, with the cart tab icon showing a badge with the item count [cite: `store/cart.store.ts`, `app/(tabs)/cart.tsx`, `components/CartItem.tsx`].
* **User Profile & Updates:** A dedicated profile tab displays user information (username, email, phone). Users can navigate to an "Update Profile" screen to edit their details, which are then synced with Appwrite [cite: `app/(tabs)/profile.tsx`, `app/update-profile.tsx`].
* **Native Styling with Tailwind:** The entire application is styled using **Nativewind**, bringing the power and developer experience of TailwindCSS to React Native [cite: `tailwind.config.js`, `app/global.css`].

---

## 🛠️ Technical Showcase & Architecture

This project demonstrates a modern, scalable, and efficient approach to full-stack mobile application development.

* **Framework:** **React Native (Expo)**. The project is built using the latest Expo SDK, leveraging its powerful tooling and libraries.
* **Backend-as-a-Service (Appwrite):** Instead of a traditional monolithic backend, this project uses **Appwrite** for all backend needs. This showcases proficiency in integrating with modern BaaS platforms.
    * **Service Abstraction:** All Appwrite SDK calls are neatly abstracted into a dedicated `lib/` directory. This creates a clean "service layer" that separates business logic from the Appwrite implementation (`lib/auth.appwrite.ts`, `lib/data.appwrite.ts`).
* **Routing (Expo Router):** This project uses **Expo Router**, the file-system-based router for React Native. This is a modern pattern inspired by web frameworks like Next.js.
    * **Route Groups:** The app is organized into route groups (`(auth)` and `(tabs)`) to manage different navigation stacks, such as the authentication flow vs. the main application flow [cite: `app/(auth)/_layout.tsx`, `app/(tabs)/_layout.tsx`].
    * **Dynamic Routes:** The item details page (`app/details/[id].tsx`) is a dynamic route that fetches data based on the ID in the URL.
    * **Protected Routes:** The root layout (`app/_layout.tsx`) intelligently redirects users to the `(auth)` flow or the `(tabs)` flow based on the authentication state from `useAuthStore`.
* **State Management (Zustand):** Global state is managed with **Zustand**, a lightweight, hook-based state management solution.
    * **`auth.store.ts`:** Holds the user's session, authentication status, and user data [cite: `store/auth.store.ts`].
    * **`cart.store.ts`:** Manages the entire shopping cart, including logic for adding items, removing items, and calculating totals [cite: `store/cart.store.ts`].
* **Data Fetching (Custom Hook):** The project uses a custom `useAppwrite` hook to simplify data fetching from Appwrite. This hook neatly encapsulates `loading` and `error` states, providing a clean, reusable way to load data in components [cite: `lib/useAppwrite.ts`, `app/(tabs)/index.tsx`].
* **Modern Styling (Nativewind):** By using Nativewind, the project benefits from TailwindCSS's utility-first classes, JIT compilation, and consistent design tokens, all within a React Native environment [cite: `tailwind.config.js`].
* **TypeScript:** The entire application is written in **TypeScript**, ensuring type safety, better developer experience, and more maintainable code [cite: `tsconfig.json`, `type.d.ts`].

---

## 🚀 Technology Stack

* **Framework:** React Native (Expo)
* **Routing:** Expo Router
* **Backend:** Appwrite (BaaS)
* **State Management:** Zustand
* **Styling:** Nativewind (TailwindCSS for React Native)
* **Forms:** `react-hook-form`
* **Language:** TypeScript

---

## 📂 Project Structure

The project uses the **Expo Router** file-system-based routing structure.

```
\
├── app/
│ ├── (auth)/ # Route group for authentication screens
│ │ ├── _layout.tsx # Stack navigator for auth flow
│ │ ├── sign-in.tsx # Login screen
│ │ └── sign-up.tsx # Register screen
│ │ │ ├── (tabs)/ # Route group for the main app (bottom tabs)
│ │ ├── _layout.tsx # Tab navigator layout
│ │ ├── cart.tsx # Cart screen
│ │ ├── index.tsx # Home screen (product catalog)
│ │ ├── profile.tsx # User profile screen
│ │ └── search.tsx # Search screen
│ │ │ ├── details/
│ │ ├── [id].tsx # Dynamic route for a single product's details
│ │ └── _layout.tsx # Stack navigator for the details flow
│ │ │ ├── _layout.tsx # Root layout (handles auth state & font loading)
│ └── update-profile.tsx # Modal screen for editing user profile
│ ├── assets/
│ ├── fonts/
│ └── icons/
│ ├── components/ # Reusable React components (MenuCard, CartItem, etc.)
│ ├── lib/
│ ├── appwrite.ts # Appwrite client configuration
│ ├── auth.appwrite.ts # Service layer for all auth-related Appwrite calls
│ ├── data.appwrite.ts # Service layer for all database-related Appwrite calls
│ └── useAppwrite.ts # Custom hook for data fetching
│ ├── store/
│ ├── auth.store.ts # Zustand store for user session
│ └── cart.store.ts # Zustand store for shopping cart
├── package.json
└── tailwind.config.js
```

---

## 🚀 Getting Started

### Prerequisites

* Node.js (LTS)
* Bun (`bun install -g bun`)
* Expo CLI (`bun install -g expo-cli`)
* An [Appwrite](https://appwrite.io/) project (self-hosted or cloud)
* An Android/iOS emulator or a physical device with the Expo Go app.

### Installation

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/your-username/fast-food-app.git](https://github.com/your-username/fast-food-app.git)
    cd fast-food-app
    ```

2.  **Install dependencies:**
    ```bash
    bun install
    ```

### Environment Setup

1.  Create a `.env` file in the root of the project.
2.  Add your Appwrite project credentials (you can find these in your Appwrite project settings):

    ```
    EXPO_PUBLIC_APPWRITE_ENDPOINT=[https://cloud.appwrite.io/v1](https://cloud.appwrite.io/v1)
    EXPO_PUBLIC_APPWRITE_PROJECT_ID=your_project_id
    EXPO_PUBLIC_APPWRITE_DATABASE_ID=your_database_id
    EXPO_PUBLIC_APPWRITE_USERS_COLLECTION_ID=your_users_collection_id
    EXPO_PUBLIC_APPWRITE_PRODUCTS_COLLECTION_ID=your_products_collection_id
    EXPO_PUBLIC_APPWRITE_TOPPINGS_COLLECTION_ID=your_toppings_collection_id
    EXPO_PUBLIC_APPWRITE_STORAGE_BUCKET_ID=your_storage_bucket_id
    ```

### Seeding the Database (Optional)

You can use the `lib/seed.ts` script to populate your Appwrite database with the initial product data.

1.  Make sure your Appwrite collections and attributes are set up to match the data structure in `lib/data.ts`.
2.  Run the seed script:
    ```bash
    bun run seed
    ```

### Running the Application

1.  **Start the Expo development server:**
    ```bash
    bun start
    ```

2.  Scan the QR code with the **Expo Go** app on your iOS or Android device.
