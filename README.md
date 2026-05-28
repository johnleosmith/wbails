# Modified Whatsapp-API
<p align='center'>
  <img src="https://i.ibb.co/ynCtrgcY/attack.jpg" width="172">
</p>

--- 

## Usage
```json
"depencies": {
  "@whiskeysockets/baileys": "github:johnleosmith/wbails"
}
```
## Import
```javascript
const {
  default:makeWASocket,
  // Other Options 
} = require('@whiskeysockets/baileys');
```

---
# How To Connect To Whatsapp
## With QR Code
```javascript
const {
  default: makeWASocket
} = require('@whiskeysockets/baileys');

const client = makeWASocket({
  browser: ['Ubuntu', 'Chrome', '20.00.1'],
  printQRInTerminal: true
})
```

## Connect With Number
```javascript
const {
  default: makeWASocket,
  fetchLatestWAWebVersion
} = require('@whiskeysockets/baileys');

const client = makeWASocket({
  browser: ['Ubuntu', 'Chrome', '20.00.1'],
  printQRInTerminal: false,
  version: fetchLatestWAWebVersion()
  // Other options
});

const number = "234XXXXX";
const code = await client.requestPairingCode(number.trim) /* Use : (number, "YYYYYYYY") for custom-pairing */

console.log("Your pairing code : " + code)
```

# Sending messages

## send orderMessage
```javascript
const fs = require('fs');
const LeoImg = fs.readFileSync('./LeoImage');

await client.sendMessage(m.chat, {
  thumbnail: LeoImg,
  message: "What's Life",
  orderTitle: "XinvasionX",
  totalAmount1000: 99999,
  totalCurrencyCode: "NGN"
}, { quoted:m })
```

## send pollResultSnapshotMessage
```javascript
await client.sendMessage(m.chat, {
  pollResultMessage: {
    name: "XinvasionX",
    options: [
      {
        optionName: "poll 1"
      },
      {
        optionName: "poll 2"
      }
    ],
    newsletter: {
      newsletterName: "TheLonerDev | XinvasionX",
      newsletterJid: "1@newsletter"
    }
  }
})
```

## send productMessage
```javascript
await client.relayMessage(m.chat, {
  productMessage {
    title: "Leo.pdf",
    description: "zZZ...",
    thumbnail: { url: "./LeoImage" },
    productId: "EXAMPLE_TOKEN",
    retailerId: "EXAMPLE_RETAILER_ID",
    url: "https://t.me/TheLonerD3v",
    body: "X",
    footer: "Footer",
    buttons: [
      {
        name: "cta_url",
        buttonParamsJson: "{\"display_text\":\"XinvasionX\",\"url\":\"https://t.me/TheLonerD3v\"}"
      }
    ],
    priceAmount1000: 99999,
    currencyCode: "NGN"
  }
})
```

## send member label
```javascript
await client.sendMessage(m.chat, {
  groupLabel: {
    labelText: "XinvasionX"
  }
})
```

## send message to members in group
```javascript
await client.sendMessageMembers(m.chat, {
  extendedTextMessage: {
    text: "X"
  }
}, {})
```
# Simple sendMessage

## send text
```javascript
await client.sendText(m.chat, "XinvasionX", {
  contextInfo: {
    mentionedJid: [m.chat]
  }
}, {
  key: {
    remoteJid: "status@broadcast",
    participant: m.sender,
    fromMe: true
  },
  message: {
    conversation: "\0"
  }
})
```
## send image
```javascript
await client.sendImage(m.chat, { url: "./Leo.jpg" }, "TheLonerDev", {
  contextInfo: {
    mentionedJid: [m.chat]
  }
}, {
  key: {
    remoteJid: "status@broadcast",
    participant: m.sender,
    fromMe: true
  },
  message: {
    conversation: "\0"
  }
})
```

## send video
```javascript
await client.sendVideo(m.chat, { url: "./Leo.mp4" }, "XinvasionX", {
  contextInfo: {
    mentionedJid: [m.chat]
  }
}, {
  key: {
    remoteJid: "status@broadcast",
    participant: m.sender,
    fromMe: true
  },
  message: {
    conversation: "\0"
  }
})
```

## send audio
```javascript
await client.sendAudio(m.chat, { url: "./Leo.mp3" }, {
  contextInfo: {
    mentionedJid: [m.chat]
  }
}, {
  key: {
    remoteJid: "status@broadcast",
    participant: m.sender,
    fromMe: true
  },
  message: {
    conversation: "\0"
  }
})
```

## send location
```javascript
await client.sendLocation(m.chat, "XinvasionX", 90.0, 90.0, "https://t.me/XinvasionX", "1234567890", {
  contextInfo: {
    mentionedJid: [m.chat]
  }
}, {
  key: {
    remoteJid: "status@broadcast",
    participant: m.sender,
    fromMe: true
  },
  message: {
    conversation: "\0"
  }
})
```

## send polling
```javascript
await client.sendPoll(m.chat, "TheLonerDev", ["1", "2", "3"], true, {
  contextInfo: {
    mentionedJid: [m.chat]
  }
}, {
  key: {
    remoteJid: "status@broadcast",
    participant: m.sender,
    fromMe: true
  },
  message: {
    conversation: "\0"
  }
})
```

## send quiz
```javascript
await client.sendQuiz(m.chat, "TheLonerDev", ["1", "2", "3"], "2", {
  contextInfo: {
    mentionedJid: [m.chat]
  }
}, {
  key: {
    remoteJid: "status@broadcast",
    participant: m.sender,
    fromMe: true
  },
  message: {
    conversation: "\0"
  }
})
```

## send status mention
```javascript
await client.statusMention(m.chat, {
  extendedTextMessage: {
    text: "TheLonerDev"
  }
})
```
Follow https://t.me/XinvasionX for more information.
