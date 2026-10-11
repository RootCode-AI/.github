<div align="center">

# RootCode-AI

**Giving Sinhala a voice in the classroom.**

We are a student research team building **VoiceLK** — a Sinhala/English code-switched text-to-speech system and the learning platform around it, made for Sri Lanka's G.C.E. O/L ICT students.

</div>

---

## 🎯 The problem

ICT lessons in Sri Lanka are taught in Sinhala, but the subject is full of English terms — *RAM*, *CPU*, *HTML*, *e-mail*. Off-the-shelf speech engines either cannot speak Sinhala or stumble the moment a sentence switches language. VoiceLK is built to read that mixed classroom language naturally, so students can listen to explanations instead of only reading them.

## 💡 How VoiceLK works

A student types or pastes an ICT topic. The backend asks Google Gemini for a Sinhala explanation, then sends the text to our speech service, which normalises it, converts it to phonemes with a code-switched pronunciation engine, and renders the audio with our own trained VITS model. The clip is stored and played back right in the chat.

> **Browser** → **Spring Boot backend** → **TTS Bridge** → **VITS model**
> The backend also talks to Supabase (database and audio storage), Gemini and Firebase; the bridge carries the text front-end — normaliser and grapheme-to-phoneme engine.

The speech service only turns text into audio and holds no secrets, so it can move to a GPU machine without touching the rest of the system. Every generated clip records the exact checkpoint that produced it, so any audio can be traced back to its weights.

---

## 📦 Repositories

| Repository | What it is | Stack |
| --- | --- | --- |
| [**voicelk_fe**](https://github.com/RootCode-AI/voicelk_fe) | Web client — chat-style topic input, audio playback, history, profile, guest mode and help centre | React 19 · Vite · Tailwind CSS |
| [**voicelk_be**](https://github.com/RootCode-AI/voicelk_be) | Application backend — authentication, questions and answers, Gemini orchestration, audio storage and records, speech endpoints | Java 25 · Spring Boot · Supabase |
| [**bridge**](https://github.com/Tharinda-Pamindu/bridge) | TTS microservice — serves the trained model over HTTP; self-contained and deployable with Docker or systemd | Python · FastAPI · PyTorch |
| [**voicelk_ml**](https://github.com/RootCode-AI/voicelk_ml) | Research code — Sinhala/English text normalisation, code-switched G2P with an ICT lexicon, dataset preparation, VITS training, synthesis and evaluation | Python · PyTorch · Coqui TTS (vendored) |

## 🔬 Research highlights

- **One text front-end.** Normalisation and pronunciation are written once in the research repository and used for dataset preparation, training, evaluation and serving. The bridge carries a synced, fingerprinted copy, so a stale front-end shows up in its health check instead of quietly mispronouncing words.
- **Code-switching first.** Numbers, symbols, acronyms and English ICT vocabulary are expanded and pronounced the way a Sri Lankan teacher would say them, mid-sentence.
- **Two voices.** A multi-speaker model trained on the Pathnirwana corpus and a custom single-speaker model, selectable per request with speaker and speaking-rate controls.
- **Presentable by design.** Core libraries such as Coqui TTS and its trainer are vendored as real source, so every part of the pipeline can be read and examined.

---

## 🛠️ Tech we use

![React](https://img.shields.io/badge/React-19-61DAFB?style=for-the-badge&logo=react&logoColor=white)
![Vite](https://img.shields.io/badge/Vite-646CFF?style=for-the-badge&logo=vite&logoColor=white)
![TailwindCSS](https://img.shields.io/badge/TailwindCSS-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white)
![Java](https://img.shields.io/badge/Java-25-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-6DB33F?style=for-the-badge&logo=springboot&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Supabase](https://img.shields.io/badge/Supabase-3FCF8E?style=for-the-badge&logo=supabase&logoColor=white)
![Firebase](https://img.shields.io/badge/Firebase-FFCA28?style=for-the-badge&logo=firebase&logoColor=black)
![Google Gemini](https://img.shields.io/badge/Google_Gemini-8E75B2?style=for-the-badge&logo=googlegemini&logoColor=white)

---

## 👥 Team

<table>
  <tr>
  <td align="center">
      <a href="https://github.com/Tharinda-Pamindu">
        <img src="https://github.com/Tharinda-Pamindu.png" width="100" alt="Tharinda Pamindu"/><br />
        <b>Tharinda Pamindu</b>
      </a><br />
      <sub>Owner</sub><br />
      <sub><a href="https://github.com/Tharinda-Pamindu">@Tharinda-Pamindu</a></sub>
    </td>
    <td align="center">
      <a href="https://github.com/Dilakshi13">
        <img src="https://github.com/Dilakshi13.png" width="100" alt="Dilakshi Sakila"/><br />
        <b>Dilakshi Sakila</b>
      </a><br />
      <sub>Owner</sub><br />
      <sub><a href="https://github.com/Dilakshi13">@Dilakshi13</a></sub>
    </td>
    <td align="center">
      <a href="https://github.com/Mihiran-Thilakarathna">
        <img src="https://github.com/Mihiran-Thilakarathna.png" width="100" alt="T.H.Mihiran Thilakarathna"/><br />
        <b>T.H.Mihiran Thilakarathna</b>
      </a><br />
      <sub>Owner</sub><br />
      <sub><a href="https://github.com/Mihiran-Thilakarathna">@Mihiran-Thilakarathna</a></sub>
    </td>
    <td align="center">
      <a href="https://github.com/Piyumanjalee">
        <img src="https://github.com/Piyumanjalee.png" width="100" alt="Piyumanjalee Kavindi"/><br />
        <b>Piyumanjalee Kavindi</b>
      </a><br />
      <sub>Member</sub><br />
      <sub><a href="https://github.com/Piyumanjalee">@Piyumanjalee</a></sub>
    </td>
    <td align="center">
      <a href="https://github.com/Thinuka2835">
        <img src="https://github.com/Thinuka2835.png" width="100" alt="Thinuka Ransidu"/><br />
        <b>Thinuka Ransidu</b>
      </a><br />
      <sub>Owner</sub><br />
      <sub><a href="https://github.com/Thinuka2835">@Thinuka2835</a></sub>
    </td>
  </tr>
</table>

---

## 🤝 Contributing

Each repository has its own contributing guide, code of conduct and security policy. Pronunciation problems are especially welcome — if VoiceLK says a word wrongly, open an issue on the speech service with the sentence and what you expected to hear. All repositories are released under the MIT License.

## 📬 Get in touch

- Email: [rootcode2026@gmail.com](mailto:rootcode2026@gmail.com)

<!-- TODO: add website, X/Twitter, LinkedIn, etc. once available -->

---

<sub>VoiceLK is an academic research project. This is our GitHub organization profile — it's shown on [github.com/RootCode-AI](https://github.com/RootCode-AI).</sub>
