# 🚀 Supabase Backend Setup Guide

## Overview

Your dashboard now uses **Supabase** for:
- ✅ **User Authentication** - Secure login/signup
- ✅ **PostgreSQL Database** - Persistent checkbox storage
- ✅ **Real-Time Sync** - Instant updates across all users
- ✅ **Row Level Security** - Each user sees shared team data

## Quick Start (20 minutes)

### Step 1: Create Supabase Project (5 min)

1. Go to **https://supabase.com**
2. Click **"Start your project"**
3. Sign in with GitHub (or email)
4. Click **"New project"**
5. Fill in details:
   - **Name**: `tissini-dashboard`
   - **Database Password**: Create a strong password (SAVE IT!)
   - **Region**: Choose closest to you
   - **Pricing Plan**: Free (more than enough!)
6. Click **"Create new project"**
7. Wait 2-3 minutes for project to initialize

### Step 2: Create Database Table (5 min)

1. In your Supabase project, click **"SQL Editor"** in left menu
2. Click **"New query"**
3. **Copy and paste this SQL:**

```sql
-- Create checkboxes table
CREATE TABLE checkboxes (
    id BIGSERIAL PRIMARY KEY,
    checkbox_id TEXT UNIQUE NOT NULL,
    checked BOOLEAN NOT NULL DEFAULT false,
    updated_by TEXT,
    updated_at TIMESTAMPTZ DEFAULT NOW(),
    created_at TIMESTAMPTZ DEFAULT NOW()
);

-- Enable Row Level Security
ALTER TABLE checkboxes ENABLE ROW LEVEL SECURITY;

-- Create policy: Authenticated users can read all checkboxes
CREATE POLICY "Authenticated users can read checkboxes"
    ON checkboxes FOR SELECT
    TO authenticated
    USING (true);

-- Create policy: Authenticated users can insert checkboxes
CREATE POLICY "Authenticated users can insert checkboxes"
    ON checkboxes FOR INSERT
    TO authenticated
    WITH CHECK (true);

-- Create policy: Authenticated users can update checkboxes
CREATE POLICY "Authenticated users can update checkboxes"
    ON checkboxes FOR UPDATE
    TO authenticated
    USING (true)
    WITH CHECK (true);

-- Create policy: Authenticated users can delete checkboxes
CREATE POLICY "Authenticated users can delete checkboxes"
    ON checkboxes FOR DELETE
    TO authenticated
    USING (true);

-- Enable Realtime
ALTER PUBLICATION supabase_realtime ADD TABLE checkboxes;

-- Create content_edits table (for inline editing)
CREATE TABLE content_edits (
    id BIGSERIAL PRIMARY KEY,
    content_id TEXT UNIQUE NOT NULL,
    content TEXT NOT NULL,
    updated_by TEXT,
    updated_at TIMESTAMPTZ DEFAULT NOW(),
    created_at TIMESTAMPTZ DEFAULT NOW()
);

-- Enable Row Level Security
ALTER TABLE content_edits ENABLE ROW LEVEL SECURITY;

-- Create policy: Authenticated users can read all content_edits
CREATE POLICY "Authenticated users can read content_edits"
    ON content_edits FOR SELECT
    TO authenticated
    USING (true);

-- Create policy: Authenticated users can insert content_edits
CREATE POLICY "Authenticated users can insert content_edits"
    ON content_edits FOR INSERT
    TO authenticated
    WITH CHECK (true);

-- Create policy: Authenticated users can update content_edits
CREATE POLICY "Authenticated users can update content_edits"
    ON content_edits FOR UPDATE
    TO authenticated
    USING (true)
    WITH CHECK (true);

-- Create policy: Authenticated users can delete content_edits
CREATE POLICY "Authenticated users can delete content_edits"
    ON content_edits FOR DELETE
    TO authenticated
    USING (true);

-- Enable Realtime for content_edits
ALTER PUBLICATION supabase_realtime ADD TABLE content_edits;
```

4. Click **"Run"** (or press Ctrl/Cmd + Enter)
5. You should see: **"Success. No rows returned"**

### Step 3: Get Your Credentials (2 min)

