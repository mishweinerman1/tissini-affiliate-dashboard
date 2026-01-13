# Tissini TikTok Affiliate Program Dashboard

Interactive dashboard for managing and planning the Tissini TikTok affiliate program.

## Features

- **Dynamic Calculations**: Edit input fields (yellow) and watch calculated fields (green) update automatically
- **10 Interactive Tabs**: Overview, Economics, Training, Content Strategy, Tracking, Recruitment, Support, Implementation, Legal, Comparison
- **Revenue Projections**: Fully editable financial models with real-time calculations
- **Training Curriculum**: Complete 6-module affiliate training program
- **Content Strategy**: 7 content types with video scripts and examples
- **Search Functionality**: Search across all dashboard content
- **Interactive Checkboxes**: Click to mark tasks complete with progress tracking
- **🔐 User Authentication**: Secure login/signup system with Supabase
- **🔥 Multi-User Sync**: Real-time collaboration across all team members
- **Persistent Data**: Saved to PostgreSQL database (Supabase)

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
1. Users visit dashboard and see **login modal**
2. Create account or login with existing credentials
3. Check boxes to mark tasks complete
4. Changes **instantly sync** to all logged-in team members
5. All data persists in cloud database

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
