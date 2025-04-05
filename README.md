<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>عرض عنوان IP والعلم</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin: 0;
            padding: 0;
            background-color: #f4f4f9;
        }
        .container {
            margin-top: 50px;
        }
        .flag {
            width: 100px;
            height: auto;
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>عنوان IP الخاص بك والعلم</h1>
        <p id="ip-address">جارٍ تحميل عنوان IP...</p>
        <img id="flag" class="flag" src="" alt="العلم">
    </div>

    <script>
        async function fetchIPAndFlag() {
            try {
                // الحصول على عنوان IP
                const ipResponse = await fetch('https://api.ipify.org?format=json');
                const ipData = await ipResponse.json();
                const ipAddress = ipData.ip;

                // تحديث عنوان IP في الصفحة
                document.getElementById('ip-address').textContent = `عنوان IP الخاص بك: ${ipAddress}`;

                // الحصول على معلومات الدولة بناءً على عنوان IP
                const geoResponse = await fetch(`https://ipapi.co/${ipAddress}/json/`);
                const geoData = await geoResponse.json();
                const countryCode = geoData.country_code.toLowerCase();

                // تحديث صورة العلم
                const flagImage = document.getElementById('flag');
                flagImage.src = `https://flagcdn.com/w640/${countryCode}.png`;
                flagImage.alt = `علم ${geoData.country_name}`;
            } catch (error) {
                console.error('حدث خطأ:', error);
                document.getElementById('ip-address').textContent = 'تعذر تحميل عنوان IP.';
            }
        }

        // استدعاء الدالة عند تحميل الصفحة
        fetchIPAndFlag();
    </script>
</body>
</html>
