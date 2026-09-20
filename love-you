import base64
import os
import streamlit as st
import streamlit.components.v1 as components

# Pengaturan halaman Streamlit
st.set_page_config(
    page_title="I Love You <3",
    page_icon="💙",
    layout="centered",
    initial_sidebar_state="collapsed",
)


# Fungsi membaca file lagu ke format Base64 agar audio bisa jalan di mana saja
def get_audio_base64(file_path):
  if os.path.exists(file_path):
    with open(file_path, "rb") as f:
      return base64.b64encode(f.read()).decode()
  return ""


# Mengambil data lagu love_you.mp3
audio_b64 = get_audio_base64("love_you.mp3")
audio_src = (
    f"data:audio/mp3;base64,{audio_b64}" if audio_b64 else "love_you.mp3"
)

# Kode HTML & Canvas Animasi Hati
html_code = f"""
<!DOCTYPE html>
<html>
<head>
    <style>
        body {{
            margin: 0;
            background: #000000;
            overflow: hidden;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }}
        canvas {{
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
        }}
        .center-text {{
            position: absolute;
            color: #ffffff;
            font-size: 2.8rem;
            font-weight: bold;
            text-align: center;
            z-index: 10;
            text-shadow: 0 0 10px #00bfff, 0 0 20px #00bfff, 0 0 30px #1e90ff, 0 0 40px #1e90ff;
            animation: pulse 2s infinite ease-in-out;
            pointer-events: none;
        }}
        @keyframes pulse {{
            0%, 100% {{ transform: scale(1); }}
            50% {{ transform: scale(1.08); }}
        }}
        .btn-play {{
            position: absolute;
            bottom: 30px;
            z-index: 20;
            padding: 12px 28px;
            background: linear-gradient(135deg, #1e90ff, #00bfff);
            color: white;
            border: none;
            border-radius: 25px;
            font-size: 1rem;
            font-weight: bold;
            cursor: pointer;
            box-shadow: 0 0 15px rgba(0, 191, 255, 0.6);
            transition: transform 0.2s;
        }}
        .btn-play:hover {{
            transform: scale(1.05);
        }}
    </style>
</head>
<body>
    <canvas id="canvas"></canvas>
    <div class="center-text">Love You</div>
    <button class="btn-play" onclick="playAudio(this)">🎵 Putar Lagu 🎵</button>

    <audio id="bgMusic" loop>
        <source src="{audio_src}" type="audio/mp3">
    </audio>

    <script>
        const canvas = document.getElementById('canvas');
        const ctx = canvas.getContext('2d');
        let width = canvas.width = window.innerWidth;
        let height = canvas.height = window.innerHeight;

        window.addEventListener('resize', () => {{
            width = canvas.width = window.innerWidth;
            height = canvas.height = window.innerHeight;
        }});

        function heartXY(t) {{
            const x = 16 * Math.pow(Math.sin(t), 3);
            const y = 13 * Math.cos(t) - 5 * Math.cos(2*t) - 2 * Math.cos(3*t) - Math.cos(4*t);
            return {{ x: x, y: -y }};
        }}

        const colors = ['#4682B4', '#1E90FF', '#00BFFF', '#6495ED', '#4169E1'];
        const words = ['love you', 'Love You', 'LOVE YOU'];
        const particles = [];

        for (let i = 0; i < 180; i++) {{
            const t = (i / 180) * Math.PI * 2;
            const pos = heartXY(t);
            const scale = Math.min(width, height) / 45;
            particles.push({{
                x: width / 2 + pos.x * scale,
                y: height / 2 + pos.y * scale,
                word: words[Math.floor(Math.random() * words.length)],
                color: colors[Math.floor(Math.random() * colors.length)],
                size: Math.random() * 4 + 13,
                alpha: Math.random()
            }});
        }}

        function draw() {{
            ctx.fillStyle = 'rgba(0, 0, 0, 0.2)';
            ctx.fillRect(0, 0, width, height);

            particles.forEach(p => {{
                p.alpha += 0.02;
                if (p.alpha > 1) p.alpha = 0.2;

                ctx.shadowBlur = 12;
                ctx.shadowColor = p.color;
                ctx.fillStyle = p.color;
                ctx.globalAlpha = p.alpha;
                ctx.font = `bold ${{p.size}}px Arial`;
                ctx.fillText(p.word, p.x, p.y);
            }});

            requestAnimationFrame(draw);
        }}
        draw();

        function playAudio(btn) {{
            const music = document.getElementById('bgMusic');
            music.play();
            btn.style.display = 'none';
        }}
    </script>
</body>
</html>
"""

# Tampilkan komponen HTML di Streamlit
components.html(html_code, height=620)
