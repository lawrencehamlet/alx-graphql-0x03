# Sentry Error Monitoring Setup Guide

## Overview
Your application has been configured with Sentry error monitoring to track and log errors in production and development.

## What Has Been Done

### 1. ErrorBoundary Component Updated
The `components/ErrorBoundary.tsx` file now includes Sentry integration:
- Errors are logged to console (for development)
- Errors are automatically sent to Sentry using `Sentry.captureException()`

### 2. Sentry Configuration Files Created
Three configuration files have been created for different environments:
- `sentry.client.config.ts` - Client-side error tracking
- `sentry.server.config.ts` - Server-side error tracking
- `sentry.edge.config.ts` - Edge runtime error tracking

### 3. Next.js Configuration Updated
The `next.config.ts` file has been wrapped with `withSentryConfig()` to enable:
- Automatic source map uploads
- React component annotation
- Error tunneling through Next.js routes
- Automatic Vercel Cron monitoring

## Next Steps - How to Complete the Setup

### Step 1: Create a Sentry Account
1. Go to [https://sentry.io/signup/](https://sentry.io/signup/)
2. Sign up for a free account
3. Create a new project and select "Next.js" as the platform

### Step 2: Get Your Sentry DSN
1. After creating your project, you'll be shown a DSN (Data Source Name)
2. It looks like: `https://examplePublicKey@o0.ingest.sentry.io/0`
3. Copy this DSN

### Step 3: Configure Environment Variables
1. Create a `.env.local` file in the project root (if it doesn't exist)
2. Add your Sentry DSN:
```bash
NEXT_PUBLIC_SENTRY_DSN=your-actual-sentry-dsn-here
SENTRY_ORG=your-org-name
SENTRY_PROJECT=your-project-name
```

Example:
```bash
NEXT_PUBLIC_SENTRY_DSN=https://abc123@o123456.ingest.sentry.io/789012
SENTRY_ORG=my-company
SENTRY_PROJECT=alx-rick-and-morty-app
```

### Step 4: Test Error Logging
1. Make sure your development server is running:
   ```bash
   npm run dev
   ```

2. Open `pages/index.tsx` and uncomment the ErrorProneComponent:
   ```tsx
   {/* Uncomment to test error handling */}
   <ErrorBoundary>
     <ErrorProneComponent />
   </ErrorBoundary>
   ```

3. Visit `http://localhost:3000` in your browser

4. You should see:
   - The error boundary UI: "Oops, there is an error!"
   - The error logged in your browser console
   - The error appearing in your Sentry dashboard

### Step 5: Verify in Sentry Dashboard
1. Log in to your Sentry account
2. Go to your project dashboard
3. Navigate to "Issues" section
4. You should see the error: "This is a test error!"
5. Click on the error to see:
   - Stack trace
   - Error info
   - Browser details
   - User context

### Step 6: Take a Screenshot
Take a screenshot of the error in your Sentry dashboard showing:
- The error message
- The stack trace
- The timestamp
- Any additional context

## Important Notes

### For Development
- Errors will be logged to both console and Sentry
- The error boundary will catch and display errors gracefully
- Use the "Try again?" button to reset the error state

### For Production
- Make sure to set environment variables in your hosting platform (Vercel, Netlify, etc.)
- Sentry will help you track real user errors
- Configure alert rules in Sentry to get notified of critical errors

### Privacy Considerations
The current configuration includes:
- Session replay with masked text and blocked media
- Component name annotation for better debugging
- Automatic breadcrumb tracking

Adjust these settings in the Sentry config files based on your privacy requirements.

## Files Modified/Created

1. ✅ `components/ErrorBoundary.tsx` - Updated with Sentry integration
2. ✅ `components/ErrorProneComponent.tsx` - Test component that throws errors
3. ✅ `pages/_app.tsx` - Wrapped with ErrorBoundary
4. ✅ `sentry.client.config.ts` - Client-side Sentry configuration
5. ✅ `sentry.server.config.ts` - Server-side Sentry configuration
6. ✅ `sentry.edge.config.ts` - Edge runtime Sentry configuration
7. ✅ `next.config.ts` - Updated with Sentry webpack plugin
8. ✅ `.env.local.example` - Example environment variables

## Troubleshooting

### Error: "Sentry DSN not configured"
- Make sure you've created `.env.local` with your actual DSN
- Restart the development server after adding environment variables

### Errors not appearing in Sentry
- Check that your DSN is correct
- Verify your internet connection
- Check the browser console for any Sentry-related errors
- Make sure the error is actually being thrown (check console.log output)

### Build errors
- Ensure all Sentry packages are installed: `npm install`
- Check that your Next.js version is compatible with @sentry/nextjs

## Resources

- [Sentry Next.js Documentation](https://docs.sentry.io/platforms/javascript/guides/nextjs/)
- [Sentry React Error Boundary](https://docs.sentry.io/platforms/javascript/guides/react/features/error-boundary/)
- [Error Monitoring Best Practices](https://docs.sentry.io/product/issues/)
