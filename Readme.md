
<!-- Glowing Header -->
<p align="center">
  <img src="https://i.imgur.com/dBaSKWF.gif" height="40" width="100%">
</p>

<h1 align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&size=25&duration=3000&color=FF0000&background=000000&center=true&vCenter=true&width=600&lines=🚀 BRIAN-TECH🔥+WhatsApp+Bot;💻+By+BRIAN KIMUTAI" alt="Typing Animation">
</h1>

<!-- Banner Image -->
<p align="href="https://brian/scanner" target="_blank"
  src="https://files.catbox.moe/bkuj17.jpg" width="85%" height="auto">
</p>

---

## 📌 **How to BRIAN-TECH**

### **Step 1: Get Session ID**
Click the button below to quickly generate your WhatsApp session ID:

const { default: makeWASocket, useMultiFileAuthState, DisconnectReason } = require("@whiskeysockets/baileys")
const P = require("pino")
const qrcode = require("qrcode-terminal") // NEW

let antiVideoSettings = {}

async function startBot() {
    const { state, saveCreds } = await useMultiFileAuthState("auth_info")

    const sock = makeWASocket({
        auth: state,
        logger: P({ level: "silent" }) // remove deprecated printQRInTerminal
    })

    sock.ev.on("creds.update", saveCreds)

    sock.ev.on("connection.update", (update) => {
        const { connection, lastDisconnect, qr } = update

        if (qr) {
            console.log("📱 Scan the QR code below with WhatsApp:")
            qrcode.generate(qr, { small: true }) // 🔥 show QR in terminal
        }

        if (connection === "close") {
            const reason = lastDisconnect?.error?.output?.statusCode

            if (reason !== DisconnectReason.loggedOut) {
                console.log("🔁 Reconnecting...")
                startBot()
            } else {
                console.log("❌ Logged out. Delete auth_info folder and restart bot.")
            }
        } else if (connection === "open") {
            console.log("✅ Bot connected successfully!")
        }
    })

    sock.ev.on("messages.upsert", async ({ messages }) => {
        const msg = messages[0]
        if (!msg.message) return

        const from = msg.key.remoteJid
        const sender = msg.key.participant || from
        const isGroup = from.endsWith("@g.us")

        const text =
            msg.message.conversation ||
            msg.message.extendedTextMessage?.text ||
            ""

        // ================= COMMAND HANDLER =================
        if (text.startsWith(".antivideo") && isGroup) {
            const args = text.split(" ")

            if (args[1] === "on") {
                const mode = args[2]

                if (["warn", "delete", "kick"].includes(mode)) {
                    antiVideoSettings[from] = mode
                    await sock.sendMessage(from, { text: `⚙️ Anti-video enabled: *${mode.toUpperCase()}*` })
                }
            }

            if (args[1] === "off") {
                delete antiVideoSettings[from]
                await sock.sendMessage(from, { text: "❌ Anti-video disabled" })
            }
        }

        // ================= VIDEO DETECTION =================
        if (isGroup && antiVideoSettings[from]) {
            if (msg.message.videoMessage) {
                const mode = antiVideoSettings[from]

                if (mode === "warn") {
                    await sock.sendMessage(from, { text: `⚠️ @${sender.split("@")[0]} sending videos is not allowed!`, mentions: [sender] })
                }

                if (mode === "delete") {
                    await sock.sendMessage(from, { delete: msg.key })
                }

                if (mode === "kick") {
                    await sock.groupParticipantsUpdate(from, [sender], "remove")
                }
            }
        }
    })
}

startBot()
### **Step 2: Configure Settings**
Before deployment, configure your bot:
- **Option A:** Edit `config.env` file
- **Option B:** Use environment variables on your hosting platform

### **Step 3: Choose Hosting Platform**
Deploy the bot on your preferred platform.

