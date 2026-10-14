This is an excellent master prompt already. For ChatGPT, Claude, Gemini, Cursor, Replit AI, Bolt.new, Lovable, or Windsurf, you'll get much better results if you convert it into an implementation-focused prompt that explicitly requests folder structure, reusable components, modular JavaScript, and complete file generation.

Use the enhanced prompt below.

AI Website Generation Prompt
Generate Complete Export Catalog Website

Create a complete production-ready multi-page website for a professional export company using:

HTML5
CSS3
Vanilla JavaScript ES6+
Font Awesome
JSON Data Source

No frameworks.

No Bootstrap.

No React.

No jQuery.

Must be pure HTML/CSS/JavaScript.

Project Structure

Generate all files below:

/project

│
├── index.html
├── categories.html
├── guarantee.html
├── workflow.html
├── contact.html
├── product.html
│
├── css/
│   └── style.css
│
├── js/
│   ├── main.js
│   ├── products.js
│   └── search.js
│
├── data/
│   └── products.json
│
├── images/
│   ├── hero-banner.jpg
│   ├── category-ceramics.jpg
│   ├── category-bathroom.jpg
│   ├── category-totebags.jpg
│   ├── category-home.jpg
│   └── category-kitchen.jpg
│
└── assets/
    └── logo.png

Design Requirements

Create a modern professional export company website.

Style:

White
Navy Blue
Light Gray

Visual Style:

Corporate
Premium
Export Industry
B2B Wholesale

Requirements:

Responsive Desktop
Responsive Tablet
Responsive Mobile

Sticky Header

Smooth Scroll

Mobile Hamburger Menu

Professional Footer

Card Hover Effects

Dark / Light Mode

Scroll To Top Button

Lazy Loaded Images

Animation On Scroll

SEO Friendly

Schema Markup

Accessible Design

Header

Include:

Logo

Home
Categories
Our Guarantee
Order Workflow
Contact Us

Request Quote Button


Features:

Sticky Navigation
Active Menu Highlight
Mobile Drawer Menu

Homepage (index.html)
Hero Section

Large background image.

Headline:

Premium Export Quality Products Delivered Worldwide

Subheadline:

Serving Importers, Distributors, Retail Chains, Private Label Brands

Buttons:

Explore Products
Contact Us
Animated Counters

Create animated number counting effect.

Display:

1000+ Products

50+ Countries Served

500+ Happy Customers

20+ Years Experience

Categories Section

Load from JavaScript array.

Categories:

[
  {
    "id": 1,
    "name": "Ceramics",
    "icon": "fa-mug-hot",
    "image": "images/category-ceramics.jpg"
  },
  {
    "id": 2,
    "name": "Bathroom Accessories",
    "icon": "fa-bath",
    "image": "images/category-bathroom.jpg"
  },
  {
    "id": 3,
    "name": "Tote Bags",
    "icon": "fa-bag-shopping",
    "image": "images/category-totebags.jpg"
  },
  {
    "id": 4,
    "name": "Home Decor",
    "icon": "fa-house",
    "image": "images/category-home.jpg"
  },
  {
    "id": 5,
    "name": "Kitchenware",
    "icon": "fa-utensils",
    "image": "images/category-kitchen.jpg"
  }
]


Card Layout:

Image
Icon
Name

View Products

Why Choose Us

Create 4 premium cards.

Premium Quality

Global Shipping

Custom Branding

Competitive Pricing


Use icons and animations.

Categories Page
Features

Search Categories

Category Cards

Banner

Product Count

Responsive Grid

Card Structure:

Image

Category Name

Description

Product Count

View Products

Our Guarantee Page

Create professional guarantee section.

Cards:

Quality Inspection

Secure Packaging

Timely Delivery

Transparent Communication

Private Label Support

Customer Satisfaction


Requirements:

Icons

Timeline Graphics

Trust Indicators

Certificates Area

Export Process Graphics

Workflow Page

Create responsive export-order workflow timeline.

Display:

1 Product Inquiry

↓

2 Quotation

↓

3 Sample Approval

↓

4 Production

↓

5 Quality Inspection

