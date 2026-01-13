# Tissini TikTok Affiliate Program Dashboard

Interactive dashboard for managing and planning the Tissini TikTok affiliate program.

## Features

### Core Dashboard
- **10 Interactive Tabs**: Overview, Economics, Training, Content Strategy, Tracking, Recruitment, Support, Implementation, Legal, Comparison
- **Dynamic Calculations**: Edit input fields (yellow) and watch calculated fields (green) update automatically
- **Revenue Projections**: Fully editable financial models with real-time calculations
- **Training Curriculum**: Complete 6-module affiliate training program
- **Content Strategy**: 7 content types with video scripts and examples
- **Search Functionality**: Search across all dashboard content

### Authentication & Security
- **🔐 User Authentication**: Secure login/signup system with Supabase
- **🔒 Read-Only for Visitors**: Non-authenticated users can view the latest version but cannot edit
- **👥 Multi-User Support**: Team members can collaborate in real-time
- **🔑 Row Level Security**: Database-level security ensures data privacy

### Task Management
- **✅ Interactive Checkboxes**: Click to mark tasks complete with progress tracking
- **➕ Add Custom Tasks**: Easily add new tasks to any week (Week 1-8)
- **📊 Progress Tracking**: Real-time progress bar shows completion percentage
- **🔄 Real-Time Sync**: Changes sync instantly across all users
- **💾 Persistent Data**: All data saved to PostgreSQL database (Supabase)

## Quick Deploy to Netlify

### Option 1: Drag & Drop (Easiest)
1. Go to [app.netlify.com](https://app.netlify.com)
2. Sign up/log in (free account)
3. Drag this entire folder onto the Netlify dashboard
4. Your site will be live at `[random-name].netlify.app`

### Option 2: Netlify CLI
```bash
# Install Netlify CLI
npm install -g netlify-cli

# Login to Netlify
netlify login

# Deploy
netlify deploy --prod
```

### Option 3: Git-Based Deployment
1. Initialize git repository:
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   ```
2. Push to GitHub
3. Connect GitHub repo to Netlify for automatic deployments

## Custom Domain

To use a custom domain:
1. Deploy to Netlify
2. Go to Site Settings → Domain Management
3. Add your custom domain (e.g., `affiliate.tissini.com`)
4. Update DNS records as instructed

## 🔥 Multi-User Sync Setup (Required for Team Collaboration)

Enable real-time collaboration with **Supabase** so your entire team can see checkbox updates instantly!

### Quick Setup (20 minutes):

1. **Create Supabase Project**: [supabase.com](https://supabase.com)
2. **Create Database Table**: Run provided SQL to set up checkboxes table
3. **Get Credentials**: Copy Project URL and anon key from API settings
4. **Update Dashboard**: Replace `SUPABASE_URL` and `SUPABASE_ANON_KEY` in `index.html`
5. **Deploy**: Upload to Netlify and create your first account

**📖 Full Instructions**: See [SUPABASE_SETUP.md](./SUPABASE_SETUP.md) for detailed step-by-step guide

### Benefits:
- ✅ **Secure Authentication** - Users must login to access
- ✅ **Real-time sync** across all team members
- ✅ **PostgreSQL database** - Enterprise-grade data storage
- ✅ **See updates instantly** (no refresh needed)
- ✅ **Connection status indicator**
- ✅ **Audit trail** - See who changed what and when
- ✅ **Free tier** supports up to 50,000 users
- ✅ **Row Level Security** - Data is secure by default

### How It Works:

**For Team Members (Authenticated):**
1. Visit dashboard and see **login modal**
2. Create account or login with existing credentials
3. ✅ Check/uncheck boxes to mark tasks complete
4. ➕ Add new tasks to any week using the task selector
5. Changes **instantly sync** to all team members
6. All edits persist in cloud database

**For Visitors (Non-Authenticated):**
1. Visit dashboard and see the **latest version**
2. Can view all content and current task status
3. Cannot edit or check boxes (read-only mode)
4. Perfect for sharing progress with stakeholders

## File Structure

```
tissini-affiliate-deploy/
├── index.html              # Main dashboard file with Supabase integration
├── netlify.toml            # Netlify configuration
├── README.md               # This file
├── DEPLOY.md               # Quick deploy instructions
├── CHANGES.md              # Changelog of recent updates
├── SUPABASE_SETUP.md       # Step-by-step Supabase setup guide
└── .gitignore              # Git ignore rules
```

## Technical Details

- **Backend**: Supabase (PostgreSQL + Real-time subscriptions)
- **Authentication**: Supabase Auth (email/password with optional verification)
- **Dependencies**: Supabase JavaScript SDK (loaded from CDN)
- **Browser Compatibility**: Works in all modern browsers
- **Mobile Responsive**: Optimized for desktop, tablet, and mobile
- **Data Storage**: PostgreSQL database with Row Level Security
- **Real-Time Updates**: Instant sync via Supabase real-time subscriptions
- **Security**: RLS policies ensure only authenticated users can access data

## Editing Content

All content is embedded in the HTML file. To edit:
1. Open `index.html` in a text editor
2. Find the section you want to modify
3. Update the content
4. Save and redeploy

## Dashboard Tabs

1. **Overview**: Program summary, key metrics, success factors
2. **Economics**: Commission tiers, revenue projections, ROI analysis
3. **Training**: 6-module curriculum for affiliates
4. **Content Strategy**: 7 content types with scripts and examples
5. **Tracking**: TikTok Pixel, Northbeam, Refersion setup
6. **Recruitment**: Strategies to find and onboard affiliates
7. **Weekly Support**: Support program, competitions, incentives
8. **Implementation**: Complete roadmap from pre-launch to growth
9. **Legal**: FTC compliance, agreements, risk mitigation
10. **Comparison**: Affiliate vs Emprendedora model analysis

## Support

For questions or issues, contact the Tissini team.

---

**Built with Claude Code** • January 2026
