<div align="center">

<pre>
████████╗██╗   ██╗██████╗ ███████╗███████╗██████╗ ██╗██████╗ ███████╗
╚══██╔══╝██║   ██║██╔══██╗██╔════╝██╔════╝██╔══██╗██║██╔══██╗██╔════╝
   ██║   ██║   ██║██████╔╝█████╗   ███████╗██████╔╝██║██████╔╝█████╗  
   ██║   ██║   ██║██╔══██╗██╔══╝   ╚════██║██╔═══╝ ██║██╔══██╗██╔══╝  
   ██║   ╚██████╔╝██████╔╝███████╗███████║██║     ██║██║  ██║███████╗
   ╚═╝    ╚═════╝ ╚═════╝ ╚══════╝╚══════╝╚═╝     ╚═╝╚═╝  ╚═╝╚══════╝
</pre>

# TubeSpire

### A High-Performance Engine for Seamless YouTube Media Archiving.

<p>
  <a href="https://github.com/KartikeyaPandey313/TubeSpire/stargazers"><img alt="GitHub stars" src="https://img.shields.io/github/stars/KartikeyaPandey313/TubeSpire?style=for-the-badge&logo=github&color=0d1117&logoColor=white&labelColor=black"></a>
  <img alt="Status" src="https://img.shields.io/badge/status-production_ready-brightgreen?style=for-the-badge&logo=serverless&logoColor=white&labelColor=black">
  <img alt="Python" src="https://img.shields.io/badge/python-3.8+-3776AB?style=for-the-badge&logo=python&logoColor=white&labelColor=black">
  <a href="#-license"><img alt="License" src="https://img.shields.io/badge/License-Proprietary-B80F0A?style=for-the-badge&labelColor=black"></a>
</p>
</div>

**TubeSpire** is not just another downloader—it's a robust, self-hosted engine engineered for elite media archiving. Forged with a focus on raw performance, absolute privacy, and a hardcore minimalist UX, it provides a clean, powerful gateway to YouTube's media library, free from ads and trackers. This is a professional-grade tool for creators, researchers, and archivists who demand control and reliability.

### 📚 Table of Contents

