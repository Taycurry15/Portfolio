# Deploy to keontaycurry.com with GitHub Pages
## Quick Setup Guide (20 Minutes)

---

## 🎯 WHAT YOU'LL ACCOMPLISH

Deploy your GRC Executive portfolio to:
- ✅ **https://www.keontaycurry.com** (primary)
- ✅ **https://keontaycurry.com** (redirects to www)
- ✅ Free HTTPS/SSL certificate
- ✅ Fast global CDN
- ✅ Easy updates via GitHub

---

## 📋 FILES TO DEPLOY

You have 4 files ready to upload:
1. ✅ `index.html` - Your portfolio
2. ✅ `robots.txt` - SEO instructions
3. ✅ `sitemap.xml` - Site map for search engines
4. ✅ `CNAME` - Custom domain configuration

---

## 🚀 STEP 1: CREATE GITHUB REPOSITORY (5 minutes)

### **Option A: Via GitHub Web (Easiest)**

1. **Go to GitHub:**
   - Navigate to: https://github.com/new

2. **Repository Settings:**
   ```
   Repository name: taycurry15.github.io
   Description: GRC Executive Portfolio - keontaycurry.com
   Public: ✅ (MUST be public)
   Initialize: Leave unchecked
   ```

3. **Click "Create repository"**

### **Option B: Command Line**

```bash
# If you prefer terminal - skip if you did Option A
gh repo create taycurry15.github.io --public --description "GRC Executive Portfolio"
```

---

## 📤 STEP 2: UPLOAD YOUR FILES (5 minutes)

### **Option A: Via GitHub Web Interface (Recommended)**

1. **On your new repository page, click:**
   - "uploading an existing file" link

2. **Drag and drop these 4 files:**
   - `index.html`
   - `robots.txt`
   - `sitemap.xml`
   - `CNAME`

3. **Commit:**
   ```
   Commit message: Initial portfolio deployment with custom domain
   ```

4. **Click "Commit changes"**

### **Option B: Via Command Line**

```bash
# Navigate to your portfolio folder
cd /mnt/user-data/outputs

# Initialize git
git init
git add index.html robots.txt sitemap.xml CNAME

# Commit
git commit -m "Initial portfolio deployment with custom domain"

# Add remote and push
git branch -M main
git remote add origin https://github.com/taycurry15/taycurry15.github.io.git
git push -u origin main
```

---

## 🌐 STEP 3: CONFIGURE DNS (10 minutes)

**Where is your domain registered?**
- Namecheap
- GoDaddy
- Google Domains
- Cloudflare
- Other

### **DNS Configuration (Same for all registrars)**

**1. Log into your domain registrar**

**2. Find DNS Settings:**
- Namecheap: "Advanced DNS" tab
- GoDaddy: "DNS" → "Manage Zones"
- Google Domains: "DNS" section
- Cloudflare: "DNS" section

**3. Add these 4 A Records:**

```
Type: A
Host: @ (or leave blank or use "keontaycurry.com")
Value: 185.199.108.153
TTL: 3600 (or Auto)

Type: A
Host: @
Value: 185.199.109.153
TTL: 3600

Type: A
Host: @
Value: 185.199.110.153
TTL: 3600

Type: A
Host: @
Value: 185.199.111.153
TTL: 3600
```

**4. Add CNAME Record for www:**

```
Type: CNAME
Host: www
Value: taycurry15.github.io
TTL: 3600
```

### **Visual Example (Namecheap)**

Your DNS records should look like this:

| Type  | Host | Value                  | TTL  |
|-------|------|------------------------|------|
| A     | @    | 185.199.108.153        | 3600 |
| A     | @    | 185.199.109.153        | 3600 |
| A     | @    | 185.199.110.153        | 3600 |
| A     | @    | 185.199.111.153        | 3600 |
| CNAME | www  | taycurry15.github.io   | 3600 |

**5. Delete any existing A or CNAME records** that point to old hosting

**6. Save changes**

---

## ✅ STEP 4: ENABLE GITHUB PAGES (2 minutes)

1. **Go to your repository settings:**
   - https://github.com/taycurry15/taycurry15.github.io/settings/pages

2. **Configure:**
   ```
   Source: Deploy from a branch
   Branch: main
   Folder: / (root)
   ```

3. **Click "Save"**

4. **Custom domain (should auto-populate from CNAME file):**
   ```
   Custom domain: www.keontaycurry.com
   ```
   - If not auto-filled, type it in
   - Click "Save"

5. **Wait 5-10 minutes, then:**
   - ✅ Check "Enforce HTTPS"
   - Click "Save"

---

## ⏱️ STEP 5: WAIT FOR DNS PROPAGATION

**Typical wait times:**
- Minimum: 15-30 minutes
- Average: 1-2 hours
- Maximum: 24-48 hours

**Check propagation status:**
- Visit: https://www.whatsmydns.net
- Enter: `keontaycurry.com`
- Should show: `185.199.108.153` (and other 3 IPs)

