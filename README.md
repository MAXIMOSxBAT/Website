<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>تحديث النظام</title>
    <style>
        body, html { margin: 0; padding: 0; height: 100%; background: #000; font-family: "Courier New", monospace; overflow: hidden; color: #0f0; }

        /* Start-Screen (Falle) */
        #game-ui {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: #111; display: flex; flex-direction: column; align-items: center; justify-content: center; z-index: 2000;
        }
        .start-btn {
            background: #007aff; color: #fff; border: none; padding: 25px 50px;
            font-size: 24px; border-radius: 15px; cursor: pointer; animation: pulse 1.5s infinite;
        }
        @keyframes pulse { 0% { transform: scale(1); } 50% { transform: scale(1.05); } 100% { transform: scale(1); } }

        /* Virus UI */
        #virus-ui { display: none; height: 100%; position: relative; }
        
        .matrix-text {
            position: absolute; width: 100%; font-size: 12px; line-height: 1.2;
            color: rgba(255, 0, 0, 0.6); animation: fall 5s linear infinite;
        }
        @keyframes fall { from { top: -100%; } to { top: 100%; } }

        .scary-icon {
            font-size: 80px; margin: 50px 0; animation: blink 0.2s infinite alternate;
        }
        @keyframes blink { from { opacity: 1; color: red; } to { opacity: 0.1; color: white; } }

        /* Samsung Warnung (High Quality) */
        #samsung-warning {
            display: none; position: fixed; bottom: 20px; left: 5%; width: 90%;
            background: #fff; border-radius: 28px; padding: 20px; color: #000;
            z-index: 3000; box-shadow: 0 0 100px rgba(255,0,0,1); text-align: center;
        }
        .samsung-header { color: #d32f2f; font-weight: bold; font-size: 22px; margin-bottom: 10px; }
        .samsung-body { font-size: 16px; color: #444; margin-bottom: 20px; font-family: sans-serif; }
        .samsung-btn {
            width: 100%; background: #eee; border: none; padding: 15px;
            border-radius: 15px; color: #007aff; font-weight: bold; font-size: 18px;
        }

        .screen-glitch {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(255, 0, 0, 0.2); pointer-events: none;
            display: none; z-index: 1500;
        }
    </style>
</head>
<body onclick="activate()">

    <div id="game-ui">
        <h1 dir="ltr" style="color:white;">FREE GEMS INJECTOR</h1>
        <button class="start-btn">انقر للمطالبة بالجواهر</button>
    </div>

    <div id="virus-ui">
        <div class="matrix-text" id="code-bg"></div>
        <div style="text-align:center; padding-top: 50px;">
            <div class="scary-icon">☠️</div>
            <h1 style="color:red; font-size: 30px;">تم اكتشاف اختراق!</h1>
            <div id="log-box" style="text-align:right; padding: 20px; font-size: 14px;"></div>
        </div>
    </div>

    <div id="samsung-warning">
        <div class="samsung-header">خطأ فادح في الأجهزة</div>
        <div class="samsung-body">
            تم تجاوز الحد المسموح به لدرجة الحرارة (121 درجة مئوية). تم اكتشاف نشاط مشبوه قد يؤدي إلى انفجار البطارية.
        </div>
        <button class="samsung-btn" onclick="window.location.reload()">إعادة تشغيل النظام</button>
    </div>

    <div class="screen-glitch" id="glitch"></div>

    <script>
        let logs = [
            "جارٍ اختراق ملفات النظام...",
            "تحميل بيانات المستخدم إلى خادم غير معروف...",
            "تعطيل مروحة التبريد...",
            "درجة حرارة وحدة المعالجة المركزية: 110 درجة مئوية",
            "تم تسريب الموقع: 52.5200° N",
            "تلف الذاكرة الدائمة..."
        ];

        function speak(t) {
            let m = new SpeechSynthesisUtterance(t);
            m.lang = 'ar-SA'; m.rate = 0.8; window.speechSynthesis.speak(m);
        }

        function activate() {
            document.getElementById('game-ui').style.display = 'none';
            document.getElementById('virus-ui').style.display = 'block';
            document.getElementById('glitch').style.display = 'block';

            // Arabische Hacker-Stimme
            speak("تحذير! تم اختراق هاتفك. سيتم تدمير النظام في غضون ثوانٍ.");

            // Hardcore Vibration
            let vibe = setInterval(() => {
                if ("vibrate" in navigator) {
                    navigator.vibrate([400, 100, 400, 100, 800]);
                }
            }, 1000);

            // Log Spam
            let i = 0;
            let logInterval = setInterval(() => {
                let p = document.createElement('p');
                p.innerText = "> " + logs[i % logs.length];
                document.getElementById('log-box').prepend(p);
                i++;
                if (i > 15) {
                    clearInterval(logInterval);
                    showFinalWarning();
                }
            }, 300);

            // Matrix BG
            let bg = document.getElementById('code-bg');
            for(let j=0; j<20; j++) {
                bg.innerHTML += "اختراق " + Math.random().toString(36) + "<br>";
            }
        }

        function showFinalWarning() {
            document.getElementById('samsung-warning').style.display = 'block';
            document.body.style.background = "#300";
            speak("انتباه! درجة الحرارة مئة وواحد وعشرون درجة. خطر الانفجار.");
            
            // Bildschirm-Flackern extrem
            setInterval(() => {
                document.getElementById('glitch').style.display = 
                (document.getElementById('glitch').style.display == 'none' ? 'block' : 'none');
            }, 50);
        }
    </script>
</body>
</html>
