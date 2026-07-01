# **Executive Portfolio Website \- Abhay Jain**

A modern, high-performance, and responsive personal portfolio website built for an executive professional. This project features a clean, dual-theme (Dark/Light) UI, fluid scroll animations, and a fully integrated serverless backend for managing direct inquiries and newsletter subscriptions.

## **🚀 Features**

* **Responsive Design:** Fully optimized for both mobile and desktop viewing, featuring custom responsive navigation.  
* **Dark/Light Mode:** Built-in theme toggle with localStorage memory to respect user preferences.  
* **Modern UI/UX:** Utilizes advanced CSS animations, background gradients, scroll-reveals, and glassmorphism styling.  
* **Serverless Backend:** HTML forms are directly wired to a PostgreSQL database using Supabase, complete with HTML5 validation and error handling.  
* **Zero-Build Setup:** Uses Tailwind CSS via CDN, eliminating the need for complex Node.js build pipelines or local terminal environment configurations.

## **🛠️ Tech Stack**

* **Frontend:** HTML5, Vanilla JavaScript, CSS3  
* **Styling:** [Tailwind CSS](https://tailwindcss.com/) (Production CDN)  
* **Backend/Database:** [Supabase](https://supabase.com/) (PostgreSQL)  
* **Fonts:** Google Fonts ('Inter' for UI, 'Forum' for headings)

## **📂 Project Structure**

├── index.html                  \# Home page (Hero, Track Record, Contact Form)  
├── about.html                  \# About page (Executive Profile, Pedigree, Honors)  
├── README.md                   \# Project documentation  
└── Assets (Images)  
    ├── Abhay\_Jain\_profile\_pic.jpg  
    ├── Abhay\_Jain\_banner\_pic.jpg  
    ├── kalam\_bg.jpg  
    ├── mckinsey\_logo.png  
    ├── stanford\_logo.png  
    └── ... (other local logos)

## **⚙️ Setup & Installation**

Because this project uses the Tailwind CDN and Vanilla JS, there is no build process required.

1. **Clone the repository:**  
   git clone https://github.com/YOUR\_USERNAME/YOUR\_REPO\_NAME.git

2. **Open the files:** Simply double-click index.html to open it in your browser, or use a local development server like the VS Code "Live Server" extension for the best experience.

## **🗄️ Database Configuration (Supabase)**

To get the contact and subscription forms working, you must connect the project to a Supabase backend.

### **1\. Create the Tables**

Run the following SQL commands in your Supabase SQL Editor to create the required tables:

\-- Create table for Contact Form  
create table inquiries (  
  id bigint primary key generated always as identity,  
  first\_name text not null,  
  last\_name text not null,  
  email text not null,  
  phone text,  
  subject text,  
  message text not null,  
  created\_at timestamp with time zone default timezone('utc'::text, now()) not null  
);

\-- Create table for Email Subscriptions  
create table subscriptions (  
  id bigint primary key generated always as identity,  
  email text not null unique,  
  created\_at timestamp with time zone default timezone('utc'::text, now()) not null  
);

### **2\. Connect the API Keys**

In both index.html and about.html, locate the \<script\> tag at the very bottom of the file. Replace the placeholder strings with your actual Supabase Project URL and Anon Key:

const SUPABASE\_URL \= 'https://YOUR\_PROJECT\_ID.supabase.co';  
const SUPABASE\_ANON\_KEY \= 'YOUR\_LONG\_ANON\_KEY';

### **3\. Security (Row Level Security)**

**Crucial Step:** Do not leave your database completely open. To allow public form submissions while keeping your data private, run this SQL command to enable Row Level Security (RLS) with Insert-Only policies:

\-- Enable RLS  
alter table inquiries enable row level security;  
alter table subscriptions enable row level security;

\-- Allow public to submit (insert) data, but block public reading  
create policy "Allow public inserts on inquiries" on inquiries for insert to anon with check (true);  
create policy "Allow public inserts on subscriptions" on subscriptions for insert to anon with check (true);

## **📄 License**

This project is intended for personal portfolio use. Content, professional history, and images belong to Abhay Jain.