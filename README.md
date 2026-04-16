# Fidra-Instagram-Accounts-Creator
TABLE OF CONTENTS
-----------------
1. Disclaimer
2. Features
3. Prerequisites
4. Installation
5. Configuration
6. Usage
7. How It Works
8. Error Handling
9. Monitoring
10. Anti-Detection Features
11. Troubleshooting
12. File Structure
13. Performance
14. Security Recommendations

================================================================================
1. DISCLAIMER
================================================================================

THIS TOOL IS FOR EDUCATIONAL PURPOSES ONLY. Creating fake or unauthorized 
Instagram accounts violates Instagram's Terms of Service. Use at your own risk. 
The developers are not responsible for any misuse or consequences arising from 
using this tool.

By using this tool, you agree that you will only use it on accounts you own or 
have explicit permission to manage.

================================================================================
2. FEATURES
================================================================================

✓ Automated Account Creation - Creates Instagram accounts with random usernames 
  and passwords

✓ Gmail Integration - Uses IMAP to fetch verification codes automatically

✓ Dot-Email Technique - Generates unlimited unique email addresses from one 
  Gmail account

✓ Multi-Credential Support - Rotates through multiple Gmail credentials 
  automatically

✓ Profile Customization - Sets random profile pictures from local folder

✓ Auto-Posting - Uploads random posts from specified folder

✓ Auto-Following - Follows target accounts after creation

✓ Telegram Notifications - Sends account details to Telegram when created

✓ Session Management - Saves account credentials and session IDs

✓ Banned Email Tracking - Automatically removes banned credentials

✓ Proxy Support - Configurable proxy rotation

✓ Error Recovery - Automatic retry and credential switching

================================================================================
3. PREREQUISITES
================================================================================

Required Software:
------------------
- Python 3.7 or higher
- Gmail account(s) with App Password enabled
- Proxy support (recommended for high-volume creation)
- Internet connection

Gmail Setup:
------------
1. Go to Google Account Settings
2. Navigate to Security → 2-Step Verification
3. Enable 2-Step Verification if not already enabled
4. Go to Security → App Passwords
5. Select "Mail" as the app and your device
6. Generate and save the 16-character password

================================================================================
4. INSTALLATION
================================================================================

Step 1: Clone or Download the Repository
-----------------------------------------
git clone https://github.com/yourusername/instagram-account-generator.git
cd instagram-account-generator

OR download the ZIP file and extract it.

Step 2: Install Required Packages
----------------------------------
pip install -r requirements.txt

Manual installation if requirements.txt is not available:
pip install curl_cffi instagrapi names requests

Step 3: Create Required Folders
--------------------------------
Create these folders in the same directory as main.py:
- Avatars/     (for profile pictures)
- Posts/       (for post images)

The accounts/ and sessions/ folders will be created automatically.

================================================================================
5. CONFIGURATION
================================================================================

5.1 credentials.txt - Gmail Credentials (REQUIRED)
---------------------------------------------------
Create a file named "credentials.txt" in the main directory.
Format: email:app_password (one per line)

Example:
your_email@gmail.com:abcd efgh ijkl mnop
second_email@gmail.com:qrst uvwx yz12 3456

Note: Remove spaces from the app password if present.

5.2 settings.json - Bot Settings (OPTIONAL)
-------------------------------------------
Create a file named "settings.json" in the main directory.

Example:
{
    "max_wait": 60,
    "interval": 2,
    "max_retries": 3,
    "retry_delay": 2,
    "follow_targets": ["target_username1", "target_username2"]
}

Settings Explanation:
- max_wait: Maximum seconds to wait for verification code (default: 60)
- interval: Seconds between checking for new emails (default: 2)
- max_retries: Number of retry attempts for failed actions (default: 3)
- retry_delay: Seconds to wait between retries (default: 2)
- follow_targets: List of Instagram usernames to follow (optional)

5.3 bot.json - Telegram Notifications (OPTIONAL)
------------------------------------------------
Create a file named "bot.json" in the main directory.

Example:
{
    "bot_token": "1234567890:ABCdefGHIjklMNOpqrsTUVwxyz",
    "chat_id": "123456789"
}

How to get Telegram credentials:
1. Message @BotFather on Telegram
2. Send /newbot and follow instructions to create a bot
3. Copy the bot token
4. Message your bot and send /start
5. Visit https://api.telegram.org/bot<YOUR_TOKEN>/getUpdates
6. Find your chat_id in the response

