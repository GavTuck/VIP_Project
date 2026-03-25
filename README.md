# VIP_Project

Technical Logic — Data & Attribution

Fields captured: First Name, Last Name, Email, Company, Phone, Guest Count, Dietary Restrictions, Submission Timestamp, and UTM parameters (source, medium, campaign).

Data flow: On submission, form data is posted to a serverless endpoint (e.g. Make/Zapier webhook or direct API call) that writes a record to HubSpot CRM — appending lead source, campaign tag, and device type before writing to the contacts database. A confirmation email triggers via HubSpot Workflows or a transactional provider like Postmark.

Source attribution: The page URL accepts ?utm_source=email&utm_medium=email&utm_campaign=vip_movie_2025 parameters. On load, JavaScript reads these params and passes them as hidden fields in the submission payload — so every record in the database is tagged with how the user arrived (Email, SMS, Direct Mail, or Direct). This surfaces in HubSpot as a custom property and in GA4 as a conversion event.

Tools of choice: Landing page hosted on Webflow (no-code, fast, mobile-first). Form submissions via native Webflow form → Zapier → HubSpot CRM. UTM tracking via GA4 + a custom HubSpot property. SMS traffic tracked by appending utm_medium=sms to the shortened link in the text blast. Direct Mail tracked via a unique vanity URL (e.g. acquire.com/vip) with utm_medium=direct-mail pre-appended.
