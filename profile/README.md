<div align="center">

<img src="./assets/voicelk-cover.png" alt="VoiceLK by RootCode-AI — Giving Sinhala a voice in the classroom. Sinhala and English text-to-speech." width="1200" />

# RootCode-AI

**Giving Sinhala a voice in the classroom.**

We are a student research team building **VoiceLK** — a Sinhala/English code-switched text-to-speech system and the learning platform around it, made for Sri Lanka's G.C.E. O/L ICT students.

[![Try VoiceLK](https://img.shields.io/badge/Try_VoiceLK-chat.voicelk.dev-111111?style=for-the-badge)](https://chat.voicelk.dev)
[![Visit our blog](https://img.shields.io/badge/Visit_our_blog-voicelk.dev-8E75B2?style=for-the-badge)](https://voicelk.dev)

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

## 🎧 Hear VoiceLK

These clips were rendered by **Speaker 02 V2.1**, our next single-speaker release, straight from the sentences below. Nothing was edited afterwards. Select a waveform to open its clip.

| Listen | Sentence | What it shows |
| --- | --- | --- |
| [<img src="./assets/samples/01-ram.png" alt="Waveform of the RAM sample" width="260" />](https://github.com/RootCode-AI/.github/blob/main/profile/assets/samples/01-ram.wav) | RAM එක කියන්නේ computer එකේ තාවකාලික මතකයයි. | An English acronym and an English word inside a Sinhala sentence |
| [<img src="./assets/samples/02-cpu.png" alt="Waveform of the CPU sample" width="260" />](https://github.com/RootCode-AI/.github/blob/main/profile/assets/samples/02-cpu.wav) | CPU එක පරිගණකයේ මොළය ලෙස හඳුන්වනවා. | Acronyms spelt out letter by letter, the way a teacher says them |
| [<img src="./assets/samples/03-html.png" alt="Waveform of the HTML sample" width="260" />](https://github.com/RootCode-AI/.github/blob/main/profile/assets/samples/03-html.wav) | HTML භාවිතා කරලා අපිට web page එකක් හදන්න පුළුවන්. | Switching language several times in one sentence |
| [<img src="./assets/samples/04-units.png" alt="Waveform of the units sample" width="260" />](https://github.com/RootCode-AI/.github/blob/main/profile/assets/samples/04-units.wav) | 1 GB එකක MB 1024ක් තියෙනවා. | Digits and units expanded into spoken words |
| [<img src="./assets/samples/05-email.png" alt="Waveform of the e-mail sample" width="260" />](https://github.com/RootCode-AI/.github/blob/main/profile/assets/samples/05-email.wav) | ඔබේ e-mail ගිණුම ශක්තිමත් password එකකින් ආරක්ෂා කරගන්න. | Hyphenated terms and everyday ICT vocabulary |

<sub>22.05 kHz mono WAV, about 3 seconds each. Speaker 02 V2.1 is not live in the app yet; the voices you can use today are listed in the app's voice picker.</sub>

---

## 📦 Repositories

| Repository | What it is | Stack |
| --- | --- | --- |
| [**voicelk_ml**](https://github.com/RootCode-AI/voicelk_ml) | Research code — Sinhala/English text normalisation, code-switched G2P with an ICT lexicon, dataset preparation, VITS training, synthesis and evaluation | Python · PyTorch · Coqui TTS (vendored) |
| [**voicelk_bridge**](https://github.com/RootCode-AI/voicelk_bridge) | TTS microservice — serves the trained models over HTTP; self-contained and deployable with Docker or systemd | Python · FastAPI · PyTorch |
| [**voicelk_be**](https://github.com/RootCode-AI/voicelk_be) | Application backend — authentication, questions and answers, Gemini orchestration, voice catalogue, audio storage and records, speech endpoints | Java 25 · Spring Boot 4.1 · Supabase |
| [**voicelk_fe**](https://github.com/RootCode-AI/voicelk_fe) | Web client — chat-style topic input, voice picker, audio playback, history, profile, guest mode and help centre; live at [chat.voicelk.dev](https://chat.voicelk.dev) | React 19 · Vite · Tailwind CSS |
| [**voicelk_blog**](https://github.com/RootCode-AI/voicelk_blog) | Source of our project blog at [voicelk.dev](https://voicelk.dev) | — |

Every part of VoiceLK is open source, from the research pipeline to the speech service, the application and the blog, so the whole system can be read and examined end to end. The research code, the speech service, the backend and the web client are released under the MIT License; the Coqui TTS and trainer sources vendored into the research code and the speech service keep their own licenses, listed in those repositories' third-party notices.

## 🔬 Research highlights

- **One text front-end.** Normalisation and pronunciation are written once in the research repository and used for dataset preparation, training, evaluation and serving. The bridge carries a synced, fingerprinted copy, so a stale front-end shows up in its health check instead of quietly mispronouncing words.
- **Code-switching first.** Numbers, symbols, acronyms and English ICT vocabulary are expanded and pronounced the way a Sri Lankan teacher would say them, mid-sentence.
- **Versioned voices.** A multi-speaker model trained on the Pathnirwana corpus (Speaker 03) and our own single-speaker model, Speaker 02, whose releases are served side by side — V1.0, the new V2.0, and V2.1 coming soon. Each is selectable per request with speaker and speaking-rate controls, and older voices are retired openly rather than swapped out silently.
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

## 🤝 Contributing

Issues and pull requests are welcome on every repository. Each one carries its own code of conduct and security policy — read them first, and report security problems privately as they describe rather than in a public issue.

Open your issue where the problem lives:

| If… | Open it on |
| --- | --- |
| VoiceLK says a word wrongly | [**voicelk_ml**](https://github.com/RootCode-AI/voicelk_ml/issues) — the text front-end that decides how words are read lives there; include the sentence and what you expected to hear |
| Audio fails to generate, or a voice will not load | [**voicelk_bridge**](https://github.com/RootCode-AI/voicelk_bridge/issues) |
| Sign-in, answers or saved audio misbehave | [**voicelk_be**](https://github.com/RootCode-AI/voicelk_be/issues) |
| Something looks or works wrong in the app | [**voicelk_fe**](https://github.com/RootCode-AI/voicelk_fe/issues) |
| A blog post has a mistake | [**voicelk_blog**](https://github.com/RootCode-AI/voicelk_blog/issues) |

The bridge carries a generated copy of the text front-end, so pronunciation fixes always go to **voicelk_ml** first and reach the speech service from there.

## 📬 Get in touch

- App: [chat.voicelk.dev](https://chat.voicelk.dev) — try VoiceLK in your browser
- Blog: [voicelk.dev](https://voicelk.dev) — follow our research notes and project updates
- Email: [rootcode2026@gmail.com](mailto:rootcode2026@gmail.com)

<!-- TODO: add X/Twitter, LinkedIn, etc. once available -->

---

<sub>VoiceLK is an academic research project. This is our GitHub organization profile — it's shown on [github.com/RootCode-AI](https://github.com/RootCode-AI).</sub>
