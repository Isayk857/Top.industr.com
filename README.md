TOP INDUSTRY — Netlify-ready full-stack starter
This package is prepared to deploy the frontend and Express backend together on Netlify Functions.
Included
PostgreSQL database schema
User registration/login with bcrypt + JWT
User balance
Video catalogue
Deposit requests
Admin deposit approval
Admin video management
Withdrawal requests
Netlify Function adapter for Express
Netlify routing configuration
Payment endpoint placeholder (no fake payments)
Netlify setup
Create a PostgreSQL database and run schema.sql.
Deploy this folder to Netlify.
Add environment variables in Netlify:
DATABASE_URL
JWT_SECRET
FRONTEND_URL (your Netlify site URL, or * temporarily for testing)
Redeploy.
Test: https://YOUR-SITE.netlify.app/api/health
Netlify deploys the Express backend through a serverless function. The frontend already calls /api/..., so it can use the same site origin.
Payment
Automatic payment is not activated in this package. A real provider requires merchant/API credentials and a verified webhook before a successful payment can credit a user's balance.
Login/Register setup — important
The frontend Login/Register is included and uses:
POST /api/auth/register
POST /api/auth/login
JWT token stored in the browser
bcrypt password hashing on the server
PostgreSQL users table
For real accounts on Netlify, create a PostgreSQL database and run schema.sql, then add these Netlify environment variables:
DATABASE_URL = your PostgreSQL connection string
JWT_SECRET = a long random secret
FRONTEND_URL = your Netlify site URL
After saving the variables, redeploy the site. Do not put DATABASE_URL or JWT_SECRET inside index.html.
Deposit methods configured
The Deposit page supports:
Telebirr
Sinqee
Awash Bank
A deposit request is stored in PostgreSQL and does not increase balance automatically. An admin must approve it first. This prevents fake client-side deposits.
Important for deployment
You still need:
A PostgreSQL database (for example Neon).
DATABASE_URL in Netlify environment variables.
A strong JWT_SECRET in Netlify environment variables.
Deploy the topindustry folder as the Netlify site.
Real automatic payment processing requires a supported payment provider's merchant/API credentials and verified webhook. Do not put secret API keys in public/index.html.
Gravatar profile integration
The site now includes the public Gravatar profile card for the supplied profile URL: https://gravatar.com/isayaokeba4
No Gravatar API key is embedded in the frontend. The profile card is loaded through the public profile-card URL.
Render deployment
This package includes render.yaml. For the easiest deployment, put this folder in a GitHub repository and in Render choose New → Blueprint, then select the repository. Render will create the web service and PostgreSQL database from the blueprint.
After deployment, open the generated onrender.com URL. The server serves the website and /api/* from the same service.