**Check CNAME:**
- Enter: `www.keontaycurry.com`
- Should show: `taycurry15.github.io`

---

## 🎉 STEP 6: VERIFY IT WORKS

**Test these URLs (after DNS propagates):**

1. ✅ https://www.keontaycurry.com (main site)
2. ✅ https://keontaycurry.com (should redirect to www)
3. ✅ https://www.keontaycurry.com/robots.txt (should show)
4. ✅ https://www.keontaycurry.com/sitemap.xml (should show)

**Check these features:**
- Portfolio loads correctly
- Dark mode works
- All sections visible
- Links work
- Mobile responsive
- HTTPS (green lock icon)

---

## 🔧 TROUBLESHOOTING

### **Problem: "www.keontaycurry.com" not working**

**Check:**
1. CNAME file exists in repo with `www.keontaycurry.com`
2. All 4 A records added to DNS
3. CNAME record added to DNS
4. DNS propagation complete (use whatsmydns.net)
5. GitHub Pages custom domain is set to `www.keontaycurry.com`

**Solution:**
```bash
# Verify CNAME file
cat CNAME
# Should show: www.keontaycurry.com

# If wrong, update it
echo "www.keontaycurry.com" > CNAME
git add CNAME
git commit -m "Fix CNAME"
git push
```

### **Problem: HTTPS not available**

**Wait:** 10-15 minutes after DNS propagates

**If still not working:**
1. Go to Settings → Pages
2. Uncheck "Enforce HTTPS"
3. Save
4. Wait 1 minute
5. Re-check "Enforce HTTPS"
6. Save

### **Problem: "keontaycurry.com" (non-www) not redirecting**

**Check:**
- All 4 A records are present in DNS
- DNS has propagated

**Force redirect in GitHub:**
- This should happen automatically
- If not, just tell people to use www.keontaycurry.com

### **Problem: 404 Error**

**Check:**
1. Files uploaded to repo
2. `index.html` is in repo root (not in a folder)
3. Repository is public
4. GitHub Pages is enabled
5. Wait 2-3 minutes after pushing

**Force rebuild:**
```bash
git commit --allow-empty -m "Trigger rebuild"
git push
```

### **Problem: Old site still showing**

**Clear cache:**
- Hard refresh: Ctrl+Shift+R (Windows) or Cmd+Shift+R (Mac)
- Or open in incognito/private window

---

## 🔄 UPDATING YOUR SITE

### **Method 1: GitHub Web Interface (Easiest)**

1. Go to: https://github.com/taycurry15/taycurry15.github.io
2. Click on `index.html`
3. Click pencil icon (Edit this file)
4. Make your changes
5. Scroll down, commit message: "Update experience section"
6. Click "Commit changes"
7. Wait 1-2 minutes → Changes are live at www.keontaycurry.com

### **Method 2: Command Line (Faster for frequent updates)**

```bash
# Navigate to your portfolio folder
cd /path/to/portfolio

# Make changes to index.html
# (use your favorite editor)

# Check what changed
git status

# Add changes
git add index.html

# Commit
git commit -m "Update skills section"

# Push to GitHub
git push

# Wait 1-2 minutes → Live!
```

### **Method 3: GitHub Desktop (Visual)**

1. Download: https://desktop.github.com
2. Clone your repo
3. Edit files in your editor
4. GitHub Desktop shows changes
5. Commit + Push
6. Live in 1-2 minutes

---

## 📊 POST-DEPLOYMENT SEO TASKS

### **Immediate (Within 24 Hours)**

**1. Google Search Console:**
- Go to: https://search.google.com/search-console
- Add property: `www.keontaycurry.com`
- Verify ownership (DNS or HTML file)
- Submit sitemap: `https://www.keontaycurry.com/sitemap.xml`
- Request indexing for homepage

**2. Bing Webmaster Tools:**
- Go to: https://www.bing.com/webmasters
- Add site: `www.keontaycurry.com`
- Verify ownership
- Submit sitemap

**3. Update LinkedIn:**
- Profile → Contact Info
- Website: https://www.keontaycurry.com
- Featured section: Add website link

**4. Update Email Signature:**
```
Keontay Curry, CISM, MBA
GRC Executive & CISO
📧 kcurry@thebronzeshield.com
📱 502-812-8606
💼 linkedin.com/in/keontaycurry
🌐 www.keontaycurry.com
```

### **First Week:**

1. Create Google My Business
2. Add to 10 business directories
3. Share on LinkedIn
4. Monitor Google Analytics (if added)

---

## 📈 EXPECTED TIMELINE

**Immediate (0-5 min):**
- Repository created
- Files uploaded
- GitHub Pages enabled

**Short wait (15 min - 2 hours):**
- DNS propagation
- HTTPS certificate issued
- Site accessible

**Medium wait (24-48 hours):**
- Google indexes site
- Full DNS propagation globally
- Rankings begin

**Long term (30-90 days):**
- Page 1 rankings for your name
- Top 20 for "GRC Executive Louisville"
- Recruiter inquiries start

---

