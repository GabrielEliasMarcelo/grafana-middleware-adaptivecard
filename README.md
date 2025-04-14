# grafana-middleware-adaptivecard

A lightweight middleware service that transforms Grafana alerts into rich Adaptive Cards and forwards them to Microsoft Teams channels. This middleware allows better customization and visualization of alerts, overcoming Grafana's limitations in formatting Teams notifications directly.

---

## 📌 Overview

Grafana has limited capabilities for customizing webhook payloads, especially when integrating with Microsoft Teams. This middleware acts as a translator, receiving raw Grafana alert payloads and reformatting them into structured Adaptive Cards suitable for Teams channels.

---

## 🚀 Features

- 🔄 Converts Grafana alert payloads into Adaptive Card format
- 📥 Receives standard webhook POSTs from Grafana
- 📤 Sends customized messages to Microsoft Teams channels via Webhook URLs
- 🧩 Supports different alert types and dynamic payload structures
- ⚙️ Customizable message templates

---

## 📐 Architecture

```
Grafana ──▶ Middleware (grafana-middleware-adaptivecard) ──▶ Microsoft Teams
           [Receives alerts]                    [Sends Adaptive Cards]
```

---

## ⚙️ Setup

### 1. Clone the Repository

```bash
git clone https://github.com/your-org/grafana-middleware-adaptivecard.git
cd grafana-middleware-adaptivecard
```

### 2. Configure

Update the configuration file or environment variables:

| Variable              | Description                                     |
|-----------------------|-------------------------------------------------|
| `TEAMS_WEBHOOK_URL`   | Microsoft Teams Incoming Webhook URL           |
| `PORT`                | Port to run the middleware (default: 8080)     |

You can use a `.env` file:

```env
TEAMS_WEBHOOK_URL=https://your-teams-webhook-url
PORT=8080
```

### 3. Run the Middleware

```bash
go run main.go
```

Or build the binary:

```bash
go build -o grafana-middleware-adaptivecard
./grafana-middleware-adaptivecard
```

---

## 📤 Configuring Grafana

1. Go to **Alerting > Contact points**
2. Add a **Webhook** contact point
3. Set the URL to your middleware endpoint, e.g.:

```
http://<middleware-host>:8080/webhook
```

---

## 📊 Example

Example Grafana Alert:

```json
{
  "status": "firing",
  "alerts": [
    {
      "labels": {
        "alertname": "HighCPUUsage",
        "severity": "critical"
      },
      "annotations": {
        "summary": "CPU usage is over 90% for 5 minutes"
      }
    }
  ]
}
```

Resulting Adaptive Card in Teams:

- **Title:** 🔥 HighCPUUsage
- **Severity:** Critical
- **Summary:** CPU usage is over 90% for 5 minutes

---

## 📎 Related

- [Grafana Alerting Documentation](https://grafana.com/docs/grafana/latest/alerting/)
- [Microsoft Teams Adaptive Cards](https://adaptivecards.io/)
- [Go Web Framework (chi/gin)] if you're using any

---

## 🛠️ Development

This project is written in Go. Contributions are welcome!

```bash
go mod tidy
go run main.go
```

---

## 📄 License

[MIT License](LICENSE)

---

## 📬 Feedback

Feel free to open issues or submit pull requests to improve functionality or templates!
