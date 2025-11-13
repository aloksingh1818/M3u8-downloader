# M3u8-downloader


You are building a backend Flask-based Python application called m3u8-downloader.

The purpose of this app is to allow users to download and convert .m3u8 video streams (including blob-based videos) into a single .mp4 file on the server (localhost or GitHub Codespace).

Please create a complete working version with the following requirements:


---

💡 Functional Requirements

1. The app runs locally (localhost:5000) or in a GitHub Codespace environment.


2. It exposes a single API endpoint:

GET /download?url=<m3u8_link>

url is the public .m3u8 link of the video.

The endpoint should start downloading all .ts video segments from the playlist.



3. After all segments are downloaded:

Merge them sequentially into one file (e.g., merged.ts).

Use ffmpeg to convert the .ts file into an .mp4 file.

Save the final file as output.mp4 in the project root directory.



4. Return a JSON response after completion:

{
  "message": "Download complete",
  "saved_as": "output.mp4"
}


5. Use ThreadPoolExecutor to download multiple segments in parallel (10 threads max).


6. Handle exceptions gracefully and return error messages in JSON format.


7. Show progress logs in the terminal (like “Downloaded 25/150 segments (16%)”).




---

⚙️ Technical Requirements

Use Python 3.9+

Use Flask for the web framework

Use requests and m3u8 Python libraries

Use ffmpeg (system-installed) for video merging

Directory structure:

/m3u8-downloader
├── app.py
├── requirements.txt
├── temp_ts/   ← store temporary .ts chunks
├── merged.ts
└── output.mp4

Include a requirements.txt file containing:

flask
requests
m3u8

Before running the app, automatically check if ffmpeg is installed; if not, print a clear message:
“⚠️ ffmpeg not found. Please install it using: sudo apt-get install ffmpeg”.



---

🚀 Example Usage

After running the app with:

python app.py

Open this URL in the browser or API client:

http://127.0.0.1:5000/download?url=https://cdn.example.com/video/hls_2M_.m3u8

The terminal should log something like:

Found 120 segments.
[#####----------------] 25% Downloaded (30/120)
[#############--------] 75% Downloaded (90/120)
✅ All segments downloaded. Merging...
✅ Conversion complete. File saved as output.mp4

Return JSON:

{"message": "✅ Download complete", "saved_as": "output.mp4"}


---

🧰 Bonus (optional for Copilot)

If possible, add:

A /status endpoint that shows current download progress.

Auto-cleanup of temp_ts folder after merging.

Automatic renaming of downloaded files with timestamp, e.g., video_2025-11-13_14-22-10.mp4.



---

🧠 Key Focus for Copilot

1. Write production-level, well-commented Python code.


2. Ensure thread-safe downloading and progress calculation.


3. Ensure that video segments are correctly merged in order.


4. Keep code modular with helper functions like:

download_segment(url, folder)

merge_segments(segment_urls, folder, output_file)

convert_to_mp4(input_file, output_file)





---

✅ Deliverables

Complete working Flask app (app.py)

requirements.txt

Step-by-step comments in code for understanding

Instructions to run (Flask + ffmpeg installation note)
