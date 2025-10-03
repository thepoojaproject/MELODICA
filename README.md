
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Enhanced Music Card</title>
  <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500;700&display=swap" rel="stylesheet">
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
    
    body {
      font-family: 'Roboto', sans-serif;
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 20px;
    }
    
    .card {
      width: 220px;
      height: 320px;
      background: lightgrey;
      border-radius: 16px;
      position: relative;
      font-family: Roboto, sans-serif;
      box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
      overflow: hidden;
    }

    .card .one {
      width: 220px;
      height: 320px;
      z-index: 10;
      position: absolute;
      background: rgba(255, 255, 255, 0.55);
      box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.37);
      backdrop-filter: blur(8.5px);
      -webkit-backdrop-filter: blur(8.5px);
      border-radius: 16px;
      border: 1px solid rgba(255, 255, 255, 0.18);
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: space-between;
      padding: 15px 0;
    }

    .title {
      width: 80px;
      border: 1px solid rgba(180, 177, 177, 0.308);
      text-align: center;
      font-size: 11px;
      border-radius: 12px;
      color: rgba(102, 100, 100, 0.911);
      padding: 4px 0;
      font-weight: 500;
      letter-spacing: 0.5px;
    }

    .music {
      width: 100px;
      height: 100px;
      background: rgba(216, 212, 212, 0.726);
      border-radius: 15px;
      display: flex;
      align-items: center;
      justify-content: center;
      overflow: hidden;
      position: relative;
      cursor: pointer;
      transition: all 0.3s ease;
      box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
    }
    
    .music:hover {
      transform: scale(1.05);
      background: rgba(230, 227, 227, 0.8);
    }

    .music-icon {
      font-size: 40px;
      color: rgba(102, 100, 100, 0.7);
    }
    
    .file-label {
      position: absolute;
      width: 100%;
      height: 100%;
      display: flex;
      align-items: center;
      justify-content: center;
      cursor: pointer;
    }

    .music input[type="file"] {
      position: absolute;
      width: 100%;
      height: 100%;
      opacity: 0;
      cursor: pointer;
    }
    
    .file-name {
      font-size: 10px;
      margin-top: 5px;
      color: rgba(50, 49, 51, 0.7);
      max-width: 150px;
      overflow: hidden;
      text-overflow: ellipsis;
      white-space: nowrap;
      text-align: center;
    }

    .name {
      width: 180px;
      font-size: 14px;
      font-weight: 500;
      text-align: center;
      color: rgba(50, 49, 51, 0.8);
      margin-top: 5px;
    }

    .name1 {
      width: 140px;
      font-size: 10px;
      text-align: center;
      color: rgba(50, 49, 51, 0.6);
      margin-bottom: 10px;
    }

    audio {
      width: 180px;
      margin-top: 8px;
      outline: none;
    }
    
    audio::-webkit-media-controls-panel {
      background-color: rgba(255, 255, 255, 0.7);
    }

    .footer {
      width: 100%;
      text-align: center;
      font-size: 10px;
      color: rgba(50,50,50,0.6);
      padding: 8px 0;
      border-top: 1px solid rgba(255,255,255,0.3);
      background: linear-gradient(180deg, rgba(255,255,255,0.0), rgba(255,255,255,0.05));
    }
    
    .footer .heart {
      color: #ff4b6e;
      margin: 0 3px;
    }

    /* Floating balls animation */
    .card .two {
      width: 70px;
      height: 70px;
      background-color: rgb(131, 25, 163);
      filter: drop-shadow(0 0 10px rgb(131, 25, 163));
      border-radius: 50%;
      position: absolute;
      top: 30px;
      left: 20px;
      animation: one 5s infinite;
    }

    .card .three {
      width: 70px;
      height: 70px;
      background-color: rgb(29, 209, 149);
      filter: drop-shadow(0 0 10px rgb(29, 209, 149));
      border-radius: 50%;
      position: absolute;
      top: 90px;
      left: 90px;
      animation: two 5s infinite;
    }
    
    .card .four {
      width: 50px;
      height: 50px;
      background-color: rgb(255, 165, 0);
      filter: drop-shadow(0 0 10px rgb(255, 165, 0));
      border-radius: 50%;
      position: absolute;
      top: 180px;
      left: 40px;
      animation: three 5s infinite;
    }

    @keyframes one {
      0% { top: 30px; left: 20px; }
      20% { top: 50px; left: 40px; }
      40% { top: 80px; left: 70px; }
      50% { top: 60px; left: 40px; }
      60% { top: 35px; left: 90px; }
      80% { top: 70px; left: 70px; }
      100% { top: 30px; left: 20px; }
    }

    @keyframes two {
      0% { top: 90px; left: 90px; }
      20% { top: 50px; left: 40px; }
      40% { top: 60px; left: 20px; }
      50% { top: 80px; left: 30px; }
      60% { top: 35px; left: 90px; }
      80% { top: 70px; left: 60px; }
      100% { top: 90px; left: 90px; }
    }
    
    @keyframes three {
      0% { top: 180px; left: 40px; }
      20% { top: 150px; left: 80px; }
      40% { top: 120px; left: 50px; }
      60% { top: 160px; left: 100px; }
      80% { top: 140px; left: 30px; }
      100% { top: 180px; left: 40px; }
    }
    
    /* Loading animation */
    .loading {
      display: none;
      width: 30px;
      height: 30px;
      border: 3px solid rgba(255, 255, 255, 0.3);
      border-radius: 50%;
      border-top-color: #764ba2;
      animation: spin 1s ease-in-out infinite;
      margin: 10px auto;
    }
    
    @keyframes spin {
      to { transform: rotate(360deg); }
    }
    
    /* Error message */
    .error {
      color: #ff4b6e;
      font-size: 10px;
      text-align: center;
      margin-top: 5px;
      display: none;
    }
  </style>