1. [🔥 The TubeSpire Ethos](#-the-tubespire-ethos)
2. [📸 Preview & Demo](#-preview--demo)
3. [💎 Elite Features](#-elite-features)
4. [🧠 Architecture Deep Dive](#-architecture-deep-dive)
5. [🛠️ Forged With](#️-forged-with)
6. [🧬 Modes of Operation](#-modes-of-operation)
7. [🚀 Deployment & Operations](#-deployment--operations)
8. [❓ The Debriefing (FAQ)](#-the-debriefing-faq)
9. [🏆 The Architects](#-the-architects)
10. [📜 License](#-license)

---

> _A tool forged in the fires of digital sovereignty._

## 🔥 The TubeSpire Ethos

This project is built on an uncompromising foundation.

- **🚀 UNCOMPROMISING SPEED:** Engineered for pure velocity. A lightweight Flask backend and efficient processing pipeline mean your downloads are handled with minimal overhead. No waiting. No excuses.<br><br>
- **✨ RADICAL SIMPLICITY:** Power doesn't require complexity. The UI is brutally efficient and intuitive, designed to serve your needs and then get out of the way.<br><br>
- **🛡️ ABSOLUTE PRIVACY:** Your operations are your own. TubeSpire's core application operates on a zero-log policy for user downloads. No user accounts, no download history. Period.<br><br>

<p align="right"><a href="#-table-of-contents">↑ back to top</a></p>

## 📸 Preview & Demo

A glimpse into the clean, focused, and powerful user interface of TubeSpire, followed by a live demonstration of the operational workflow.

<p align="center">
  <img src="extras/preview_ui.png" alt="TubeSpire UI Preview">
</p>

<div align="center">
  <video width="80%" controls>
    <source src="extras/demo.mp4" type="video/mp4">
    Your browser does not support the video tag. 
  </video>
</div>

<p align="right"><a href="#-table-of-contents">↑ back to top</a></p>

## 💎 Elite Features

| Feature                         | The Arsenal                                                                                                             |
| :------------------------------ | :---------------------------------------------------------------------------------------------------------------------- |
| 💿 **4K & High-Fidelity Video** | Archive video in resolutions up to pristine 4K UHD. Your media, preserved in its highest form.                          |
| 🎵 **High-Bitrate Audio**       | Rip and convert audio streams directly to high-bitrate MP3. Perfect for music, podcasts, and critical audio analysis.   |
| ⚡ **Efficient Backend**        | Built on a high-throughput Flask architecture that handles requests with ruthless efficiency for a zero-lag experience. |
| 🕶️ **Aggressive Dark UI/UX**    | A sleek, fully responsive interface with a native dark mode that's easy on the eyes and hard on distractions.           |
| 🔒 **Zero-Log Privacy**         | With zero user tracking and no request logging in its core, TubeSpire is your secure, private media archiving vault.    |

<p align="right"><a href="#-table-of-contents">↑ back to top</a></p>

## 🧠 Architecture Deep Dive

TubeSpire is engineered with a clean, decoupled architecture for maximum performance and maintainability.

1.  **Frontend (Client-Side):**

    - The user interacts with a clean, responsive UI built with semantic **HTML5** and styled with modern **CSS3**.
    - All pages inherit from a central `base.html` template, which includes SEO optimizations, security headers, and analytics hooks.
    - Interactive elements like the download animation are powered by lightweight, vanilla **JavaScript**.

2.  **Backend (Server-Side):**

    - The **Flask** application (`app.py`) serves as the central nervous system. It's a lightweight WSGI framework that handles all incoming requests.
    - When a user submits a URL, the `/` route calls the `fetch_video_info` helper function.
    - This function interfaces directly with the **`yt-dlp`** library to retrieve all metadata about the video without downloading it.
    - The data is then passed to the `process_video_formats` helper, which sanitizes and organizes the available streams into a user-friendly list.
    - The `index.html` template is re-rendered with the video information, displaying the download options.

3.  **The Download Process:**
    - When the user clicks a download button, the form submits a POST request to the `/download` endpoint.
    - The backend builds a precise set of options for `yt-dlp` using the `build_download_options` helper.
    - For high-resolution video, it commands `yt-dlp` to download the best video-only stream and the best audio-only stream.
    - **FFmpeg** is then automatically invoked by `yt-dlp` to merge ("mux") these two streams into a single, high-quality MP4 file. For audio, FFmpeg converts the best audio stream to a high-bitrate MP3.
    - The final file is saved to the temporary `downloads/` folder, and Flask's `send_from_directory` serves it to the user, triggering a browser download.

<p align="right"><a href="#-table-of-contents">↑ back to top</a></p>

> _The tools we wield define the art we create._

## 🛠️ Forged With

TubeSpire is built with a stack of battle-tested, high-performance technologies.

<p align="center">
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white&labelColor=0d1117" alt="Python"/>
  <img src="https://img.shields.io/badge/Flask-FFFFFF?style=for-the-badge&logo=flask&logoColor=black&labelColor=0d1117" alt="Flask"/>
  <img src="https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black&labelColor=0d1117" alt="JavaScript"/>
  <img src="https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white&labelColor=0d1117" alt="HTML5"/>
  <img src="https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white&labelColor=0d1117" alt="CSS3"/>
  <br>
  <img src="https://img.shields.io/badge/yt--dlp-8A2BE2?style=for-the-badge&labelColor=0d1117" alt="yt-dlp"/>
  <img src="https://img.shields.io/badge/FFmpeg-007800?style=for-the-badge&logo=ffmpeg&logoColor=white&labelColor=0d1117" alt="FFmpeg"/>
  <img src="https://img.shields.io/badge/Gunicorn-499848?style=for-the-badge&logo=gunicorn&logoColor=white&labelColor=0d1117" alt="Gunicorn"/>
  <img src="https://img.shields.io/badge/GitHub_Actions-2088FF?style=for-the-badge&logo=github-actions&logoColor=white&labelColor=0d1117" alt="GitHub Actions"/>
</p>

<p align="right"><a href="#-table-of-contents">↑ back to top</a></p>

## 🧬 Modes of Operation

TubeSpire is engineered for flexibility, adapting to your specific operational needs.

- **🌐 `Web Mode` (Default):**
  The full-featured, graphical web interface. Optimized for accessibility and a premium user experience with a responsive, dark-themed UI and interactive elements. Ideal for general use.

- **🎛️ `Lite Mode` (Future Vision):**
  A planned command-line interface (CLI) for pure, blazing-fast performance. Designed for power users, scripting, and batch operations. Minimal overhead, maximum throughput.

- **🧪 `Experimental Mode` (Future Vision):**
  An upcoming branch for developers and early adopters. This mode will house beta features, edge-case handling, and next-generation archival tools before they are merged into the main production build.

<p align="right"><a href="#-table-of-contents">↑ back to top</a></p>

## 🚀 Deployment & Operations

Get your own instance of TubeSpire operational in minutes.
(Detailed instructions for local setup can be found in the `ADMIN_GUIDE.md`)

> To access `ADMIN_GUIDE.md` contact admin.

<p align="right"><a href="#-table-of-contents">↑ back to top</a></p>

## ❓ The Debriefing (FAQ)

<details>
<summary><strong>Is this legal?</strong></summary>
<br>
Let's be clear: We provide a powerful tool. You are responsible for wielding it ethically. This software is intended for legitimate archival of public content (e.g., your own creations, public domain media, research materials). Do not use it for piracy or copyright infringement. Respect the creators and the law.
</details><br>

<details>
<summary><strong>Why do I need FFmpeg?</strong></summary>
<br>
Because quality demands it. For anything above 1080p, YouTube delivers video and audio as separate streams. FFmpeg is the industry-standard surgical tool required to merge—or "mux"—these streams into a single, flawless, high-resolution file. No FFmpeg, no elite quality.
</details><br>

<details>
<summary><strong>What makes this better than online downloader sites?</strong></summary>
<br>
Those sites are cesspools of ads, trackers, and malware, and they often throttle your speeds. TubeSpire is your own private, self-hosted instance. It's faster, infinitely safer, and respects your privacy. You control the hardware and the code. It's the difference between a rusty public payphone and a military-grade encrypted satellite phone. If you've any privacy issue you can visit us <a href="mailto:pandeykartikeya313@gmail.com">pandeykartikeya313@gmail.com</a>
</details><br>

<details>
<summary><strong>Can I download private or age-restricted content?</strong></summary>
<br>
No. Full stop. This is a deliberate ethical and technical constraint. TubeSpire is engineered to access public content only and will not bypass authentication or restrictions. We respect people's privacy and not violate any law. 
</details><br>

<p align="right"><a href="#-table-of-contents">↑ back to top</a></p>

---

<div align="center">
<h3>🤝 Want to help evolve TubeSpire?</h3>
<p>
  This project is built for elite operators. If you have the skills to enhance the arsenal, we welcome your contributions.
  <br />
  Consult the <strong><a href="CONTRIBUTING.md">Contributing Guide</a></strong> for mission parameters.
</p>

> We do not believe in age, we believe in skill, wheather you're under 16 or 50+, we welcome you!

## </div>

## 🏆 The Architects

This project was conceived and built by dedicated creators.

### The Master Architect

<table width="100%">
  <tr>
    <td width="150" align="center">
      <a href="https://github.com/KartikeyaPandey313">
        <img src="extras/profile_picture.png" width="120" alt="Kartikeya Pandey" style="border-radius:50%; border: 2px solid #30363D;"/>
      </a>
    </td>
    <td>
      <strong>Kartikeya Pandey</strong>
      <br/><br/>
      The visionary architect and lead developer of TubeSpire. He forged this application from the ground up, driven by a passion for clean code, hardcore performance, and an uncompromising user experience.
      <br/><br/>
      <a href="mailto:pandeykartikeya313@gmail.com"><img src="https://img.shields.io/badge/Email-D14836?style=for-the-badge&logo=gmail&logoColor=white&labelColor=0d1117"></a>
      <a href="https://github.com/KartikeyaPandey313"><img src="https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white&labelColor=0d1117"></a>
    </td>
  </tr>
</table>

### The Vanguard (Contributors)

Our eternal gratitude to the legends who have contributed code, ideas, and bug reports. Join their ranks.

<p align="center">
  <a href="https://github.com/KartikeyaPandey313/tubespire/graphs/contributors">
    <img src="https://contrib.rocks/image?repo=KartikeyaPandey313/tubespire" />
  </a>
</p>

<p align="right"><a href="#-table-of-contents">↑ back to top</a></p>

## 📜 License

This project is governed by a **Proprietary License**. Access is granted by the architect.

<details>
<summary><strong>Access & Use Mandate // EULA</strong></summary>
<br>

> #### **Copyright (c) 2025 Kartikeya Pandey**
>
> **PREAMBLE:** This End-User License Agreement ("EULA") constitutes a legally binding agreement between you and the Author for the TubeSpire software product ("Software").
>
> **ARTICLE I: GRANT OF LICENSE**
>
> - Permission is hereby granted, **strictly upon obtaining prior written authorization from the copyright holder**, to any individual or entity to use, copy, and modify the Software.
> - Distribution, sublicensing, or selling copies of the Software is **expressly forbidden** without explicit written consent.
>
> **ARTICLE II: ATTRIBUTION**
>
> - Attribution to **Kartikeya Pandey** is mandatory and must be conspicuously displayed in all public distributions, user interfaces, documentation, and any derivative works.
>
> **ARTICLE III: PROHIBITIONS**
>
> - Unauthorized use, redistribution, reverse-engineering, or modification of this Software is a direct violation of this EULA and is **strictly prohibited**. Such actions may result in immediate termination of rights and potential legal action.
>
> **ARTICLE IV: DISCLAIMER OF WARRANTY**
>
> - THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR ANY CLAIM, DAMAGES, OR OTHER LIABILITY.
>
> **For all permissions and inquiries, contact the Author directly:** [pandeykartikeya313@gmail.com](mailto:pandeykartikeya313@gmail.com)

</details>

<p align="right"><a href="#-table-of-contents">↑ back to top</a></p>

<div align="center">
  <em>“The best way to predict the future is to build it.”</em>
  <br>
  <strong>&copy; 2025 TubeSpire</strong>
</div>
