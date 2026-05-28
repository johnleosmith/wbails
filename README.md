# WSBails

<p align="center">
  <img src="https://i.ibb.co/ynCtrgcY/attack.jpg" width="172" alt="WSBails logo">
</p>

## Overview

WSBails is a modified WhatsApp API built on top of `@whiskeysockets/baileys`. It provides the same powerful socket-based WhatsApp client with additional examples for sending advanced message types.

---

## Installation

```bash
npm install github:johnleosmith/wbails
```

Or add it to `package.json`:

```json
"dependencies": {
  "@whiskeysockets/baileys": "github:johnleosmith/wbails"
}
```

---

## Quick Start

```javascript
const { default: makeWASocket } = require('@whiskeysockets/baileys');

const client = makeWASocket({
  browser: ['Ubuntu', 'Chrome', '20.00.1'],
  printQRInTerminal: true
});
```

---

## Features

- Connect via QR code or phone number pairing
- Send text, image, video, audio, location, poll, and quiz messages
- Send order, product, and newsletter/poll snapshot messages
- Manage group labels and broadcast messages to members
- Compatible with the Baileys socket client API

---

## Connect to WhatsApp

### 1. Connect with QR code

```javascript
const { default: makeWASocket } = require('@whiskeysockets/baileys');

const client = makeWASocket({
  browser: ['Ubuntu', 'Chrome', '20.00.1'],
  printQRInTerminal: true
});
```

### 2. Connect with phone number

```javascript
const {
  default: makeWASocket,
  fetchLatestWAWebVersion
} = require('@whiskeysockets/baileys');

const client = makeWASocket({
  browser: ['Ubuntu', 'Chrome', '20.00.1'],
  printQRInTerminal: false,
  version: fetchLatestWAWebVersion()
});

const number = '234XXXXX';
const code = await client.requestPairingCode(number.trim());
// Use: requestPairingCode(number, 'YYYYYYYY') for custom pairing.

console.log('Your pairing code:', code);
```

---

## Sending Messages

### Text message

```javascript
await client.sendText(m.chat, 'XinvasionX', {
  contextInfo: {
    mentionedJid: [m.chat]
  }
}, {
  key: {
    remoteJid: 'status@broadcast',
    participant: m.sender,
    fromMe: true
  },
  message: {
    conversation: '\0'
  }
});
```

### Image

```javascript
await client.sendImage(
  m.chat,
  { url: './Leo.jpg' },
  'TheLonerDev',
  {
    contextInfo: { mentionedJid: [m.chat] }
  },
  {
    key: {
      remoteJid: 'status@broadcast',
      participant: m.sender,
      fromMe: true
    },
    message: { conversation: '\0' }
  }
);
```

### Video

```javascript
await client.sendVideo(
  m.chat,
  { url: './Leo.mp4' },
  'XinvasionX',
  {
    contextInfo: { mentionedJid: [m.chat] }
  },
  {
    key: {
      remoteJid: 'status@broadcast',
      participant: m.sender,
      fromMe: true
    },
    message: { conversation: '\0' }
  }
);
```

### Audio

```javascript
await client.sendAudio(
  m.chat,
  { url: './Leo.mp3' },
  {
    contextInfo: { mentionedJid: [m.chat] }
  },
  {
    key: {
      remoteJid: 'status@broadcast',
      participant: m.sender,
      fromMe: true
    },
    message: { conversation: '\0' }
  }
);
```

### Location

```javascript
await client.sendLocation(
  m.chat,
  'XinvasionX',
  90.0,
  90.0,
  'https://t.me/XinvasionX',
  '1234567890',
  {
    contextInfo: { mentionedJid: [m.chat] }
  },
  {
    key: {
      remoteJid: 'status@broadcast',
      participant: m.sender,
      fromMe: true
    },
    message: { conversation: '\0' }
  }
);
```

### Poll

```javascript
await client.sendPoll(
  m.chat,
  'TheLonerDev',
  ['1', '2', '3'],
  true,
  {
    contextInfo: { mentionedJid: [m.chat] }
  },
  {
    key: {
      remoteJid: 'status@broadcast',
      participant: m.sender,
      fromMe: true
    },
    message: { conversation: '\0' }
  }
);
```