</head>
<body>
  <div class="card">
    <div class="one">
      <div class="title">Music</div>

      <div class="music">
        <div class="music-icon">🎧</div>
        <label for="fileInput" class="file-label">
          <input type="file" accept="audio/*" id="fileInput">
        </label>
      </div>
      
      <div class="file-name" id="fileName">No file selected</div>

      <div class="name">Your Song</div>
      <div class="name1">Select from Disk</div>
      
      <div class="loading" id="loading"></div>
      <div class="error" id="error"></div>

      <audio id="audioPlayer" controls></audio>

      <div class="footer">
        Made with <span class="heart">💖</span> By Armeen
      </div>
    </div>
    <div class="two"></div>
    <div class="three"></div>
    <div class="four"></div>
  </div>

  <script>
    const fileInput = document.getElementById("fileInput");
    const audioPlayer = document.getElementById("audioPlayer");
    const fileName = document.getElementById("fileName");
    const loading = document.getElementById("loading");
    const error = document.getElementById("error");

    fileInput.addEventListener("change", function() {
      const file = this.files[0];
      
      // Reset states
      error.style.display = "none";
      loading.style.display = "block";
      
      if (file) {
        // Validate file type
        if (!file.type.startsWith('audio/')) {
          error.textContent = "Please select an audio file";
          error.style.display = "block";
          loading.style.display = "none";
          return;
        }
        
        // Update file name display
        fileName.textContent = file.name.length > 20 
          ? file.name.substring(0, 17) + "..." 
          : file.name;
        
        // Create object URL and play
        const url = URL.createObjectURL(file);
        audioPlayer.src = url;
        
        // Hide loading when audio is ready
        audioPlayer.oncanplaythrough = function() {
          loading.style.display = "none";
          audioPlayer.play();
        };
        
        // Handle errors
        audioPlayer.onerror = function() {
          loading.style.display = "none";
          error.textContent = "Error loading audio file";
          error.style.display = "block";
        };
      } else {
        loading.style.display = "none";
        fileName.textContent = "No file selected";
      }
    });
  </script>
</body>
</html>
