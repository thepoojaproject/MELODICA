<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Harmony Music Player</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: #000;
            color: #fff;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            padding: 20px;
        }
        
        .music-player {
            width: 100%;
            max-width: 400px;
            background: #111;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(255, 255, 255, 0.05);
            overflow: hidden;
            padding: 30px;
            border: 1px solid #333;
            position: relative;
        }
        
        .player-header {
            text-align: center;
            margin-bottom: 25px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 15px;
        }
        
        .logo {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            overflow: hidden;
            display: flex;
            justify-content: center;
            align-items: center;
            background: #fff;
            padding: 5px;
        }
        
        .logo img {
            width: 100%;
            height: 100%;
            object-fit: contain;
        }
        
        .player-header h1 {
            font-size: 1.8rem;
            font-weight: 300;
            letter-spacing: 1px;
        }
        
        .album-art {
            width: 240px;
            height: 240px;
            border-radius: 12px;
            margin: 0 auto 25px;
            overflow: hidden;
            box-shadow: 0 8px 20px rgba(255, 255, 255, 0.05);
            background: #222;
            display: flex;
            justify-content: center;
            align-items: center;
            color: #666;
            font-size: 14px;
            border: 1px solid #333;
        }
        
        .album-art img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            display: none;
        }
        
        .track-info {
            text-align: center;
            margin-bottom: 25px;
        }
        
        .track-title {
            font-size: 22px;
            font-weight: 500;
            margin-bottom: 5px;
            color: #fff;
        }
        
        .track-artist {
            color: #aaa;
            font-size: 16px;
        }
        
        .progress-area {
            margin-bottom: 25px;
        }
        
        .progress-bar {
            height: 4px;
            background: #333;
            border-radius: 2px;
            cursor: pointer;
            margin-bottom: 8px;
        }
        
        .progress {
            height: 100%;
            width: 0%;
            background: #fff;
            border-radius: 2px;
            transition: width 0.1s linear;
        }
        
        .time {
            display: flex;
            justify-content: space-between;
            color: #aaa;
            font-size: 13px;
        }
        
        .controls {
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 25px;
            margin-bottom: 20px;
        }
        
        .control-btn {
            background: none;
            border: none;
            color: #fff;
            cursor: pointer;
            font-size: 20px;
            width: 44px;
            height: 44px;
            border-radius: 50%;
            display: flex;
            justify-content: center;
            align-items: center;
            transition: all 0.2s ease;
        }
        
        .control-btn:hover {
            background: rgba(255, 255, 255, 0.1);
        }
        
        .play-pause {
            width: 60px;
            height: 60px;
            background: #fff;
            color: #000;
            font-size: 24px;
        }
        
        .play-pause:hover {
            transform: scale(1.05);
            background: #f0f0f0;
        }
        
        .volume-controls {
            display: flex;
            align-items: center;
            gap: 10px;
            margin-bottom: 25px;
        }
        
        .volume-bar {
            flex: 1;
            height: 4px;
            background: #333;
            border-radius: 2px;
            position: relative;
            cursor: pointer;
        }
        
        .volume-level {
            position: absolute;
            left: 0;
            top: 0;
            height: 100%;
            width: 70%;
            background: #fff;
            border-radius: 2px;
        }
        
        .playlist {
            margin-bottom: 20px;
            max-height: 200px;
            overflow-y: auto;
            border-top: 1px solid #333;
            padding-top: 20px;
        }
        
        .playlist-item {
            display: flex;
            align-items: center;
            padding: 12px 0;
            border-bottom: 1px solid #222;
            cursor: pointer;
            transition: background 0.2s ease;
        }
        
        .playlist-item:hover {
            background: rgba(255, 255, 255, 0.05);
        }
        
        .playlist-item.active {
            color: #fff;
            background: rgba(255, 255, 255, 0.1);
        }
        
        .playlist-item-info {
            flex: 1;
            overflow: hidden;
        }
        
        .playlist-item-title {
            font-size: 15px;
            margin-bottom: 2px;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }
        
        .playlist-item-artist {
            font-size: 12px;
            color: #aaa;
        }
        
        .playlist-item.active .playlist-item-artist {
            color: #ddd;
        }
        
        .playlist-item-duration {
            font-size: 13px;
            color: #666;
        }
        
        .playlist-item.active .playlist-item-duration {
            color: #ddd;
        }
        
        .empty-playlist {
            text-align: center;
            color: #666;
            font-size: 14px;
            padding: 20px 0;
        }
        
        .upload-area {
            border: 2px dashed #555;
            border-radius: 12px;
            padding: 20px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s ease;
            margin-top: 10px;
        }
        
        .upload-area:hover {
            background: rgba(255, 255, 255, 0.05);
            border-color: #fff;
        }
        
        .upload-icon {
            font-size: 32px;
            margin-bottom: 10px;
            color: #fff;
        }
        
        .upload-text {
            font-size: 16px;
            margin-bottom: 5px;
        }
        
        .upload-subtext {
            font-size: 12px;
            color: #aaa;
        }
        
        #file-input {
            display: none;
        }
        
        .hidden {
            display: none;
        }
        
        .player-footer {
            text-align: center;
            margin-top: 25px;
            padding-top: 20px;
            border-top: 1px solid #333;
            color: #666;
            font-size: 14px;
            letter-spacing: 0.5px;
        }

        /* Custom scrollbar for playlist */
        .playlist::-webkit-scrollbar {
            width: 6px;
        }

        .playlist::-webkit-scrollbar-track {
            background: #222;
            border-radius: 3px;
        }

        .playlist::-webkit-scrollbar-thumb {
            background: #444;
            border-radius: 3px;
        }

        .playlist::-webkit-scrollbar-thumb:hover {
            background: #555;
        }
    </style>