↓

6 Shipment

↓

7 Delivery


Requirements:

Desktop Horizontal Timeline

Mobile Vertical Timeline

Icons Per Stage

Animations

Contact Page

Sections:

Contact Form

Google Map Placeholder

Phone

Email

WhatsApp

Office Address


Contact Form Fields:

Name

Company Name

Email

Phone

Country

Message


Validation:

Required Fields

Email Validation

Success Message

Error Message

Product Details Page

File:

product.html?id=1

Layout
------------------------------------
Sidebar | Product Details
------------------------------------

Sticky Sidebar

Include:

Categories

Filters

Related Products

Download Catalogue Button


Desktop Sticky.

Collapsible On Mobile.

Product Content

Load dynamically from:

data/products.json

Image Gallery

Features:

Main Image

Thumbnail Gallery

Image Slider

Image Zoom

Lazy Loading

Product Information

Display:

Product Name

SKU

Category

MOQ

Material

Available Sizes

Country Of Origin

Lead Time

Feature Highlights

Visual badges:

Reusable

Export Quality

Customizable

Eco Friendly

Product Tabs
Specifications

Generate table from JSON.

Description

Load HTML content from JSON.

Related Products

Automatically load:

3-4 related products

Same category

products.json

Create realistic data.

Minimum:

{
  "products": [
    {
      "id": 1,
      "name": "Blue Pottery Vase",
      "category": "Ceramics",
      "sku": "BPV-001",
      "price": "Quote Required",
      "material": "Ceramic",
      "origin": "India",
      "moq": "200 Pieces",
      "leadTime": "30 Days",
      "sizes": ["Small", "Medium", "Large"],
      "images": [
        "images/product1-1.jpg",
        "images/product1-2.jpg",
        "images/product1-3.jpg"
      ],
      "features": [
        "Handcrafted",
        "Export Quality",
        "Custom Packaging",
        "Eco Friendly"
      ],
      "specifications": {
        "Material": "Ceramic",
        "Color": "Blue White",
        "Weight": "1.5 Kg",
        "Packaging": "Export Carton"
      },
      "description": "<p>Premium handcrafted ceramic vase suitable for gift and decor markets.</p>"
    }
  ]
}


Create at least:

10 Products


Across:

Ceramics

Bathroom Accessories

Tote Bags

Home Decor

Kitchenware

Footer

Create professional export footer.

Section 1:

About Company

Section 2:

Quick Links

Home
Categories
Guarantee
Workflow
Contact


Section 3:

Product Categories

Ceramics

Bathroom Accessories

Home Decor

Kitchenware

Tote Bags


Section 4:

Contact Details

Address

Phone

Email

WhatsApp


Section 5:

Social Icons

Facebook
Instagram
LinkedIn
YouTube


Bottom Bar:

© 2026 Company Name.
All Rights Reserved.

Advanced JavaScript Features

Implement:

Dark Mode Toggle

Sticky Header

Scroll To Top

Product Search

Category Filtering

Dynamic JSON Fetch API

Breadcrumb Navigation

Product Gallery Slider

Product Zoom

Related Products

Mobile Navigation

Form Validation

Animated Counter

Animate On Scroll

Lazy Loading Images

SEO Requirements

Add:

<meta name="description">

<meta name="keywords">

<meta property="og:title">

<meta property="og:description">

<meta property="og:image">

<meta property="og:type">

<link rel="canonical">


Add structured data:

JSON-LD Schema Markup


For:

Organization

Product

Website

Code Quality Requirements

Generate:

Reusable Components

Clean CSS Variables

Modular JavaScript

Detailed Comments

Cross-Browser Compatible

Production Ready

W3C Compliant

Fast Loading

Final Output

Generate complete source code for every file:

index.html
categories.html
guarantee.html
workflow.html
contact.html
product.html

css/style.css

js/main.js
js/products.js
js/search.js

data/products.json


Include all HTML, CSS, JavaScript, and JSON code with proper file references so the website runs immediately after opening index.html on a local computer or when uploaded to GitHub Pages, Netlify, Vercel, or any web hosting platform.
