### 👉 _“What will you do so that your React Native app should not be hacked?”_

---

# 🔐 Deep Dive into App Security (React Native Focus)

---

## 1️⃣ **Secure Data Storage**

**Problem:** If a hacker gets access to a phone (lost/stolen) or if malware runs, they can open your app’s files. If you saved passwords/tokens in **AsyncStorage** (like a normal DB), they can just read it.

**Solution:**

- Use **Secure Storage**:

  - **Android** → Keystore (protected by hardware security module).
  - **iOS** → Keychain (protected by Face ID/Touch ID or device passcode).

- Libraries: `react-native-keychain` or `expo-secure-store`.
- Sensitive info like tokens/passwords must **never be stored in plain text**.

👉 Example: instead of:

```js
AsyncStorage.setItem("token", "abc123");
```

you’d use secure storage. That way, even if the hacker roots the phone, it’s much harder to read.

---

## 2️⃣ **Secure Communication**

**Problem:** Hackers can sniff network traffic (using tools like Wireshark or fake Wi-Fi). If your app sends sensitive data without proper encryption, they can read or modify it.

**Solution:**

- Always use **HTTPS (TLS 1.2/1.3)**.
- **SSL Pinning** → app will only trust your real server’s certificate. If a hacker tries a fake certificate (MITM attack), the app will reject it.
- Never put **API keys** inside your app code (they can be extracted). Put them in your **backend**.

👉 Example:
If your API key is in the app:

```js
const API_KEY = "sk_test_123";
```

A hacker can decompile your app and find it. Instead → move to backend and return only what client needs.

---

## 3️⃣ **Authentication & Authorization**

**Problem:** If authentication is weak (like storing sessions forever, or only checking on frontend), hackers can impersonate users.

**Solution:**

- Use **short-lived access tokens (JWT)**.
- Add **refresh tokens** that are securely stored.
- Always check **permissions on the backend** (don’t trust frontend).
- Logout should also invalidate the token on the server.

👉 Example:
If a hacker steals a token, but your token expires every 15 mins → damage is limited.

---

## 4️⃣ **Protect the App Code**

**Problem:** React Native bundles are just JavaScript. Anyone can decompile and read them → see your logic, API URLs, maybe even keys.

**Solution:**

- **Obfuscate/Minify** your JS bundle (harder to reverse-engineer).
- Use **ProGuard/R8** for Android native code.
- Detect **rooted/jailbroken devices** → stop app from running (since those devices are easier to hack).

👉 Example:
Without obfuscation → hacker can see function names like `verifyPayment()`.
With obfuscation → it looks like `a1(), b2()` → much harder to guess.

---

## 5️⃣ **UI / Device Security**

**Problem:** Screens with sensitive info (bank balance, OTP) can be screenshot or screen-recorded.

**Solution:**

- Block screenshots → Android: `FLAG_SECURE`.
- Use **biometric auth** for payments/login (`react-native-biometrics`).
- Auto logout after inactivity.

👉 Example: If your banking app doesn’t block screenshots, someone with access could take a picture of your OTP screen.

---

## 6️⃣ **Backend & API Security**

**Problem:** Even if app is secure, APIs can be attacked directly by hackers (without using your app).

**Solution:**

- Validate all inputs on server (don’t trust client).
- Use **rate limiting** (block brute force login attempts).
- Allow only **authorized roles** (staff vs admin vs user).
- Monitor unusual requests (like someone trying 1000 logins).

👉 Example:
If your app allows `/getUser?id=123`, a hacker might try `/getUser?id=124` to see someone else’s data. Backend must block that.

---

## 7️⃣ **Monitoring & Updates**

**Problem:** New vulnerabilities are discovered every month. If you don’t patch, hackers will exploit.

**Solution:**

- Use **Sentry** / **Firebase Crashlytics** to detect unusual errors.
- Watch for **suspicious API requests**.
- Regularly update React Native, libraries, and server dependencies.

👉 Example:
If a library you use has a security bug and you don’t update, hackers can exploit it (even if your app logic is safe).

---

# 🎯 Final Interview-Friendly Summary

If asked in interview:
👉 “To prevent hacking, I’d secure storage (Keychain/Keystore), enforce HTTPS with SSL pinning, never hardcode secrets, use JWT with short lifetimes, obfuscate code, detect rooted devices, block screenshots, and enforce all validation & authorization on backend. On top, I’d monitor with crash/error reporting and push frequent security updates.”

---

---

## Javascript question what is the output

**Your Code**

```jsx
const handleClick = () => {
  for (let i = 0; i <= 3; i++) {
    setCount((count) => count + i);
  }
};
```

---

## **Step-by-Step Explanation**

1. **Loop Values**

```js
(i = 0), 1, 2, 3;
```

- So the loop runs **4 times**.

2. **Inside the Loop**

```js
setCount((count) => count + i);
```

- Here you are using **functional update**, which is correct.
- **Important**: `i` changes each iteration (`0 → 1 → 2 → 3`).

---

### **How React Executes State Updates**

React **batches state updates** during event handlers.

- When using the **functional form** `setCount(prev => prev + something)`, React ensures **each update uses the latest state**.
- So each iteration **adds `i` to the latest count**.

---

### **Iteration Breakdown**

Assume initial `count = 0`:

| Loop | `i` | Calculation | Resulting count |
| ---- | --- | ----------- | --------------- |
| 1    | 0   | 0 + 0       | 0               |
| 2    | 1   | 0 + 1       | 1               |
| 3    | 2   | 1 + 2       | 3               |
| 4    | 3   | 3 + 3       | 6               |

✅ Final `count` after **one click** → **6**

---

### **Why Functional Update is Important**

If you had written:

```js
setCount(count + i);
```

- It would **always use the original `count`** for all iterations, so the updates would not accumulate correctly.
- Result with normal `count` → only `count + 3` (last iteration) → final count = **3**, which is **wrong**.

---

### **Button Behavior**

```jsx
<Button onPress={handleClick} />
```

- Each time you click the button, **the loop runs again**, adding `0+1+2+3 = 6` to `count`.
- So sequence of presses:

| Press # | Count after click |
| ------- | ----------------- |
| 1       | 6                 |
| 2       | 12                |
| 3       | 18                |

---

### **Key Interview Points**

1. The code uses **functional state updates** → correct way to handle state inside a loop.
2. The loop adds **0+1+2+3 = 6** each time → predictable increment.
3. If you used `setCount(count + i)` → would **not work as expected** because React batches state updates.
4. `for` loop + `setCount` in functional form → classic React interview trick.

---
