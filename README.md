# 🔐 Cryptographic Converter

> A node-graph playground for hashing — wire a string into a hash node and watch the digest fall out.

<p align="left">
  <a href="https://cryptographic-converter.vercel.app"><img src="https://img.shields.io/badge/Live%20demo-000?style=for-the-badge&logo=vercel&logoColor=white" alt="Live demo" /></a>
  <img src="https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB" alt="React" />
  <img src="https://img.shields.io/badge/React%20Flow-FF0072?style=for-the-badge&logo=react&logoColor=white" alt="React Flow" />
  <img src="https://img.shields.io/badge/Vite-646CFF?style=for-the-badge&logo=vite&logoColor=white" alt="Vite" />
</p>

**[▶ Try it live](https://cryptographic-converter.vercel.app)**

## Why

Hashing is usually a black box: text goes in, a hex string comes out. This turns it into something
you can *see* — a visual pipeline where each stage is a node you can inspect, so the input, the
algorithm and the digest are all on screen at once and change together as you type.

## Nodes

| Node | What it does |
|---|---|
| **String** | The input. Type any text; everything downstream recomputes live. |
| **Hash** | Pick the algorithm — **SHA-1**, **SHA-256**, **SHA-384** or **SHA-512**. |
| **Result** | The digest, rendered as a `0x`-prefixed hex string. |

Drag to rearrange, pan and zoom the canvas, and connect nodes by their handles.

## How it works

Digests are computed entirely in the browser with the native
[**Web Crypto API**](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/digest)
(`crypto.subtle.digest`) — no crypto library, no network round-trip, and your input never leaves
the page. The canvas is [React Flow](https://reactflow.dev); each node type is a plain React
component wired up through `nodeTypes`.

```ts
const hashBuffer = await crypto.subtle.digest(algorithm, encoder.encode(message));
const hex = "0x" + Array.from(new Uint8Array(hashBuffer))
  .map((b) => b.toString(16).padStart(2, "0"))
  .join("");
```

## Run it locally

```bash
git clone https://github.com/prakashshuklahub/cryptographic-converter.git
cd cryptographic-converter
npm install
npm run dev
```

Then open the URL Vite prints (usually `http://localhost:5173`).

| Script | Does |
|---|---|
| `npm run dev` | Start the dev server with HMR |
| `npm run build` | Production build to `dist/` |
| `npm run preview` | Serve the production build locally |
| `npm run lint` | ESLint |

## Note on scope

This is a learning and demo project, not a security tool. `crypto.subtle` is the right primitive,
but SHA-1 is included for illustration only — **do not use it for anything that needs to be
collision-resistant.** For password hashing, use a purpose-built KDF such as Argon2 or bcrypt.

---

Built by **[Prakash Shukla](https://github.com/prakashshuklahub)** ·
[The Hustling Engineer](https://www.youtube.com/@TheHustlingEngineer)
