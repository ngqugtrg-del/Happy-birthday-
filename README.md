
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Happy Birthday Cô Gái 18! ✨</title>
    <!-- Font chữ Comfortaa (bo tròn cute) và font Caveat (viết tay mềm mại) -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Caveat:wght@600;700&family=Comfortaa:wght@400;700&display=swap" rel="stylesheet">
    
    <!-- Thư viện tạo pháo hoa, pháo giấy và tim bay mượt mà -->
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
    <!-- Bộ icon FontAwesome siêu cute -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">

    <style>
        :root {
            --bg-dark-cute: #1e1a24;
            --pink-pastel: #ffb7b2;
            --yellow-pastel: #ffdac1;
            --mint-pastel: #e2f0cb;
            --paper-color: #fffaf0;
        }

        * { box-sizing: border-box; margin: 0; padding: 0; }
        
        body {
            background-color: var(--bg-dark-cute);
            font-family: 'Comfortaa', cursive;
            overflow: hidden;
            height: 100vh;
            width: 100vw;
            display: flex;
            justify-content: center;
            align-items: center;
            perspective: 1500px;
            margin: 0;
            padding: 0;
        }

        /* NỀN SAO LẤP LÁNH CHUNG */
        .star-bg {
            position: absolute; top: 0; left: 0; width: 100%; height: 100%;
            background: url('https://www.transparenttextures.com/patterns/stardust.png');
            opacity: 0.3; pointer-events: none; z-index: 1;
        }

        /* KHUNG CHUẨN CHO CÁC MÀN HÌNH */
        .screen {
            position: absolute; width: 100%; height: 100%;
            top: 0; left: 0;
            display: flex; flex-direction: column; justify-content: center; align-items: center;
            opacity: 0; visibility: hidden; z-index: 2;
            transition: opacity 1s ease-in-out, visibility 1s, background-image 1.2s ease-in-out;
            padding: 20px;
            text-align: center;
        }
        .active-screen { opacity: 1; visibility: visible; }

        /* MÀN HÌNH 1: PHÁO HOA KHI VỪA MỞ WEB */
        #screen1 { background: #0c0a10; }
        .loading-text { color: #fff; font-size: 20px; font-weight: 300; letter-spacing: 3px; animation: pulse 1.5s infinite alternate; }

        /* MÀN HÌNH 2: HỘP QUÀ + CÂY NẾN CUTE */
        .gift-container {
            background: rgba(255, 255, 255, 0.05); padding: 40px; border-radius: 24px;
            border: 2px dashed var(--pink-pastel); max-width: 550px;
            box-shadow: 0 15px 30px rgba(0,0,0,0.2);
        }
        .gift-box { font-size: 90px; animation: bounceWiggle 0.6s infinite alternate; margin-bottom: 10px; }
        .package-text { color: #fff; font-size: 18px; margin-bottom: 25px; line-height: 1.6; }
        
        /* Cây nến cute */
        .candle-wrapper { cursor: pointer; display: inline-block; position: relative; margin-top: 15px; }
        .flame {
            width: 16px; height: 26px; background: #ff9e00; border-radius: 50% 50% 20% 20%;
            position: absolute; top: -24px; left: 7px; animation: flicker 0.1s infinite alternate;
            box-shadow: 0 0 15px #ff9e00, 0 0 5px #fff;
        }
        .candle-stick { width: 30px; height: 65px; background: linear-gradient(to right, #ffb7b2, #ff9aa2); border-radius: 6px; }

        /* MÀN HÌNH 3: ẢNH NỀN 1 (BÀN HỌC & MÁY ẢNH) */
        #screen3 {
            background-image: linear-gradient(rgba(20, 16, 26, 0.45), rgba(20, 16, 26, 0.75)), url('723987831_972374652461047_273943143000118799_n.jpg');
            background-size: cover;
            background-position: center;
            background-repeat: no-repeat;
        }
        .wish-text-wrapper {
            max-width: 650px; background: rgba(30, 26, 36, 0.8); padding: 35px; border-radius: 24px;
            backdrop-filter: blur(4px); border: 1px solid rgba(255, 183, 178, 0.25);
            box-shadow: 0 12px 30px rgba(0,0,0,0.4); margin: 20px;
        }
        .wish-text1 { color: #ffffff; font-size: 22px; line-height: 1.8; text-align: center; font-weight: 400; }

        /* MÀN HÌNH 4: BAN ĐẦU KHÔNG CÓ NỀN (HIỂN THỊ NOTE & ẢNH ÁO DÀI) */
        #screen4 {
            background-size: cover;
            background-position: center;
            background-repeat: no-repeat;
        }

        /* Khung chứa note và ảnh áo dài */
        .content-split-container {
            display: flex; align-items: center; justify-content: center; gap: 40px;
            max-width: 1100px; width: 100%; padding: 20px;
            transition: transform 1.3s ease-in-out, opacity 1s;
            transform-origin: left top;
        }
        
        /* Cấu trúc tờ note */
        .note-wrapper { position: relative; width: 480px; height: 530px; flex-shrink: 0; }
        .sticky-note {
            position: absolute; top: 0; left: 0; width: 100%; height: 100%;
            background: var(--paper-color); padding: 40px 35px;
            box-shadow: 10px 10px 30px rgba(0,0,0,0.25); border-radius: 20px;
            border-left: 6px solid var(--pink-pastel);
        }
        .sticky-note::before { content: '📌'; position: absolute; top: -15px; left: 47%; font-size: 26px; }
        .note-content { font-family: 'Caveat', cursive; font-size: 26px; line-height: 35px; color: #2d2d2d; text-align: left; white-space: pre-wrap; }
        
        /* Cấu trúc ảnh áo dài bên hồ cá */
        .side-image-wrapper {
            width: 380px; height: 530px; flex-shrink: 0;
            border-radius: 24px; overflow: hidden;
            border: 5px solid rgba(255, 255, 255, 0.1);
            box-shadow: 15px 15px 35px rgba(0,0,0,0.3);
            background: rgba(255, 255, 255, 0.05);
        }
        .side-image { width: 100%; height: 100%; object-fit: cover; }

        /* Hiệu ứng lật cụm cũ biến mất mượt mà */
        .flipped { transform: rotate(-115deg) translateY(200px) scale(0.6); opacity: 0; pointer-events: none; }

        /* ĐỒNG HỒ CÁT VÀ Ô NHẬP ĐIỀU ƯỚC KHI BACKGROUND MỚI HIỆN RA */
        .hourglass-container { display: none; flex-direction: column; align-items: center; animation: fadeInUp 1s ease-in-out forwards; z-index: 5; }
        .hourglass-icon { font-size: 70px; color: var(--yellow-pastel); cursor: pointer; animation: rotateHourglass 2.5s infinite ease-in-out; text-shadow: 0 0 15px rgba(255, 218, 193, 0.4); }
        .future-title { color: #fff; font-size: 22px; margin: 25px 0 15px 0; font-weight: 600; text-shadow: 0 2px 8px rgba(0,0,0,0.6); }
        
        /* Tờ note viết điều ước nhỏ nhắn */
        .wish-note-paper {
            background: rgba(255, 255, 255, 0.95); padding: 30px; border-radius: 20px; width: 420px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.4); display: none; margin-top: 15px;
            border-top: 5px solid var(--yellow-pastel); position: relative;
            backdrop-filter: blur(5px);
        }
        .wish-note-paper::before { content: '✨'; position: absolute; top: -12px; right: 20px; font-size: 20px; }
        .wish-note-paper textarea {
            width: 100%; height: 90px; border: 2px dashed var(--pink-pastel);
            border-radius: 12px; padding: 12px; font-family: 'Comfortaa'; resize: none; outline: none; font-size: 14px; background: #fffdf9;
        }
        .btn-send {
            background: linear-gradient(135deg, var(--pink-pastel), #ff9aa2); border: none; padding: 12px 25px;
            border-radius: 25px; color: #333; font-weight: bold; cursor: pointer;
            margin-top: 15px; font-family: 'Comfortaa'; transition: transform 0.2s, box-shadow 0.2s; box-shadow: 0 5px 10px rgba(255, 183, 178, 0.4);
        }
        .btn-send:hover { transform: scale(1.05); box-shadow: 0 7px 14px rgba(255, 183, 178, 0.6); }

        /* RESPONSIVE CHO MÀN HÌNH ĐIỆN THOẠI */
        @media (max-width: 900px) {
            .content-split-container { flex-direction: column; height: 90vh; overflow-y: auto; gap: 20px; }
            .note-wrapper { width: 100%; max-width: 440px; height: 420px; }
            .side-image-wrapper { width: 100%; max-width: 440px; height: 320px; }
            .note-content { font-size: 22px; line-height: 30px; }
            .wish-note-paper { width: 90%; }
        }

        /* CÁC EFFECT ANIMATION */
        @keyframes bounceWiggle { 0% { transform: translateY(0) scale(1); } 100% { transform: translateY(-10px) scale(1.05); } }
        @keyframes flicker { 0% { transform: scale(1); opacity: 0.9; } 100% { transform: scale(1.15); opacity: 1; } }
        @keyframes rotateHourglass { 0%, 100% { transform: rotate(0deg); } 40%, 60% { transform: rotate(180deg); } }
        @keyframes pulse { from { opacity: 0.5; } to { opacity: 1; } }
        @keyframes fadeInUp { from { opacity: 0; transform: translateY(30px); } to { opacity: 1; transform: translateY(0); } }
    </style>
</head>
<body>

    <div class="star-bg"></div>

    <!-- MÀN HÌNH 1: MÀN PHÁO HOA HOÀNH TRÁNG 5 GIÂY ĐẦU -->
    <div class="screen active-screen" id="screen1">
        <div class="loading-text">💖 ĐANG CHUẨN BỊ BẤT NGỜ... 💖</div>
    </div>

    <!-- MÀN HÌNH 2: HỘP QUÀ NHÚC NHÍCH + THỔI NẾN -->
    <div class="screen" id="screen2">
        <div class="gift-container">
            <div class="gift-box">🎁</div>
            <div class="package-text">Có một bưu kiện đặc biệt mà Trường muốn gửi cho bạn. Hãy ước một điều rồi nhấp vào cây nến dễ thương bên dưới để tắt nến nhé!</div>
            
            <div class="candle-wrapper" onclick="openGiftBox()">
                <div class="flame" id="flame"></div>
                <div class="candle-stick"></div>
            </div>
        </div>
    </div>

    <!-- MÀN HÌNH 3: ẢNH NỀN BÀN HỌC + CHỮ CHẠY -->
    <div class="screen" id="screen3">
        <div class="wish-text-wrapper">
            <div class="wish-text1" id="typewriter1"></div>
        </div>
    </div>

    <!-- MÀN HÌNH 4: TỜ NOTE VÀ TẤM ẢNH ÁO DÀI (KHI CHỮ CHẠY XONG SẼ THAY NỀN ĐIỀU ƯỚC) -->
    <div class="screen" id="screen4">
        <div class="content-split-container" id="splitContainer">
            <!-- Bên trái: Tờ note viết tay chạy chữ -->
            <div class="note-wrapper">
                <div class="sticky-note">
                    <div class="note-content" id="typewriter2"></div>
                </div>
            </div>
            
            <!-- Bên phải: Tấm ảnh áo dài dịu dàng bên hồ cá -->
            <div class="side-image-wrapper">
                <img src="716009889_1544247957334848_2396107189527443984_n.jpg" alt="Her Lovely Portrait" class="side-image">
            </div>
        </div>

        <!-- Khối đồng hồ cát bí ẩn hiện ra sau khi lật Note -->
        <div class="hourglass-container" id="hourglassContainer">
            <div class="hourglass-icon" onclick="openFutureNote()"><i class="fa-solid fa-hourglass-start"></i></div>
            <div class="future-title">Gửi 1 điều ước của em vào tương lai</div>
            
            <div class="wish-note-paper" id="wishNotePaper">
                <textarea placeholder="Gõ điều ước tuổi 18 của em vào đây nhé... ✨"></textarea>
                <button class="btn-send" onclick="submitFutureWish()">Gửi vào dòng thời gian 🚀</button>
            </div>
        </div>
    </div>

    <!-- NHẠC NỀN -->
    <audio id="happyBirthdayMusic" src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3" loop></audio>

    <script>
        // Nội dung văn bản
        const textScreen3 = "tuổi mới anh chúc em luôn giữ được sự lạc quan, nụ cười và tính cách cáu kỉnh của em, hay luôn luôn giữ lấy nó nhé Happy birthday🎂";
        const textScreen4 = "anh biết em có nhiều dự định trong tương lai, chắc chăn sẽ bận rộn. Nhưng đừng bỏ cuộc nhé, nếu chán quá thì vào làm support cho anh cũng được hoặc có thể về Việt Nam, anh sẽ dẫn em đi chụp ảnh. Hoặc có thể về đây làm mẫu ảnh cho anh cũng được. Nói vậy thôi chứ dù gì em cũng đã chọn con đường nào, đối mặt với áp lực ra sao thì quay về đây có mấy con vợ đang đợi em chơi game nhé. Tuổi mới chúc cô gái 18 luôn kiên cường. Lúc nào cảm thấy mệt mỏi, áp lực quá thì tìm đến bọn anh nhé.";

        const s1 = document.getElementById('screen1');
        const s2 = document.getElementById('screen2');
        const s3 = document.getElementById('screen3');
        const s4 = document.getElementById('screen4');

        function typewriterEffect(elementId, text, speed, callback) {
            let index = 0;
            const target = document.getElementById(elementId);
            function play() {
                if (index < text.length) {
                    target.innerHTML += text.charAt(index);
                    index++;
                    setTimeout(play, speed);
                } else if (callback) {
                    callback();
                }
            }
            play();
        }

        // MÀN HÌNH 1: Pháo hoa khai màn (5 giây)
        window.onload = function() {
            let duration = 5000;
            let end = Date.now() + duration;

            (function firework() {
                confetti({ particleCount: 7, angle: 60, spread: 55, origin: { x: 0, y: 0.8 } });
                confetti({ particleCount: 7, angle: 120, spread: 55, origin: { x: 1, y: 0.8 } });
                if (Date.now() < end) { requestAnimationFrame(firework); }
            }());

            setTimeout(() => {
                s1.classList.remove('active-screen');
                s2.classList.add('active-screen');
            }, 5000);
        };

        // MÀN HÌNH 2: Thổi nến và mở hộp quà
        function openGiftBox() {
            document.getElementById('flame').style.display = 'none';
            confetti({ particleCount: 120, spread: 70, origin: { y: 0.6 } });
            document.getElementById('happyBirthdayMusic').play().catch(() => {});

            setTimeout(() => {
                s2.classList.remove('active-screen');
                s3.classList.add('active-screen');
                
                setTimeout(() => {
                    typewriterEffect('typewriter1', textScreen3, 60, () => {
                        // Chữ chạy xong, đợi 5 giây đổi sang màn hình 4
                        setTimeout(() => {
                            s3.classList.remove('active-screen');
                            s4.classList.add('active-screen');
                            
                            setTimeout(() => {
                                typewriterEffect('typewriter2', textScreen4, 45, () => {
                                    // Văn bản tờ note chạy xong, đợi tiếp 10 giây
                                    setTimeout(() => {
                                        // Toàn bộ cụm Note + Ảnh cũ lật biến mất mượt mà
                                        document.getElementById('splitContainer').classList.add('flipped');
                                        
                                        // CHUYỂN ĐỔI BACKGROUND SANG TẤM ẢNH GƯƠNG ĐÔI ĐIỀU ƯỚC
                                        s4.style.backgroundImage = "linear-gradient(rgba(20, 16, 26, 0.5), rgba(20, 16, 26, 0.75)), url('717227966_904823359312485_6118816974694409286_n.jpg')";
                                        
                                        // Hiện đồng hồ cát viết điều ước lên trên nền ảnh mới
                                        document.getElementById('hourglassContainer').style.display = 'flex';
                                    }, 10000);
                                });
                            }, 1000);
                        }, 5000);
                    });
                }, 1000);
            }, 1200);
        }

        function openFutureNote() {
            document.getElementById('wishNotePaper').style.display = 'block';
        }

        function submitFutureWish() {
            let heartDuration = 4000;
            let heartEnd = Date.now() + heartDuration;

            (function heartRain() {
                if (Date.now() > heartEnd) return;
                confetti({
                    particleCount: 4,
                    angle: randomRange(60, 120),
                    spread: 50,
                    origin: { x: Math.random(), y: Math.random() - 0.2 },
                    colors: ['#ff9aa2', '#ffb7b2', '#ff7b7b', '#ffb3ba']
                });
                requestAnimationFrame(heartRain);
            }());

            function randomRange(min, max) { return Math.random() * (max - min) + min; }

            setTimeout(() => {
                alert("💘 điều ước của em đã được khoá lại trong dòng thời gian của mình, hẹn gặp lại em 1 ngày gần nhất ở Việt Nam");
            }, 400);
        }
    </script>
</body>
</html>
