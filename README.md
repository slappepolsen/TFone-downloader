# TFone-downloader

## 📖 Table of Contents
- [⚠️ Important notes before you start](https://github.com/slappepolsen/TFone-downloader/edit/main/README.md#%EF%B8%8F-important-notes-before-you-start)
- [🔄 How the scripts work](https://github.com/slappepolsen/TFone-downloader/edit/main/README.md#-how-the-scripts-work)
- [🏆 Choosing the right script](https://github.com/slappepolsen/TFone-downloader/edit/main/README.md#-how-the-scripts-work)
- [🛠 Installation & requirements](https://github.com/slappepolsen/TFone-downloader/edit/main/README.md#-installation--requirements)
- [🎯 How to run the scripts](https://github.com/slappepolsen/TFone-downloader/edit/main/README.md#-why-use-these-scripts)
- [❗ Common issues & troubleshooting](https://github.com/slappepolsen/TFone-downloader/edit/main/README.md#-common-issues--troubleshooting)
- [📬 Disclaimer](https://github.com/slappepolsen/TFone-downloader/edit/main/README.md#-disclaimer)


# 📥 TFone episode downloader & decrypter

This project simplifies the process of downloading, decrypting, and converting TFone videos. While it automates many steps, you **still need to manually collect** a few key details from the website before running the script.

---

## ⚠️ Important notes before you start

No matter which script you use, you **must manually collect** these four things for each episode:

1. **Episode number** (for naming the files)
2. **MPD URL** (changes frequently)
3. **PSSH Key** (can change daily)
4. **Widevine License URL** (can also change daily)

These values can be found using **Developer Tools** (`CTRL+SHIFT+I` in Firefox, Chrome, Opera etc.). For a step-by-step guide on how to collect them, refer to the `User Guide.md` file.

### 🔴 **Important warning about MPD, PSSH, and Widevine**
- These values **expire quickly**, sometimes within **24 hours**.
- **If you're using batch processing (`dna.py`), do not pre-fill the Excel file days in advance.**
- **Only enter data and run the script on the same day** to avoid errors.

---

## 🔄 How the scripts work

There are **three different scripts**, depending on how you prefer to input your data and how many episodes you want to process at once.

### **1️⃣ `batch.py` (batch processing, requires input from excel file)**
✅ Best for **multiple episodes** (e.g., 5+, 10+).  
✅ **Automated**: Reads the MPD, PSSH, and Widevine License URL **from an Excel file**.   
✅ **Hands-off**: Just start it and let it run while you do other things.  
✅ Ideal for bulk extraction.

💡 **Use this if you want to process a large number of episodes without manually entering each one.**

---

### **2️⃣ `single.py` (manual input mode)**
✅ Best for **one episode at a time**.  
✅ **No Excel needed**: You just enter the MPD, PSSH, and Widevine License URL manually.  
✅ Good if you just want to **quickly extract a single episode** without setting up a spreadsheet.  
✅ More interactive but requires manual input for each episode.

💡 **Use this if you only need to extract one or two episodes and don't mind manually entering the details.**

---

### **3️⃣ `mpd_to_srt.py` (subtitle extractor)**
✅ Focuses **only** on downloading and converting subtitles.  
✅ Works similarly to `batch.py` but processes subtitle files instead of video/audio.

💡 **Use this if you just need subtitles.**

---

## 🏆 Choosing the right script
- **Want full automation & batch processing?** → Use `batch.py` (Excel method).  
- **Want more manual control & do one episode at a time?** → Use `single.py`.  
- **Just need subtitles?** → Use `mpd_to_srt.py`.

---

## 🚀 Why use these scripts?

Downloading and decrypting videos normally requires **several manual steps**, such as:
- Finding the MPD URL, PSSH key, and Widevine License.
- Running separate commands for downloading, decrypting, merging, and converting subtitles.

**These scripts simplify the process by only asking you for four things** per episode:
- Episode Number
- MPD URL
- PSSH Key
- Widevine License URL

Once you provide this information, the script handles the rest automatically.

---

## 🔧 Installation & requirements
Before using the scripts, make sure you have the following installed on your **Windows** system (sorry, I don't have guidance (yet) for Mac/Linux):

1. **`yt-dlp`** → For downloading video and audio.
2. **`mp4decrypt`** → For decrypting encrypted video and audio.
3. **`ffmpeg`** → For processing video and subtitles.
4. **`Python`** → For running the script.

📌 See the `Installation Guide.md` for detailed installation steps.

---

## 🎯 How to run the scripts

### **Option 1: Batch processing (`batch.py`)**
1. Fill in the `input.xlsx` file with fresh episode details. Ensure the Excel file has the following columns exactly as shown:

| episode | mpd             | pssh      | widevine         |
|---------|----------------|-----------|------------------|
| 664     | https://vod...  | AAAAMHB   | https://wide...  |

Important Rules for the Excel File:

- The column names must be exactly: episode, mpd, pssh, widevine.
- No extra columns should be added, or the script might fail.
- The file must be an .xlsx Excel file (not CSV or other formats). Name the file `input.xlsx` or change the code in Notepad or other Code Editor to match the file path.
- MPD, PSSH, and Widevine values change daily → Always use fresh data and run the script on the same day.

1. Fill in the `input.xlsx` file with fresh episode details.
2. Run the script:
   ```sh
   python batch.py
   ```
3. The script will read from the Excel file and process all episodes.

---

### **Option 2: manual input (`single.py`)**
1. Run the script:
   ```sh
   python single.py
   ```
2. The script will ask for:
   - Episode Number
   - MPD URL
   - PSSH Key
   - Widevine License URL
3. Enter the details, and the script will process the episode.

---

### **Option 3: Subtitles Only (`mpd_to_srt.py`)**
1. Run the script:
   ```sh
   python mpd_to_srt.py
   ```
2. The script will extract subtitles and convert them to `.srt` format.

---

## ❗ Common issues & troubleshooting
❌ **"Decryption failed" error?**  
- Check that your PSSH and Widevine URL are correct.
- Make sure the values were collected on the same day.

❌ **"File not found" error?**  
- Ensure yt-dlp, mp4decrypt, and ffmpeg are installed correctly.
- Run the installation test:
  ```sh
  yt-dlp --version
  mp4decrypt --version
  ffmpeg -version
  python --version
  ```

❌ **Batch processing script is not working?**  
- Make sure the **MPD, PSSH, and Widevine values are fresh** and not outdated.

---

## 📢 Disclaimer
- These scripts are for **personal use only**.  
- Downloading DRM-protected content **may violate the terms of service** of the streaming platform.  
- **Use responsibly** and at your own risk.  

---

🚀 **Now you're ready to use the TFone video downloader!** Happy extracting! 🎬