</head>
<body>
    <div class="music-player">
        <div class="player-header">
            <div class="logo">
                <img src="https://i.ibb.co/F4cP5Ccn/image.png" alt="Harmony Logo">
            </div>
            <h1>HARMONY</h1>
        </div>
        
        <div class="album-art" id="album-art">
            <img id="album-image" src="" alt="Album Art">
            <div id="default-art">No track selected</div>
        </div>
        
        <div class="track-info">
            <div class="track-title" id="track-title">No track selected</div>
            <div class="track-artist" id="track-artist">Upload a file to begin</div>
        </div>
        
        <div class="progress-area">
            <div class="progress-bar" id="progress-bar">
                <div class="progress" id="progress"></div>
            </div>
            <div class="time">
                <span class="current" id="current-time">0:00</span>
                <span class="duration" id="duration">0:00</span>
            </div>
        </div>
        
        <div class="controls">
            <button class="control-btn prev" id="prev-btn">⏮</button>
            <button class="control-btn play-pause" id="play-btn">▶</button>
            <button class="control-btn next" id="next-btn">⏭</button>
        </div>
        
        <div class="volume-controls">
            <button class="control-btn volume-icon" id="volume-icon">🔊</button>
            <div class="volume-bar" id="volume-bar">
                <div class="volume-level" id="volume-level"></div>
            </div>
        </div>
        
        <div class="playlist" id="playlist">
            <div class="empty-playlist" id="empty-playlist">No tracks in playlist</div>
        </div>
        
        <div class="upload-area" id="upload-area">
            <div class="upload-icon">𝄞</div>
            <div class="upload-text">Add music files</div>
            <div class="upload-subtext">MP3, WAV, OGG supported</div>
            <input type="file" id="file-input" accept="audio/*" multiple>
        </div>
        
        <div class="player-footer">
            Made in ❤️ By Armeen
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // DOM Elements
            const uploadArea = document.getElementById('upload-area');
            const fileInput = document.getElementById('file-input');
            const albumArt = document.getElementById('album-art');
            const albumImage = document.getElementById('album-image');
            const defaultArt = document.getElementById('default-art');
            const trackTitle = document.getElementById('track-title');
            const trackArtist = document.getElementById('track-artist');
            const playBtn = document.getElementById('play-btn');
            const prevBtn = document.getElementById('prev-btn');
            const nextBtn = document.getElementById('next-btn');
            const progressBar = document.getElementById('progress-bar');
            const progress = document.getElementById('progress');
            const currentTime = document.getElementById('current-time');
            const durationTime = document.getElementById('duration');
            const volumeBar = document.getElementById('volume-bar');
            const volumeLevel = document.getElementById('volume-level');
            const playlist = document.getElementById('playlist');
            const emptyPlaylist = document.getElementById('empty-playlist');
            
            // Audio context and variables
            const audio = new Audio();
            let isPlaying = false;
            let currentSongIndex = 0;
            let songs = [];
            
            // Event Listeners
            uploadArea.addEventListener('click', () => fileInput.click());
            fileInput.addEventListener('change', handleFileUpload);
            playBtn.addEventListener('click', togglePlay);
            prevBtn.addEventListener('click', playPrevious);
            nextBtn.addEventListener('click', playNext);
            progressBar.addEventListener('click', seek);
            volumeBar.addEventListener('click', setVolume);
            audio.addEventListener('loadedmetadata', setAudioDuration);
            audio.addEventListener('timeupdate', updateProgress);
            audio.addEventListener('ended', playNext);
            
            // File upload handler
            function handleFileUpload(e) {
                const files = e.target.files;
                if (files.length === 0) return;
                
                // Clear existing playlist if it's the first upload
                if (songs.length === 0) {
                    playlist.innerHTML = '';
                    emptyPlaylist.classList.add('hidden');
                }
                
                // Process each file
                for (let i = 0; i < files.length; i++) {
                    const file = files[i];
                    
                    // Validate file type
                    if (!file.type.startsWith('audio/')) {
                        alert(`"${file.name}" is not a valid audio file.`);
                        continue;
                    }
                    
                    // Create object URL for the file
                    const url = URL.createObjectURL(file);
                    
                    // Add to songs array
                    songs.push({
                        title: file.name.replace(/\.[^/.]+$/, ""), // Remove file extension
                        artist: 'Unknown Artist',
                        duration: '0:00',
                        url: url,
                        file: file
                    });
                    
                    // Create playlist item
                    createPlaylistItem(file.name.replace(/\.[^/.]+$/, ""), songs.length - 1);
                }
                
                // If we have songs, load the first one if none is playing
                if (songs.length > 0 && !audio.src) {
                    currentSongIndex = 0;
                    loadSong(songs[0]);
                    updateActiveSong();
                }
                
                // Reset file input to allow uploading the same file again
                fileInput.value = '';
            }
            
            // Create playlist item
            function createPlaylistItem(title, index) {
                const playlistItem = document.createElement('div');
                playlistItem.className = 'playlist-item';
                playlistItem.dataset.index = index;
                
                playlistItem.innerHTML = `
                    <div class="playlist-item-info">
                        <div class="playlist-item-title">${title}</div>
                        <div class="playlist-item-artist">Unknown Artist</div>
                    </div>
                    <div class="playlist-item-duration">0:00</div>
                `;
                
                playlistItem.addEventListener('click', function() {
                    const index = parseInt(this.dataset.index);
                    currentSongIndex = index;
                    loadSong(songs[index]);
                    updateActiveSong();
                    
                    if (isPlaying) {
                        audio.play();
                    }
                });
                
                playlist.appendChild(playlistItem);
            }
            
            // Load song into audio player
            function loadSong(song) {
                audio.src = song.url;
                trackTitle.textContent = song.title;
                trackArtist.textContent = song.artist;
                
                // Hide default art and show placeholder
                albumImage.style.display = 'none';
                defaultArt.style.display = 'block';
                defaultArt.textContent = song.title;
                
                // Reset progress
                progress.style.width = '0%';
                currentTime.textContent = '0:00';
                
                // Enable/disable buttons based on playlist length
                prevBtn.disabled = songs.length <= 1;
                nextBtn.disabled = songs.length <= 1;
            }
            
            // Toggle play/pause
            function togglePlay() {
                if (songs.length === 0) return;
                
                if (isPlaying) {
                    audio.pause();
                    playBtn.innerHTML = '▶';
                } else {
                    audio.play();
                    playBtn.innerHTML = '⏸';
                }
                isPlaying = !isPlaying;
            }
            
            // Play previous song
            function playPrevious() {
                if (songs.length <= 1) return;
                
                currentSongIndex = (currentSongIndex - 1 + songs.length) % songs.length;
                loadSong(songs[currentSongIndex]);
                updateActiveSong();
                
                if (isPlaying) {
                    audio.play();
                }
            }
            
            // Play next song
            function playNext() {
                if (songs.length <= 1) return;
                
                currentSongIndex = (currentSongIndex + 1) % songs.length;
                loadSong(songs[currentSongIndex]);
                updateActiveSong();
                
                if (isPlaying) {
                    audio.play();
                }
            }
            
            // Update active song in playlist
            function updateActiveSong() {
                const playlistItems = document.querySelectorAll('.playlist-item');
                playlistItems.forEach((item, index) => {
                    if (index === currentSongIndex) {
                        item.classList.add('active');
                    } else {
                        item.classList.remove('active');
                    }
                });
            }
            
            // Set audio duration when metadata is loaded
            function setAudioDuration() {
                const duration = audio.duration;
                durationTime.textContent = formatTime(duration);
                
                // Update duration in playlist
                if (songs[currentSongIndex]) {
                    songs[currentSongIndex].duration = formatTime(duration);
                    const playlistItems = document.querySelectorAll('.playlist-item');
                    if (playlistItems[currentSongIndex]) {
                        playlistItems[currentSongIndex].querySelector('.playlist-item-duration').textContent = formatTime(duration);
                    }
                }
            }
            
            // Update progress bar
            function updateProgress() {
                if (audio.duration) {
                    const progressPercent = (audio.currentTime / audio.duration) * 100;
                    progress.style.width = `${progressPercent}%`;
                    currentTime.textContent = formatTime(audio.currentTime);
                }
            }
            
            // Seek to position in audio
            function seek(e) {
                if (songs.length === 0) return;
                
                const progressBarWidth = progressBar.clientWidth;
                const clickX = e.offsetX;
                const duration = audio.duration;
                
                audio.currentTime = (clickX / progressBarWidth) * duration;
            }
            
            // Set volume
            function setVolume(e) {
                const volumeBarWidth = volumeBar.clientWidth;
                const clickX = e.offsetX;
                const volumeLevelPercent = (clickX / volumeBarWidth) * 100;
                
                volumeLevel.style.width = `${volumeLevelPercent}%`;
                audio.volume = volumeLevelPercent / 100;
            }
            
            // Format time from seconds to MM:SS
            function formatTime(seconds) {
                const mins = Math.floor(seconds / 60);
                const secs = Math.floor(seconds % 60);
                return `${mins}:${secs < 10 ? '0' : ''}${secs}`;
            }
        });
    </script>
</body>
</html>