5.4 Folder Preparation
----------------------
Avatars Folder: Add profile pictures (.jpg, .png, .jpeg)
Posts Folder: Add images for posting (.jpg, .png, .jpeg)

Recommended:
- 10-20 different profile pictures
- 20-30 different post images
- Images should be square format (1080x1080 recommended)

================================================================================
6. USAGE
================================================================================

Basic Run:
----------
python main.py

What happens during execution:
-----------------------------
1. Tool loads credentials from credentials.txt
2. Filters out previously banned emails
3. Verifies Gmail authentication
4. Initializes Instagram headers
5. Generates dot-email variations
6. Sends verification request
7. Waits for and extracts verification code
8. Creates Instagram account
9. Uploads random profile picture
10. Uploads random post
11. Follows target accounts (if specified)
12. Saves account credentials
13. Sends Telegram notification (if configured)
14. Moves to next account creation

Keyboard Shortcuts:
------------------
Ctrl + C - Stop the bot gracefully

Output Files:
-------------
accounts/accounts_userpass.txt - Format: username:password
accounts/accounts_emailpass.txt - Format: email:password
accounts/accounts_full.json - Complete account info with session IDs
sessions/usersession.txt - Username:sessionid pairs
sessions/session.txt - Session IDs only

================================================================================
7. HOW IT WORKS
================================================================================

7.1 Dot-Email Technique
-----------------------
Original email: example@gmail.com
Generated variations:
  - example@gmail.com
  - e.xample@gmail.com
  - ex.ample@gmail.com
  - exa.mple@gmail.com
  - exam.ple@gmail.com
  - examp.le@gmail.com
  - exampl.e@gmail.com
  - e.x.a.m.p.l.e@gmail.com
  - And thousands more combinations

How it works:
- Gmail ignores dots in email addresses
- Instagram treats each dot variation as a unique email
- All emails go to the same Gmail inbox
- Each account requires a fresh verification code

7.2 Account Creation Flow
------------------------
Step 1: Load credentials from credentials.txt
Step 2: Verify Gmail credentials with IMAP
Step 3: Initialize Instagram session with random user agent
Step 4: Generate unique dot-email address
Step 5: Send verification request to Instagram
Step 6: Monitor Gmail inbox for verification code
Step 7: Extract 6-digit code from email subject
Step 8: Submit code for validation
Step 9: Create account with random username/password
Step 10: Save account information
Step 11: Set up profile picture
Step 12: Upload random post
Step 13: Follow specified targets
Step 14: Send notifications

7.3 Username Generation
-----------------------
Format: [random_name][timestamp]
Example: john12345678

Process:
1. Generate random first name using names library
2. Clean name (remove special characters)
3. Add timestamp (last 8 digits)
4. Ensure minimum 7 characters
5. Trim to maximum 30 characters if needed

7.4 Password Generation
-----------------------
Format: [First_name]@[random_numbers]
Example: John@456

Characteristics:
- Includes uppercase letter
- Includes lowercase letters
- Includes numbers
- Includes special character (@)
- Easy to remember

================================================================================
8. ERROR HANDLING
================================================================================

The bot automatically handles these scenarios:

8.1 Banned Emails
-----------------
When an email gets banned:
1. Email is added to banned_emails.json
2. Credential is removed from available list
3. Bot switches to next credential
4. Continues with remaining credentials

8.2 Proxy Detection
-------------------
If Instagram detects proxy usage:
1. Bot detects "open proxy" error
2. Bans the primary email
3. Switches to next credential
4. Continues creation process

8.3 Failed Authentication
-------------------------
If Gmail authentication fails:
1. Bot attempts to verify again
2. After multiple failures, switches credential
3. Continues with next available credential

8.4 Missing Verification Code
-----------------------------
If code is not received within max_wait time:
1. Bot logs the failure
2. Retries with same dot-email
3. If still failing, moves to next dot-email
4. Continues with same credential

8.5 Session Issues
------------------
If session becomes invalid:
1. Bot resets session state
2. Re-initializes headers
3. Continues from authentication step
4. No credential switching required

================================================================================
9. MONITORING
================================================================================

9.1 Console Output
------------------
The bot provides real-time status updates:

