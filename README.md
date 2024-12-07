To ensure the best quality is selected **before downloading** using `yt-dlp` and `ffmpeg`, you can use the following approach:

---

### Steps to Select Best Quality Before Downloading

1. **Fetch Available Formats**:  
   Use `yt-dlp` to list all available formats for the video.  

   ```bash
   yt-dlp -F <video_url>
   ```

   This command lists the available video formats with details like resolution, codecs, and bitrate.

2. **Filter Best Quality**:  
   Use the format code for the highest resolution and best quality. For example, to select the highest quality MP4 format:  

   ```bash
   yt-dlp -f bestvideo[ext=mp4]+bestaudio[ext=m4a] <video_url>
   ```

   This ensures you download the best video and audio streams, which can be merged.

3. **Merge Video and Audio (if required)**:  
   If the video and audio are separate streams, `yt-dlp` automatically uses `ffmpeg` to merge them into a single file.  

   Ensure `ffmpeg` is installed and available in your PATH for this to work seamlessly.  

4. **Fallback to Custom Quality**:  
   If a user specifies a lower resolution (e.g., 720p or 144p), pass the specific format code for that quality:  

   ```bash
   yt-dlp -f <format_code> <video_url>
   ```

   Example: To download 720p MP4:  

   ```bash
   yt-dlp -f 'bestvideo[height<=720][ext=mp4]+bestaudio[ext=m4a]' <video_url>
   ```

5. **Conversion to MP4 (if required)**:  
   If the downloaded format is not MP4, use `ffmpeg` to convert it:  

   ```bash
   ffmpeg -i input_file -c:v copy -c:a copy output.mp4
   ```

6. **Automate Selection in Backend**:  
   In your Go backend, automate this process:  
   - Use `yt-dlp` to fetch formats.  
   - Parse the format list to find the best match.  
   - Execute the appropriate `yt-dlp` and `ffmpeg` commands to download and convert.  

Would you like an example of the Go backend code to handle this?
