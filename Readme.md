# News and Media Portal

A Django web application for sharing news, sports updates, and event information.

## Project Overview

News and Media Portal is a Django-based web application designed to provide a platform for publishing and managing news articles, sports updates, and events. The application features a responsive design, user authentication system, and email verification for account security.

## Features

- **Multiple Content Sections**:
  - News articles with categories
  - Sports updates with team and player information
  - Event listings with date, location, and registration

- **User Management**:
  - User registration with email verification
  - Profile management
  - Role-based access control

- **Responsive Design**:
  - Bootstrap 5 framework
  - Mobile-friendly interface
  - Customized UI elements

- **Admin Dashboard**:
  - Content management system
  - User management interface
  - Site configuration options

## Environment Setup

### Environment Variables

Create a `.env` file in the project root with the following variables:

```properties
# Environment Configuration
# Set to True for development, False for production
DEBUG=True
ENVIRONMENT=development

# Email Configuration
EMAIL_BACKEND=django.core.mail.backends.smtp.EmailBackend
EMAIL_HOST=smtp.gmail.com
EMAIL_PORT=587
EMAIL_USE_TLS=True
EMAIL_HOST_USER=your-gmail@gmail.com
EMAIL_HOST_PASSWORD=your-app-password
DEFAULT_FROM_EMAIL=your-gmail@gmail.com

# Domain Settings
ALLOWED_HOSTS=127.0.0.1,localhost,0.0.0.0,your-production-domain.com

# CSRF Trusted Origins
CSRF_TRUSTED_ORIGINS=https://your-production-domain.com
```

### Email Setup Instructions

To set up email for verification and notifications:

1. Go to https://myaccount.google.com/security
2. Enable 2-Factor Authentication if not already enabled
3. Under "Signing in to Google", click "App passwords"
4. Select "Mail" and "Windows Computer"
5. Click "Generate" and copy the 16-character password
6. Add the password to your `.env` file

## Running the Project

### Development Mode

1. Clone the repository:
   ```
   git clone https://github.com/your-username/news-and-media-beta.git
   cd news-and-media-beta
   ```

2. Create and activate a virtual environment:
   ```
   python -m venv venv
   venv\Scripts\activate
   ```

3. Install dependencies:
   ```
   pip install -r requirements.txt
   ```

4. Configure your `.env` file with development settings:
   ```
   DEBUG=True
   ENVIRONMENT=development
   ```

5. Run migrations:
   ```
   python manage.py migrate
   ```

6. Create a superuser:
   ```
   python manage.py createsuperuser
   ```

7. Run the development server:
   ```
   python manage.py runserver
   ```

8. Access the site at: http://127.0.0.1:8000

### Production Mode

1. Configure your `.env` file with production settings:
   ```
   DEBUG=False
   ENVIRONMENT=production
   ```

2. Collect static files:
   ```
   python manage.py collectstatic
   ```

3. Run the production server using Waitress:
   ```
   python waitress_server.py
   ```
   
   This will start a production-ready server at http://localhost:8000

4. For deployment behind a proxy (recommended):
   - Configure Nginx or Apache as a reverse proxy
   - Set up SSL/TLS certificates for HTTPS
   - Configure proper caching headers

## Troubleshooting

### CSRF Verification Failed

If you encounter CSRF verification errors:

1. Check your `.env` file has properly configured `CSRF_TRUSTED_ORIGINS`:
   ```
   CSRF_TRUSTED_ORIGINS=https://your-domain.com,https://*.your-domain.com
   ```

2. Ensure all URLs in `CSRF_TRUSTED_ORIGINS` start with `https://` or `http://`

3. If using a custom domain, make sure it's included in both:
   - `ALLOWED_HOSTS`
   - `CSRF_TRUSTED_ORIGINS`

4. For local development behind a proxy, add your local URL:
   ```
   CSRF_TRUSTED_ORIGINS=https://your-domain.com,http://localhost:8000
   ```

5. Verify your templates include the `{% csrf_token %}` tag in all forms

### Static Files Issues

If static files aren't loading correctly:

1. Run `python manage.py collectstatic`
2. Check that the `STATIC_ROOT` directory exists
3. Ensure `STATICFILES_STORAGE` is properly configured in `settings.py`
4. In production, configure your web server to serve static files

### Email Verification Problems

If email verification isn't working:

1. Test your email configuration with the provided script:
   ```
   python test_email_config.py
   ```

2. Check that your Google account has 2-Factor Authentication enabled and you're using App Passwords
3. Verify email settings in your `.env` file
4. Check application logs for detailed error messages

## Additional Information

- The application uses Django 5.2.4
- Built with Python 3.13
- Frontend uses Bootstrap 5
- Security features include CSRF protection and secure email verification