[+] Success indicators - Operation completed successfully
[ ] In-progress indicators - Currently processing
[⚠] Warning indicators - Non-critical issues
[✖] Error indicators - Critical failures
[🔄] Reset indicators - Session or credential reset
[✅] Verification indicators - Code received or validated

Example console output:
[+] Using credential: example@gmail.com
[+] Remaining credentials: 3
[+] Total accounts created so far: 5
[ ] Sending verification email to e.xample@gmail.com...
⏳ Waiting for code: 15s / 60s...
✅ Code received: 123456
🎉 Account created successfully!

9.2 Telegram Notifications
--------------------------
Each successful account creation sends:

🎉 New Instagram Account Created!

📧 Email: e.xample@gmail.com
👤 Username: john12345678
🔑 Password: John@456
🆔 SessionID: 1234567890.123456...
⏰ Created: 2024-01-15T10:30:00
📊 Account #5

Followed by Instagram configuration:
👤 Profile: @john12345678
🔗 Link: instagram.com/john12345678

9.3 Log Files
-------------
The bot doesn't create separate log files but all output is shown in console.
To save logs, redirect output:
python main.py > bot_log.txt 2>&1

================================================================================
10. ANTI-DETECTION FEATURES
================================================================================

10.1 Random User Agents
-----------------------
The bot rotates through random mobile user agents:
Mozilla/5.0 (Linux; Android 9; ABC123) AppleWebKit/537.36...

10.2 Human-like Delays
----------------------
- Random delays between actions (1-3 seconds)
- Variable waiting times for verification
- Natural timing patterns

10.3 Session Management
-----------------------
- New session for each account creation
- Cookies cleared between sessions
- Fresh headers for each attempt

10.4 Proxy Support
------------------
- Configurable proxy rotation
- Supports HTTP/HTTPS proxies
- Can integrate with proxy lists

10.5 Request Impersonation
--------------------------
- Uses curl_cffi for browser impersonation
- Mimics Chrome 110 behavior
- Includes all required headers and cookies

================================================================================
11. TROUBLESHOOTING
================================================================================

Common Issues and Solutions:

Issue 1: "Gmail authentication failed"
---------------------------------------
Possible causes:
- Incorrect app password
- 2-Step Verification not enabled
- Less secure app access disabled

Solutions:
1. Generate a new app password
2. Enable 2-Step Verification
3. Check if IMAP is enabled in Gmail settings
4. Verify credentials.txt format (email:password)

Issue 2: "IP flagged as proxy"
-------------------------------
Possible causes:
- Using datacenter proxies
- Creating too many accounts too quickly
- IP address blacklisted

Solutions:
1. Switch to residential proxies
2. Increase delays between creations
3. Use different Gmail credentials
4. Wait 24 hours before retrying

Issue 3: "Could not fetch code"
--------------------------------
Possible causes:
- Email in spam folder
- Instagram not sending emails
- IMAP connection issues

Solutions:
1. Check spam folder manually
2. Increase max_wait in settings.json
3. Verify email routing (dot-email working)
4. Restart the bot

Issue 4: "No credentials found"
--------------------------------
Possible causes:
- credentials.txt missing
- Wrong format in credentials.txt
- All credentials banned

Solutions:
1. Create credentials.txt file
2. Use format: email:app_password
3. Add new credentials
4. Check banned_emails.json

Issue 5: "Failed to upload profile picture"
--------------------------------------------
Possible causes:
- Account suspended
- Invalid session
- Wrong image format

Solutions:
1. Check if account was created successfully
2. Verify session ID is valid
3. Use JPG or PNG format
4. Ensure images are not corrupted

Issue 6: "Signup blocked" error
--------------------------------
Possible causes:
- Instagram detected automation
- IP address flagged
- Too many attempts

Solutions:
1. Switch to different credential
2. Use residential proxy
3. Wait 24-48 hours
4. Reduce creation frequency

================================================================================
12. FILE STRUCTURE
================================================================================

Complete directory structure after running:

