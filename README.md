<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Speech Recognition for Hearing Impaired</title>
    <style>
        body { 
            margin: 0;
            padding: 0;
            height: 100vh;
            background: url('https://www.sennheiser.com/cdn-cgi/image/width=1920,format=avif,quality=75/globalassets/digizuite/45735-en-hd_490_pro_product_shot_in_use_axis_audio_69.jpg/SennheiserFullWidth') 
                        no-repeat center center/cover;
            font-family: Arial, sans-serif;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            color: white;
            text-align: center;
        }

        h1 {
            font-size: 36px;
        }

        label {
            font-size: 20px;
            font-weight: bold;
            display: block;
            margin-bottom: 10px;
        }

        #language-select {
            padding: 10px;
            font-size: 16px;
            background-color: #f0f0f0;
            border-radius: 10px;
            border: none;
        }

        /* Upload Box Styling */
        .upload-box {
            width: 350px;
            padding: 20px;
            background: rgba(0, 0, 0, 0.6);
            border-radius: 12px;
            text-align: center;
            cursor: pointer;
            border: 2px dashed #fff;
            transition: background 0.3s, border 0.3s;
            display: none; /* Hidden by default */
        }

        .upload-box:hover {
            background: rgba(255, 255, 255, 0.2);
            border-color: #ffcc00;
        }

        .upload-box p {
            margin: 0;
            font-size: 18px;
            font-weight: bold;
        }

        #video-upload {
            display: none;
        }

        #file-name {
            margin-top: 10px;
            font-size: 16px;
            color: #ddd;
        }

        /* Radio Button Container */
        .options {
            margin: 20px 0;
        }

        .options label {
            font-size: 18px;
            cursor: pointer;
        }

        .options input {
            margin-right: 8px;
        }

        /* Next Button */
        #next-btn {
            margin-top: 20px;
            background-color: #555; /* Gray when disabled */
            color: white;
            padding: 12px 25px;
            font-size: 18px;
            border: none;
            border-radius: 8px;
            cursor: not-allowed;
            text-decoration: none;
            opacity: 0.5;
            transition: background 0.3s, opacity 0.3s, cursor 0.3s;
        }

        /* Activated Next Button */
        #next-btn.enabled {
            background-color: #007bff;
            cursor: pointer;
            opacity: 1;
        }

        #next-btn.enabled:hover {
            background-color: #0056b3;
        }
    </style>
</head>
<body>

    <h1>Speech Recognition System for Hearing Impaired</h1>
    
    <label>
        <input type="radio" name="mode" value="speech-to-text"> Select language for Speech-to-Text
    </label>
    <select id="language-select">
        <option value="en-US">English (US)</option>
        <option value="ta-IN">Tamil (India)</option>
        <option value="hi-IN">Hindi (India)</option>
        <option value="es-ES">Spanish (Spain)</option>
        <option value="fr-FR">French (France)</option>
        <option value="de-DE">German (Germany)</option>
        <option value="it-IT">Italian (Italy)</option>
        <option value="pt-BR">Portuguese (Brazil)</option>
        <option value="zh-CN">Chinese (Mandarin)</option>
        <option value="ja-JP">Japanese (Japan)</option>
        <option value="ar-SA">Arabic (Saudi Arabia)</option>
    </select>
    
    <!-- Options to choose -->
    <div class="options">
        
        <label>
            <input type="radio" name="mode" value="video-captioning"> Upload Video for Captions
        </label>
    </div>

    <!-- Upload Box (Hidden Initially) -->
    <div id="upload-section" class="upload-box" onclick="document.getElementById('video-upload').click();">
        <p>Click to Upload Video</p>
        <div id="file-name">No file chosen</div>
    </div>
    <input type="file" id="video-upload" accept="video/*">

    <!-- Next Button -->
    <a id="next-btn" href="Untitled-1.html">Next</a>

    <script>
        const videoInput = document.getElementById("video-upload");
        const fileNameDisplay = document.getElementById("file-name");
        const nextBtn = document.getElementById("next-btn");
        const uploadSection = document.getElementById("upload-section");
        const modeOptions = document.querySelectorAll('input[name="mode"]');

        let selectedMode = null;
        let videoUploaded = false;

        // Check which mode is selected
        modeOptions.forEach(option => {
            option.addEventListener("change", function () {
                selectedMode = this.value;

                if (selectedMode === "video-captioning") {
                    uploadSection.style.display = "block";  // Show upload box
                    videoUploaded = false;  // Reset file selection
                    nextBtn.classList.remove("enabled");
                    nextBtn.href = "#";
                } else {
                    uploadSection.style.display = "none";  // Hide upload box
                    enableNextButton("speech-to-text.html");  // Set to speech-to-text page
                }
            });
        });

        // Handle file upload
        videoInput.addEventListener("change", function (event) {
            if (event.target.files.length > 0) {
                const file = event.target.files[0];
                fileNameDisplay.textContent = file.name;
                localStorage.setItem("uploadedVideo", URL.createObjectURL(file));
                videoUploaded = true;
                enableNextButton("captions.html");  // Set to video captioning page
            } else {
                fileNameDisplay.textContent = "No file chosen";
                videoUploaded = false;
                nextBtn.classList.remove("enabled");
                nextBtn.href = "#";
            }
        });

        // Enable Next Button
        function enableNextButton(targetPage) {
            if (selectedMode === "speech-to-text" || (selectedMode === "video-captioning" && videoUploaded)) {
                nextBtn.classList.add("enabled");
                nextBtn.href = targetPage;
            } else {
                nextBtn.classList.remove("enabled");
                nextBtn.href = "#";
            }
        }
    </script> 
   

</body>
</html>