### Quiz

```javascript
await client.sendQuiz(
  m.chat,
  'TheLonerDev',
  ['1', '2', '3'],
  '2',
  {
    contextInfo: { mentionedJid: [m.chat] }
  },
  {
    key: {
      remoteJid: 'status@broadcast',
      participant: m.sender,
      fromMe: true
    },
    message: { conversation: '\0' }
  }
);
```

### Order message

```javascript
const fs = require('fs');
const LeoImg = fs.readFileSync('./LeoImage');

await client.sendMessage(
  m.chat,
  {
    thumbnail: LeoImg,
    message: "What's Life",
    orderTitle: 'XinvasionX',
    totalAmount1000: 99999,
    totalCurrencyCode: 'NGN'
  },
  { quoted: m }
);
```

### Poll result snapshot message

```javascript
await client.sendMessage(m.chat, {
  pollResultMessage: {
    name: 'XinvasionX',
    options: [
      { optionName: 'poll 1' },
      { optionName: 'poll 2' }
    ],
    newsletter: {
      newsletterName: 'TheLonerDev | XinvasionX',
      newsletterJid: '1@newsletter'
    }
  }
});
```

### Product message

```javascript
await client.relayMessage(m.chat, {
  productMessage: {
    title: 'Leo.pdf',
    description: 'X',
    thumbnail: { url: './LeoImage' },
    productId: 'EXAMPLE_TOKEN',
    retailerId: 'EXAMPLE_RETAILER_ID',
    url: 'https://t.me/TheLonerD3v',
    body: 'X',
    footer: 'Footer',
    buttons: [
      {
        name: 'cta_url',
        buttonParamsJson: '{"display_text":"XinvasionX","url":"https://t.me/TheLonerD3v"}'
      }
    ],
    priceAmount1000: 99999,
    currencyCode: 'NGN'
  }
});
```

### Group label

```javascript
await client.sendMessage(m.chat, {
  groupLabel: {
    labelText: 'XinvasionX'
  }
});
```

### Message to group members

```javascript
await client.sendMessageMembers(
  m.chat,
  {
    extendedTextMessage: {
      text: 'X'
    }
  },
  {}
);
```

### Status mention

```javascript
await client.statusMention(m.chat, {
  extendedTextMessage: {
    text: 'TheLonerDev'
  }
});
```

---

## API Reference

- `makeWASocket(options)` - creates a WhatsApp socket client.
- `client.sendText(chatId, text, options, messageInfo)` - sends a text message.
- `client.sendImage(chatId, image, caption, options, messageInfo)` - sends an image.
- `client.sendVideo(chatId, video, caption, options, messageInfo)` - sends a video.
- `client.sendAudio(chatId, audio, options, messageInfo)` - sends audio.
- `client.sendLocation(chatId, name, lat, long, url, phone, options, messageInfo)` - shares a location.
- `client.sendPoll(chatId, name, options, selectableBy, optionsData, messageInfo)` - sends a poll.
- `client.sendQuiz(chatId, name, choices, correctOption, optionsData, messageInfo)` - sends a quiz.
- `client.sendMessage(chatId, message, options)` - sends a raw WhatsApp message payload.
- `client.relayMessage(chatId, message)` - forwards a raw message payload.
- `client.sendMessageMembers(chatId, message, options)` - sends a message to group members.
- `client.statusMention(chatId, message)` - sends a status mention.

---

## Notes

- `makeWASocket` is the main entry point for WhatsApp socket connections.
- When using `printQRInTerminal: true`, the QR code is displayed in your terminal.
- `requestPairingCode()` can accept a second argument for custom pairing codes.
- Replace placeholder values before using these examples in production.

> Follow https://t.me/XinvasionX for more information.

## send status mention
```javascript
await client.statusMention(m.chat, {
  extendedTextMessage: {
    text: "TheLonerDev"
  }
})
```
Follow https://t.me/XinvasionX for more information.