## ✅ DEPLOYMENT CHECKLIST

**Before deploying:**
- [x] index.html updated with your info ✅
- [x] All URLs use www.keontaycurry.com ✅
- [x] robots.txt ready ✅
- [x] sitemap.xml ready ✅
- [x] CNAME file created ✅
- [ ] Tested locally (opened index.html)

**Deployment steps:**
- [ ] GitHub repo created: taycurry15.github.io
- [ ] All 4 files uploaded
- [ ] 4 A records added to DNS
- [ ] 1 CNAME record added to DNS
- [ ] GitHub Pages enabled
- [ ] Custom domain set to www.keontaycurry.com
- [ ] HTTPS enforced
- [ ] DNS propagation verified

**Post-deployment:**
- [ ] Site loads at www.keontaycurry.com
- [ ] HTTPS works (green lock)
- [ ] Mobile responsive
- [ ] All sections display
- [ ] Submitted to Google Search Console
- [ ] Submitted to Bing Webmaster
- [ ] LinkedIn updated with website link

---

## 💡 PRO TIPS

### **Tip 1: Test Before Going Live**

Before DNS propagation, test at:
- https://taycurry15.github.io

This shows how your site will look once DNS is ready.

### **Tip 2: Keep GitHub URL as Backup**

Even with custom domain, your site is also available at:
- https://taycurry15.github.io

If DNS ever has issues, this always works.

### **Tip 3: Monitor Uptime**

Use free monitoring:
- **UptimeRobot:** https://uptimerobot.com
- Get email if site goes down
- Free for 50 monitors

### **Tip 4: Add Google Analytics**

Track visitors:
1. Create GA4 property
2. Get tracking ID
3. Add to index.html before `</head>`:

```html
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-XXXXXXXXXX');
</script>
```

### **Tip 5: Create Professional Email**

With your domain, you can create:
- keontay@keontaycurry.com
- hello@keontaycurry.com
- contact@keontaycurry.com

**Options:**
- Google Workspace: $6/month
- Namecheap Email: $1/month
- Cloudflare Email Routing: Free

---

## 🎯 QUICK REFERENCE

**Your URLs:**
- Portfolio: https://www.keontaycurry.com
- Robots: https://www.keontaycurry.com/robots.txt
- Sitemap: https://www.keontaycurry.com/sitemap.xml
- GitHub: https://github.com/taycurry15/taycurry15.github.io
- GitHub Pages: https://taycurry15.github.io (backup)

**DNS Records:**
```
A    @    185.199.108.153
A    @    185.199.109.153
A    @    185.199.110.153
A    @    185.199.111.153
CNAME www  taycurry15.github.io
```

**GitHub Settings:**
```
Repo: taycurry15.github.io
Source: Branch main, folder / (root)
Custom domain: www.keontaycurry.com
Enforce HTTPS: ✅
```

---

## 📞 SUPPORT RESOURCES

**GitHub Pages Docs:**
https://docs.github.com/en/pages

**DNS Propagation Checker:**
https://www.whatsmydns.net

**GitHub Status:**
https://www.githubstatus.com

**Community Help:**
- GitHub Discussions
- Stack Overflow
- Reddit r/github

---

## 🚀 READY TO DEPLOY?

**Estimated Time: 20 minutes**
- 5 min: Create repo & upload files
- 10 min: Configure DNS
- 5 min: Enable GitHub Pages & verify

**Cost: $0**
- GitHub Pages: Free
- HTTPS: Free
- CDN: Free
- Domain: You already own it ✅

---

## 📋 QUICK START COMMANDS

**If you're comfortable with command line, here's everything:**

```bash
# 1. Navigate to your files
cd /mnt/user-data/outputs

# 2. Initialize and deploy
git init
git add index.html robots.txt sitemap.xml CNAME
git commit -m "Deploy GRC Executive portfolio to keontaycurry.com"
git branch -M main
git remote add origin https://github.com/taycurry15/taycurry15.github.io.git
git push -u origin main

# 3. Go configure DNS (see Step 3 above)

# 4. Enable GitHub Pages at:
# https://github.com/taycurry15/taycurry15.github.io/settings/pages

# Done!
```

---

## 🎉 NEXT STEPS

**After your site is live:**

1. **Test everything** (links, mobile, dark mode)
2. **Submit to search engines** (Google, Bing)
3. **Update LinkedIn** with website link
4. **Share** on social media
5. **Monitor** Google Search Console
6. **Start creating content** (blog posts)
7. **Get backlinks** (directories, associations)

**Within 30 days:**
- 100+ visitors
- Indexed by Google
- First recruiter contacts

**Within 90 days:**
- Page 1 for your name
- Top 20 for target keywords
- Multiple interview requests

---

## ✅ YOU'RE READY!

Your portfolio is professionally built, SEO-optimized, and ready to deploy.

**Start with Step 1 and work through each step.**

**Questions? Check troubleshooting or refer to GitHub Pages documentation.**

**Let's get you live on www.keontaycurry.com! 🚀**