1. Click **"Settings"** (⚙️ gear icon) in left menu
2. Click **"API"** under Project Settings
3. Find these two values:

   **Project URL:**
   ```
   https://xxxxxxxxxxxxxx.supabase.co
   ```

   **anon/public key:**
   ```
   eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6...
   ```

4. **COPY BOTH** - you'll need them in the next step

### Step 4: Update Dashboard Configuration (5 min)

1. Open `index.html` in a text editor (VS Code, Sublime, Notepad++)
2. Find these lines (around line 2980):

```javascript
const SUPABASE_URL = 'YOUR_SUPABASE_URL_HERE'
const SUPABASE_ANON_KEY = 'YOUR_SUPABASE_ANON_KEY_HERE'
```

3. Replace with YOUR values:

```javascript
const SUPABASE_URL = 'https://xxxxxxxxxxxxxx.supabase.co'
const SUPABASE_ANON_KEY = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...'
```

4. **Save the file**

### Step 5: Deploy & Test (3 min)

1. **Upload to Netlify**: Drag the `tissini-affiliate-deploy` folder to https://app.netlify.com/drop
2. **Open the deployed URL**
3. You should see a **login modal**
4. Click **"Sign up"** to create your first account
5. Check your email for verification link (if email verification is enabled)
6. Log in!

## 🧪 Testing Multi-User Sync

### Test 1: Create Account & Login
1. Open dashboard → Click "Sign up"
2. Enter email and password
3. Check email for verification (if required)
4. Click "Login" and sign in
5. ✅ You should see your email in top-right corner

### Test 2: Check Boxes
1. Click any checkbox in the Implementation tab
2. It should check and show "✓ Synced"
3. ✅ Checkbox state saved to database

### Test 3: Multi-User Real-Time Sync
1. **Browser 1**: Login with User A
2. **Browser 2**: Login with User B (create second account)
3. **Browser 1**: Check a box
4. **Browser 2**: Watch it update in real-time! ⚡
5. ✅ Both users see the same state instantly

### Test 4: Persistence
1. Check several boxes
2. Close browser completely
3. Open dashboard and login again
4. ✅ All your checkboxes are still checked!

## 🔐 Security Features

### Row Level Security (RLS)
- Only authenticated users can access checkboxes
- Users must be logged in to see/modify data
- Database enforces security at row level

### Email Verification (Optional)
To require email verification before login:

1. Go to **Authentication** → **Settings** in Supabase
2. Scroll to **Email Auth**
3. Toggle **"Enable email confirmations"** ON
4. Users must verify email before they can login

### Password Requirements
Default: Minimum 6 characters
To make stricter:
1. Go to **Authentication** → **Settings**
2. Adjust password requirements under **Security**

## 📊 Monitoring Usage

### View Database Content
1. Go to **Table Editor** in Supabase
2. Click **"checkboxes"** table
3. See all checkbox states, who updated them, and when

### View Users
1. Go to **Authentication** in Supabase
2. Click **"Users"** tab
3. See all registered users
4. Can manually verify emails or delete users

### Real-Time Connections
1. Go to **Database** → **Realtime Inspector**
2. See active real-time connections
3. Monitor subscription status

## 🎨 Customization

### Change App Name
Edit the authentication modal in `index.html`:
```html
<h2>🔐 Login to Dashboard</h2>
```

### Change Email Templates
1. Go to **Authentication** → **Email Templates** in Supabase
2. Customize:
   - Confirmation email
   - Password reset email
   - Magic link email

### Add User Profiles
Create a `profiles` table to store additional user info:

```sql
CREATE TABLE profiles (
    id UUID REFERENCES auth.users PRIMARY KEY,
    full_name TEXT,
    avatar_url TEXT,
    created_at TIMESTAMPTZ DEFAULT NOW()
);
```

## 🐛 Troubleshooting

### "Please login to save your progress" alert
**Problem:** Not logged in
**Solution:** Click the alert, create account or login

### Login modal won't close
**Problem:** Credentials not set or incorrect
**Solution:**
1. Open browser console (F12)
2. Look for errors
3. Verify SUPABASE_URL and SUPABASE_ANON_KEY are correct

### "Failed to fetch" error
**Problem:** Wrong URL or network issue
**Solutions:**
- Check SUPABASE_URL is correct (should end in `.supabase.co`)
- Verify internet connection
- Check Supabase project is active (not paused)

