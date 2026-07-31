# Burp Suite Cheat Sheet

#burp-suite #cheatsheet #web-security #pentesting

## Common Workflow

```
Configure Browser
        ↓
Browse Application
        ↓
Proxy → HTTP History
        ↓
Target → Site Map
        ↓
Repeater
        ↓
Intruder
        ↓
Validate Findings
```

---

# Core Modules

| Module | Purpose |
|---------|---------|
| Target | Map the application |
| Proxy | Intercept HTTP(S) traffic |
| HTTP History | View all captured requests |
| Repeater | Modify and replay requests |
| Intruder | Automate repetitive requests |
| Decoder | Encode and decode data |
| Comparer | Compare requests or responses |
| Logger | Log and filter traffic |
| Extender | Install extensions |

---

# Common Right Click Actions

| Action | Purpose |
|---------|---------|
| Send to Repeater | Manual testing |
| Send to Intruder | Automated attacks |
| Send to Decoder | Decode or encode values |
| Send to Comparer | Compare requests/responses |
| Send to Organizer | Bookmark important requests |

---

# Proxy Intercept

| Button | Function |
|---------|----------|
| Forward | Send request |
| Drop | Discard request |
| Intercept On | Pause requests |
| Intercept Off | Forward automatically |

---

# HTTP Methods

| Method | Typical Use |
|---------|-------------|
| GET | Retrieve data |
| POST | Submit data |
| PUT | Replace resource |
| PATCH | Update resource |
| DELETE | Remove resource |
| OPTIONS | Supported methods |
| HEAD | Headers only |

---

# Common HTTP Status Codes

| Code | Meaning |
|------:|---------|
| 200 | OK |
| 201 | Created |
| 204 | No Content |
| 301 | Moved Permanently |
| 302 | Redirect |
| 400 | Bad Request |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 405 | Method Not Allowed |
| 429 | Too Many Requests |
| 500 | Internal Server Error |
| 502 | Bad Gateway |
| 503 | Service Unavailable |

---

# Testing Checklist

□ Define Scope

□ Browse entire application

□ Inspect HTTP History

□ Analyze Cookies

□ Analyze Headers

□ Check Parameters

□ Test Authentication

□ Test Authorization

□ Test Input Validation

□ Test File Uploads

□ Test APIs

□ Document Findings

---

# Frequently Tested Parameters

```
id=
user=
username=
email=
role=
token=
page=
file=
redirect=
callback=
search=
query=
sort=
lang=
```

---

# Useful Encodings

| Encoding | Example |
|-----------|---------|
| URL | `%20` |
| Base64 | `SGVsbG8=` |
| Hex | `48656c6c6f` |
| HTML | `&lt;script&gt;` |
| JSON | `{"id":1}` |

---

# Common Extensions

| Extension | Purpose |
|-----------|----------|
| Logger++ | Advanced logging |
| JWT Editor | JWT manipulation |
| Hackvertor | Data conversion |
| Autorize | Authorization testing |
| Param Miner | Hidden parameter discovery |
| Turbo Intruder | High-speed requests |

---

# Burp Browser Setup

```
Proxy Listener

Host: 127.0.0.1
Port: 8080
```

Firefox + FoxyProxy

```
Type : HTTP
Host : 127.0.0.1
Port : 8080
```

Remember to import Burp's CA certificate when intercepting HTTPS traffic.

---

# Typical Repeater Workflow

```
Capture Request

↓

Send to Repeater

↓

Modify Request

↓

Send

↓

Analyze Response

↓

Repeat
```

---

# Notes

- Work inside Scope whenever possible.
- Manual testing should come before automation.
- Save interesting requests early.
- Keep Repeater tabs organized.
- Use trusted extensions from the official BApp Store.