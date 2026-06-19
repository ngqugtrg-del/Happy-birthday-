<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Happy Birthday Cô Gái 18! ✨</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Caveat:wght@600;700&family=Comfortaa:wght@400;700&display=swap" rel="stylesheet">
    
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
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
            display: flex;
            justify-content: center;
            align-items: center;
            perspective: 1500px;
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
            display: flex; flex-direction: column; justify-content: center; align-items: center;
            opacity: 0; visibility: hidden; z-index: 2;
            transition: opacity 1s ease-in-out, visibility 1s;
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
        
        /* Tạo hình cây nến cute */
        .candle-wrapper { cursor: pointer; display: inline-block; position: relative; margin-top: 15px; }
        .flame {
            width: 16px; height: 26px; background: #ff9e00; border-radius: 50% 50% 20% 20%;
            position: absolute; top: -24px; left: 7px; animation: flicker 0.1s infinite alternate;
            box-shadow: 0 0 15px #ff9e00, 0 0 5px #fff;
        }
        .candle-stick { width: 30px; height: 65px; background: linear-gradient(to right, #ffb7b2, #ff9aa2); border-radius: 6px; }

        /* MÀN HÌNH 3: BẦU TRỜI ĐÊM LUNG LINH & ẢNH CÔ ẤY */
        .girl-card {
            display: flex; align-items: center; justify-content: center; gap: 40px;
            max-width: 900px; background: rgba(255, 255, 255, 0.07);
            padding: 45px; border-radius: 32px; backdrop-filter: blur(8px);
            border: 2px solid rgba(255, 183, 178, 0.2);
            box-shadow: 0 20px 40px rgba(0,0,0,0.3);
        }
        .girl-img {
            width: 250px; height: 250px; border-radius: 50%; object-fit: cover;
            border: 6px solid var(--pink-pastel); box-shadow: 0 0 30px rgba(255, 183, 178, 0.6);
        }
        .wish-text1 { color: #ffffff; font-size: 21px; line-height: 1.8; text-align: left; flex: 1; font-weight: 400; }

        /* MÀN HÌNH 4: CÁC TỜ NOTE VÀ ĐỒNG HỒ CÁT TƯƠNG LAI */
        .note-wrapper { position: relative; width: 500px; height: 530px; }
        .sticky-note {
            position: absolute; top: 0; left: 0; width: 100%; height: 100%;
            background: var(--paper-color); padding: 45px;
            box-shadow: 10px 10px 30px rgba(0,0,0,0.25); border-radius: 20px;
            border-left: 6px solid var(--pink-pastel); transform-origin: left top;
            transition: transform 1.3s cubic-bezier(0.25, 1, 0.5, 1), opacity 1s;
        }
        .sticky-note::before { content: '📌'; position: absolute; top: -15px; left: 47%; font-size: 26px; }
        .note-content { font-family: 'Caveat', cursive; font-size: 28px; line-height: 38px; color: #2d2d2d; text-align: left; white-space: pre-wrap; }
        
        /* Hiệu ứng lật trang sổ mượt mà */
        .flipped { transform: rotate(-115deg) translateY(180px) scale(0.7); opacity: 0; pointer-events: none; }

        /* ĐỒNG HỒ CÁT VÀ Ô NHẬP ĐIỀU ƯỚC */
        .hourglass-container { display: none; flex-direction: column; align-items: center; animation: fadeInUp 1s ease-in-out forwards; }
        .hourglass-icon { font-size: 70px; color: var(--yellow-pastel); cursor: pointer; animation: rotateHourglass 2.5s infinite ease-in-out; text-shadow: 0 0 15px rgba(255, 218, 193, 0.4); }
        .future-title { color: #fff; font-size: 22px; margin: 25px 0 15px 0; font-weight: 600; }
        
        /* Tờ note nhỏ tự gõ điều ước */
        .wish-note-paper {
            background: #fff; padding: 30px; border-radius: 20px; width: 420px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.3); display: none; margin-top: 15px;
            border-top: 5px solid var(--yellow-pastel); position: relative;
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

    <div class="screen active-screen" id="screen1">
        <div class="loading-text">💖 ĐANG CHUẨN BỊ BẤT NGỜ... 💖</div>
    </div>

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

    <div class="screen" id="screen3">
        <div class="girl-card">
            <img src="anh-cua-em.jpg" alt="Her Portrait" class="girl-img" onerror="this.src='https://images.unsplash.com/photo-1524504388940-b1c1722653e1?w=500'">
            <div class="wish-text1" id="typewriter1"></div>
        </div>
    </div>

    <div class="screen" id="screen4">
        <div class="note-wrapper" id="noteWrapper">
            <div class="sticky-note" id="note1">
                <div class="note-content" id="typewriter2"></div>
            </div>
        </div>

        <div class="hourglass-container" id="hourglassContainer">
            <div class="hourglass-icon" onclick="openFutureNote()"><i class="fa-solid fa-hourglass-start"></i></div>
            <div class="future-title">Gửi 1 điều ước của em vào tương lai</div>
            
            <div class="wish-note-paper" id="wishNotePaper">
                <textarea placeholder="Gõ điều ước tuổi 18 của em vào đây nhé... ✨"></textarea>
                <button class="btn-send" onclick="submitFutureWish()">Gửi vào dòng thời gian 🚀</button>
            </div>
        </div>
    </div>

    <audio id="happyBirthdayMusic" src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3" loop></audio>

    <script>
        // Nội dung văn bản chuẩn xác theo yêu cầu của bạn
        const textScreen3 = "tuổi mới anh chúc em luôn giữ được sự lạc quan, nụ cười và tính cách cáu kỉnh của em, hay luôn luôn giữ lấy nó nhé Happy birthday🎂";
        const textScreen4 = "anh biết em có nhiều dự định trong tương lai, chắc chăn sẽ bận rộn. Nhưng đừng bỏ cuộc nhé, nếu chán quá thì vào làm support cho anh cũng được hoặc có thể về Việt Nam, anh sẽ dẫn em đi chụp ảnh. Hoặc có thể về đây làm mẫu ảnh cho anh cũng được. Nói vậy thôi chứ dù gì em cũng đã chọn con đường nào, đối mặt với áp lực ra sao thì quay về đây có mấy con vợ đang đợi em chơi game nhé. Tuổi mới chúc cô gái 18 luôn kiên cường. Lúc nào cảm thấy mệt mỏi, áp lực quá thì tìm đến bọn anh nhé.";

        const s1 = document.getElementById('screen1');
        const s2 = document.getElementById('screen2');
        const s3 = document.getElementById('screen3');
        const s4 = document.getElementById('screen4');

        // Hàm hiệu ứng chữ gõ máy tự động
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

        // MÀN HÌNH 1: Bắn pháo hoa liên tiếp trong vòng 5 giây đầu tiên khi vừa tải trang
        window.onload = function() {
            let duration = 5000;
            let end = Date.now() + duration;

            (function firework() {
                confetti({ particleCount: 7, angle: 60, spread: 55, origin: { x: 0, y: 0.8 } });
                confetti({ particleCount: 7, angle: 120, spread: 55, origin: { x: 1, y: 0.8 } });
                if (Date.now() < end) { requestAnimationFrame(firework); }
            }());

            // Hết 5s pháo hoa chuyển sang Màn hình 2
            setTimeout(() => {
                s1.classList.remove('active-screen');
                s2.classList.add('active-screen');
            }, 5000);
        };

        // MÀN HÌNH 2: Hành động click tắt nến -> Mở hộp quà phát nhạc -> Sang màn hình 3
        function openGiftBox() {
            document.getElementById('flame').style.display = 'none'; // Tắt ngọn nến
            
            // Hiệu ứng nổ pháo hoa giấy nhẹ chúc mừng
            confetti({ particleCount: 120, spread: 70, origin: { y: 0.6 } });
            
            // Bật nhạc nền sinh nhật tự động phát
            document.getElementById('happyBirthdayMusic').play().catch(() => {
                console.log("Trình duyệt yêu cầu tương tác để phát nhạc.");
            });

            // Chuyển cảnh sang Bầu trời đêm lung linh & Ảnh cô ấy
            setTimeout(() => {
                s2.classList.remove('active-screen');
                s3.classList.add('active-screen');
                
                // Chạy từ từ dòng chữ chúc mừng ở màn hình 3
                setTimeout(() => {
                    typewriterEffect('typewriter1', textScreen3, 60, () => {
                        // Gõ xong chữ, đợi đúng 5 giây sau xuất hiện tờ Note ở màn hình 4
                        setTimeout(() => {
                            s3.classList.remove('active-screen');
                            s4.classList.add('active-screen');
                            
                            // Tiến hành gõ chữ viết tay mềm mại trên tờ Note giả lập
                            setTimeout(() => {
                                typewriterEffect('typewriter2', textScreen4, 50, () => {
                                    // Chữ viết tay chạy xong -> Đợi tiếp đúng 10 giây sau
                                    setTimeout(() => {
                                        // Tờ note lật cuốn đi mượt mà ra phía sau
                                        document.getElementById('note1').classList.add('flipped');
                                        // Chiếc đồng hồ cát đáng yêu nhảy ra
                                        document.getElementById('hourglassContainer').style.display = 'flex';
                                    }, 10000);
                                });
                            }, 1000);
                        }, 5000);
                    });
                }, 1000);
            }, 1200);
        }

        // HÀNH ĐỘNG: Click đồng hồ cát hiện tờ note nhỏ tự gõ điều ước
        function openFutureNote() {
            document.getElementById('wishNotePaper').style.display = 'block';
        }

        // CÁI KẾT: Ấn gửi điều ước -> Tim bay tung tóe rực rỡ + hiện popup thông báo
        function submitFutureWish() {
            let heartDuration = 4000;
            let heartEnd = Date.now() + heartDuration;

            (function heartRain() {
                if (Date.now() > heartEnd) return;
                // Cấu hình sinh confetti hình trái tim/màu hồng đỏ lãng mạn
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

            // Hiện thông báo kết thúc ngọt ngào đúng từng chữ của bạn
            setTimeout(() => {
                alert("💘 điều ước của em đã được khoá lại trong dòng thời gian của mình, hẹn gặp lại em 1 ngày gần nhất ở Việt Nam");
            }, 400);
        }
    </script>
</body>
</html># 18-7