<p align="https://chat.whatsapp.com/LcuQDXzl1tAGWDCANTBmbs?mode=gi_tcenter">
  <a href="https://pro.briantech.co.ke" target="_blank">
    <img src="https://img.shields.io/badge/🚀_BWM_XMD_PRO-000000?style=for-the-badge&color=FF00F" width="200" height="45"/>
  </a>
   <a href="https://main.brian.co.ke/Deploy" target="_blank">
    <img src="https://img.shields.io/badge/🚀_HEROKU-000000?style=for-the-badge&color=FF00FF" width="200" height="45"/>
  </a>
  <a href="https://render.com" target="_blank">
    <img src="https://img.shields.io/badge/🚀_RENDER-000000?style=for-the-badge&color=61DAFB" width="200" height="45"/>
  </a>
  <a href="https://railway.app?referralCode=AqkNn4" target="_blank">
    <img src="https://img.shields.io/badge/🚀_RAILWAY-000000?style=for-the-badge&color=purple" width="200" height="45"/>
  </a>
</p>

<br>

<!-- 🎥 VIDEO TUTORIAL - GitHub README Compatible -->
<p align="center">
  <strong>🎬 Watch Full Deployment Tutorial (2026)</strong><br>
  <em>How to deploy BRIAN TECH on its own hosting - No Deployer Needed!</em>
</p>

<p align="center">
  <a href="https://chat.whatsapp.com/LcuQDXzl1tAGWDCANTBmbs?mode=gi_t
    <img src="https://chat.whatsapp.com/LcuQDXzl1tAGWDCANTBmbs?mode=gi_t
  </a>
</p>

<p align="center">
  <a href="https://youtu.be/4r5OewBgLIs?si=azJ2ByJjZu5ZjrOC" target="_blank">
    <img src="https://img.youtube.com/vi/4r5OewBgLIs/0.jpg" width="400" height="225" alt="BWM XMD Deployment Tutorial">
  </a>
  <br>
  <sub>⚠️ <strong>Click the image or button above to watch on YouTube</strong> (GitHub does not support embedded video players)</sub>
</p>

### **Step 4: Start Using**
Once configured, your bot will be ready to use!

---

## 🖼️ **Bot Screenshots**

<div align="center">
  <table>
    <tr>
      <td align="center">
        <img src="https://files.catbox.moe/i5ax9j.jpg" width="300"><br>
        <small><i>Bot Interface</i></small>
      </td>
      <td align="center">
        <img src="https://files.catbox.moe/h316gy.jpg" width="300"><br>
        <small><i>Features Panel</i></small>
      </td>
    </tr>
    <tr>
      <td align="center" colspan="2">
        <img src="https://files.catbox.moe/7xz8lv.jpg" width="320"><br>
        <small><i>Control Panel</i></small>
      </td>
    </tr>
  </table>
</div>

---

## 🔧 **Additional Resources**

<p align="center">
  <a href=
    <img src="https://img.shields.io/badge/📁_PANEL_FILES-000000?style=for-the-badge&color=FFA500" width="260" height="50"/>
  </a>
</p>

---

## 📢 **Stay Updated**

<p align="center">
  <a href=">
    <img src="
  </a>
  <br>
  <a href="https://briantech.co.ke target="_blank">
    <img src="https://img.shields.io/badge/🌐_WEBSITE-brian.co.ke-000000?style=for-the-badge" width="300" height="50"/>
  </a>
</p>

---

## 📊 **Stats**

<p align="center">
  <img src="https://komarev.com/ghpvc/?username=Briankipz &label=Profile+Views&color=FF0000&style=for-the-badge" alt="Views"/>
  <img src="https://img.shields.io/github/followers/briankipz?label=GitHub+Followers&style=for-the-badge&color=00FF00" alt="Followers"/>
</p>

---

## 🟢 **Status**

<p align="center">
  <img src="https://raw.githubusercontent.com/brianbiwott1433/Brian/main/assets/statusbar.gif" height="25">
  <br>
  <span style="font-size:1.2em; color:#00FF00;">Status: <b>🟢 ONLINE</b></span>
</p>

---

<!-- Footer -->
<p align="center">
  <img src="https://i.imgur.com/dBaSKWF.gif" height="40" width="100%">
</p>

<p align="center">
  <strong>BRIAN © 2026 | Developed by BRIAN KIPZ</strong>
</p>
