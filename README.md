# N8N Automated Customer Inquiry Classification & Escalation

AI-powered customer support automation built with **n8n**, **Gemini AI**, **Google Sheets**, and **Slack**. This workflow automatically classifies customer inquiries, routes them to the appropriate department, updates support records, and sends real-time notifications, reducing manual effort and improving response efficiency.

## 🎯 Overview

This solution automates the entire customer inquiry lifecycle:
- **Intelligent Classification**: Uses Gemini AI to automatically categorize incoming inquiries
- **Smart Routing**: Routes inquiries to appropriate departments based on classification
- **Real-time Notifications**: Sends instant alerts via Slack
- **Centralized Records**: Updates Google Sheets with inquiry data and status
- **Escalation Management**: Automatically escalates high-priority issues

## ✨ Key Features

- 🤖 **AI-Powered Classification** - Gemini AI analyzes customer inquiries and assigns categories
- 📊 **Google Sheets Integration** - Stores and tracks all inquiries and responses
- 💬 **Slack Notifications** - Real-time alerts for new inquiries and escalations
- 🔀 **Intelligent Routing** - Automatic department assignment based on inquiry type
- ⚡ **Automated Workflows** - n8n orchestrates the entire process
- 📈 **Performance Tracking** - Monitor inquiry resolution metrics

## 🛠️ Tech Stack

- **n8n** - Workflow automation and orchestration
- **Google Gemini AI** - Natural language processing and classification
- **Google Sheets** - Data storage and management
- **Slack** - Communication and notifications
- **Node.js** - Runtime environment

## 📋 Prerequisites

Before you begin, ensure you have:

- **n8n** installed and running (self-hosted or cloud)
- **Google Cloud Project** with:
  - Gemini AI API enabled
  - Service account with Google Sheets access
- **Slack Workspace** with admin access to create/manage integrations
- **Google Sheets** for data storage

## 🚀 Setup Instructions

### 1. Google Cloud Setup

1. Create a new Google Cloud Project
2. Enable the following APIs:
   - Google Sheets API
   - Gemini AI API
3. Create a Service Account:
   - Navigate to IAM & Admin → Service Accounts
   - Create a new service account
   - Generate and download the JSON key file
4. Share your Google Sheet with the service account email

### 2. Slack Integration

1. Go to [api.slack.com](https://api.slack.com/apps) and create a new app
2. Enable **Bot Token Scopes**:
   - `chat:write`
   - `chat:write.public`
   - `files:write`
3. Install the app to your workspace
4. Copy the Bot Token (starts with `xoxb-`)

### 3. n8n Configuration

1. **Import the Workflow**:
   - In n8n, create a new workflow or import the provided workflow file
   
2. **Configure Credentials**:
   - **Google Sheets**: Add service account credentials
   - **Gemini AI**: Add your API key
   - **Slack**: Add Bot Token
   
3. **Set Environment Variables**:
   ```env
   GOOGLE_SERVICE_ACCOUNT_KEY=<your-service-account-json>
   GEMINI_API_KEY=<your-gemini-api-key>
   SLACK_BOT_TOKEN=xoxb-<your-bot-token>
   ```

4. **Configure Nodes**:
   - Update Google Sheet IDs and ranges
   - Set Slack channel names for notifications
   - Customize classification categories as needed

## 📊 Workflow Process

```
Customer Inquiry Received
        ↓
   [Trigger Node]
        ↓
   Extract Inquiry Details
        ↓
   [Gemini AI Classification]
        ↓
   Determine Priority & Department
        ↓
   [Update Google Sheets]
        ↓
   [Route to Department]
        ↓
   [Send Slack Notification]
        ↓
   [Escalate if Needed]
```

## 📝 Configuration Details

### Classification Categories

The system can classify inquiries into categories such as:
- **Billing**: Payment, invoices, subscriptions
- **Technical**: Bugs, errors, integration issues
- **Feature Request**: New functionality suggestions
- **General Inquiry**: Information requests
- **Urgent**: Critical issues requiring immediate attention

### Google Sheets Structure

| Column | Description |
|--------|-------------|
| Timestamp | When inquiry was received |
| Customer Name | Name of the customer |
| Inquiry | Original customer message |
| Category | AI-classified category |
| Priority | Urgency level (Low/Medium/High/Critical) |
| Department | Assigned department |
| Status | Current status (New/In Progress/Resolved) |
| Response | Support team response |

### Slack Notifications

Notifications include:
- ✉️ New inquiry alert with classification
- 👤 Customer name and contact info
- 📋 Inquiry summary
- 🏷️ Category and priority level
- 🔗 Link to Google Sheet record

## 🔧 Customization

### Modify Classification Categories

Edit the Gemini AI prompt in the workflow to change classification logic:

```
Analyze the following customer inquiry and classify it into one of these categories:
[Your categories here]

Inquiry: {inquiry_text}
```

### Change Slack Channels

Update the Slack notification node to route different priority levels to different channels:
- Critical → #urgent-support
- High → #support
- Medium/Low → #general-support

### Add Additional Notifications

Extend the workflow to notify:
- Email via SMTP
- SMS via Twilio
- PagerDuty for escalations
- Custom APIs

## 📈 Monitoring & Analytics

Track key metrics:
- **Average Response Time**: Time from inquiry to first response
- **Classification Accuracy**: Manual review vs. AI classification
- **Resolution Rate**: Percentage of resolved inquiries
- **Department Distribution**: Volume by department
- **Priority Distribution**: High-priority inquiry trends

## ⚠️ Troubleshooting

### Gemini AI Not Classifying Correctly
- Review and refine the classification prompt
- Ensure API quota limits aren't exceeded
- Test with sample inquiries

### Google Sheets Not Updating
- Verify service account has write permissions
- Check sheet name and range references
- Ensure sheet is properly shared with service account

### Slack Notifications Not Sending
- Confirm Bot Token is valid
- Check channel names and permissions
- Verify bot is added to required channels

## 🔐 Security Best Practices

- ✅ Store API keys in n8n credentials, never in code
- ✅ Use service accounts with minimal required permissions
- ✅ Regularly rotate API keys and tokens
- ✅ Enable audit logging in n8n
- ✅ Use Google Sheets row-level permissions as needed
- ✅ Keep n8n and dependencies updated

## 📚 Additional Resources

- [n8n Documentation](https://docs.n8n.io/)
- [Google Gemini AI API Docs](https://ai.google.dev/)
- [Google Sheets API Guide](https://developers.google.com/sheets/api)
- [Slack API Documentation](https://api.slack.com/docs)

## 🤝 Contributing

Contributions are welcome! To contribute:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/improvement`)
3. Commit your changes (`git commit -m 'Add improvement'`)
4. Push to the branch (`git push origin feature/improvement`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 💬 Support

For issues, questions, or suggestions:
- Open an [GitHub Issue](../../issues)
- Check existing discussions
- Review the troubleshooting section above

## 🎓 Use Cases

This automation is perfect for:
- SaaS companies with high inquiry volume
- E-commerce support teams
- Service providers managing multiple service types
- Enterprises needing scalable support automation
- Teams looking to reduce manual classification work

---

**Built with ❤️ using n8n, Gemini AI, and Google Workspace**