### Real-time updates not working
**Solutions:**
1. Check if table has Realtime enabled:
   ```sql
   ALTER PUBLICATION supabase_realtime ADD TABLE checkboxes;
   ```
2. Go to **Database** → **Replication** in Supabase
3. Ensure `checkboxes` table is in the publication

### "Error saving checkbox" message
**Solutions:**
- Check Row Level Security policies are created
- Verify user is logged in
- Check browser console for specific error
- Go to **Database** → **Policies** to verify RLS rules

### Checkboxes not persisting after refresh
**Solutions:**
- Verify data is in database (Table Editor)
- Check if logged in (email should show in top-right)
- Clear browser cache and try again

## 💰 Pricing & Limits

### Free Tier Includes:
- ✅ **500 MB database** (you'll use <1 MB)
- ✅ **50,000 monthly active users**
- ✅ **500 MB file storage**
- ✅ **2 GB bandwidth**
- ✅ **50,000 realtime message credits**
- ✅ **2 GB data transfer**

**Your team dashboard will easily stay within free tier!**

### If You Exceed Free Tier:
- Supabase will notify you before charging
- Pro plan: $25/month (unlikely you'll need it)
- Can set spending limits in project settings

## 🔒 Production Best Practices

### 1. Enable Email Verification
Prevents spam accounts:
- Authentication → Settings → Enable email confirmations

### 2. Add Rate Limiting
Prevent abuse:
```sql
-- In SQL Editor, add rate limiting function
-- (Optional - Supabase has built-in rate limiting)
```

### 3. Backup Database
Enable point-in-time recovery:
- Settings → Database → Enable PITR (Pro plan feature)
- Or manually export via SQL Editor

### 4. Monitor Usage
- Check **Reports** tab regularly
- Set up alerts for unusual activity
- Review **Logs** for errors

### 5. Add Team Members
Share dashboard access:
1. Settings → Team → Invite members
2. They can help manage database/users
3. Doesn't count against user limits

## 🚀 Advanced Features

### Magic Link Login (Passwordless)
Enable magic link authentication:

```javascript
// In index.html, add this function:
async function sendMagicLink(email) {
    const { error } = await supabase.auth.signInWithOtp({
        email: email,
        options: {
            emailRedirectTo: window.location.origin
        }
    });
}
```

### Social Login (Google, GitHub, etc.)
1. Go to **Authentication** → **Providers**
2. Enable Google/GitHub/etc.
3. Add client ID and secret
4. Update login UI to include social buttons

### Audit Trail
Track who changed what:

```sql
-- Already included! Check updated_by and updated_at columns
SELECT checkbox_id, checked, updated_by, updated_at
FROM checkboxes
ORDER BY updated_at DESC;
```

## 📝 SQL Queries for Management

### See all checked items:
```sql
SELECT checkbox_id, updated_by, updated_at
FROM checkboxes
WHERE checked = true
ORDER BY updated_at DESC;
```

### Reset all checkboxes:
```sql
DELETE FROM checkboxes;
```

### See who's most active:
```sql
SELECT updated_by, COUNT(*) as changes
FROM checkboxes
GROUP BY updated_by
ORDER BY changes DESC;
```

### Export checkbox data:
1. Go to **Table Editor**
2. Click checkboxes table
3. Click **"Download as CSV"**

## 🆘 Support

- **Supabase Docs**: https://supabase.com/docs
- **Discord Community**: https://discord.supabase.com
- **GitHub Issues**: https://github.com/supabase/supabase/issues
- **Stack Overflow**: Tag questions with `supabase`

## ✅ Setup Checklist

- [ ] Created Supabase project
- [ ] Created `checkboxes` table with SQL
- [ ] Enabled Row Level Security policies
- [ ] Enabled Realtime on checkboxes table
- [ ] Copied Project URL and anon key
- [ ] Updated SUPABASE_URL in index.html
- [ ] Updated SUPABASE_ANON_KEY in index.html
- [ ] Deployed to Netlify
- [ ] Created test account
- [ ] Tested checkbox sync
- [ ] Tested multi-user real-time sync
- [ ] Invited team members

---

🎉 **Congratulations!** Your dashboard now has enterprise-grade authentication and real-time collaboration!

**Next:** Share the dashboard URL with your team and start collaborating!