instagram-account-generator/
│
├── main.py                      # Main bot script
├── credentials.txt              # Gmail credentials (required)
├── settings.json                # Bot configuration (optional)
├── bot.json                     # Telegram config (optional)
├── banned_emails.json           # Banned email tracking (auto-generated)
│
├── Avatars/                     # Profile pictures folder
│   ├── pic1.jpg
│   ├── pic2.png
│   └── ...
│
├── Posts/                       # Post images folder
│   ├── post1.jpg
│   ├── post2.png
│   └── ...
│
├── accounts/                    # Generated account data
│   ├── accounts_userpass.txt    # username:password
│   ├── accounts_emailpass.txt   # email:password
│   └── accounts_full.json       # Complete account info
│
├── sessions/                    # Session storage
│   ├── usersession.txt          # username:sessionid
│   └── session.txt              # sessionid only
│
└── dot_emails_*.txt             # Generated dot emails
    (one file per credential, e.g., dot_emails_example_gmail_com.txt)

File Formats:
-------------
credentials.txt:
example@gmail.com:abcd efgh ijkl mnop
test@gmail.com:qrst uvwx yz12 3456

accounts_userpass.txt:
john12345678:John@456
jane87654321:Jane@789

accounts_emailpass.txt:
e.xample@gmail.com:John@456
j.ane@gmail.com:Jane@789

accounts_full.json:
[
  {
    "email": "e.xample@gmail.com",
    "username": "john12345678",
    "password": "John@456",
    "sessionid": "1234567890.123456...",
    "created_at": "2024-01-15T10:30:00"
  }
]

banned_emails.json:
{
  "banned_emails": [
    "banned_email@gmail.com",
    "blocked_account@gmail.com"
  ]
}

================================================================================
13. PERFORMANCE
================================================================================

Average Statistics:
------------------
Account Creation Time: 30-60 seconds per account
Success Rate: 70-90% (depends on proxy quality)
Daily Limit: 3-5 accounts per Gmail credential
Monthly Limit: 50-100 accounts per IP address

Resource Usage:
---------------
CPU: 5-10% average
RAM: 100-200 MB
Network: ~1-2 MB per account
Storage: ~1 KB per account (text files)

Factors Affecting Performance:
-----------------------------
1. Internet speed
2. Proxy quality (if used)
3. Gmail response time
4. Instagram server load
5. Time of day
6. Geographic location

Optimization Tips:
-----------------
1. Use high-speed internet connection
2. Choose residential proxies over datacenter
3. Run during off-peak hours
4. Use SSD storage
5. Keep system resources dedicated
6. Monitor and rotate proxies regularly

================================================================================
14. SECURITY RECOMMENDATIONS
================================================================================

Critical Security Practices:
---------------------------
1. NEVER commit credentials.txt to GitHub
2. NEVER commit bot.json to GitHub
3. NEVER share your app passwords
4. Use environment variables in production
5. Delete sensitive files when not in use

File Protection:
---------------
Add to .gitignore:
credentials.txt
bot.json
banned_emails.json
dot_emails_*.txt
accounts/
sessions/
__pycache__/
*.pyc
*.log

Environment Variables (Alternative to files):
--------------------------------------------
export GMAIL_CREDENTIALS="email1:pass1,email2:pass2"
export TELEGRAM_BOT_TOKEN="your_token"
export TELEGRAM_CHAT_ID="your_chat_id"

Proxy Security:
--------------
1. Use authenticated proxies
2. Rotate proxies regularly
3. Monitor proxy health
4. Don't share proxy credentials
5. Use HTTPS proxies when possible

Account Safety:
--------------
1. Don't reuse passwords
2. Don't link accounts to personal info
3. Use different email patterns
4. Warm up accounts before heavy use
5. Monitor account status regularly

Legal Compliance:
----------------
1. Only create accounts you own
2. Don't sell or transfer accounts
3. Comply with Instagram's Terms of Service
4. Respect privacy laws (GDPR, CCPA, etc.)
5. Don't use for spam or abuse

================================================================================
15. SUPPORT & CONTACT
================================================================================

Author: @f09l
Telegram Channels: 
- @ifostn
- @HexGalaxy

Issues and Contributions:
------------------------
Report issues on GitHub
Submit pull requests for improvements
Provide detailed error reports

================================================================================
16. VERSION HISTORY
================================================================================

Version 1.0 (Current):
- Initial release
- Basic account creation
- Gmail IMAP integration
- Dot-email technique
- Multi-credential support
- Telegram notifications
- Profile customization

================================================================================
17. LICENSE
================================================================================

This project is for educational purposes only.
No license is granted for commercial use.
Unauthorized use may violate Instagram's Terms of Service.

