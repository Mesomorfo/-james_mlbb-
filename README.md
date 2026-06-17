<!jemes mlbvhtml>
<html lang="ky">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ML Diamond Shop - Алмаз сатуу</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, sans-serif;
        }

        body {
            background: linear-gradient(135deg, #1a1a2e 0%, #16213e 50%, #0f3460 100%);
            color: #fff;
            min-height: 100vh;
        }

        /* HEADER */
        header {
            background: rgba(0, 0, 0, 0.4);
            padding: 20px 40px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            backdrop-filter: blur(10px);
            position: sticky;
            top: 0;
            z-index: 100;
        }

        .logo {
            font-size: 24px;
            font-weight: bold;
            color: #ffd700;
        }

        .logo span {
            color: #4fc3f7;
        }

        nav a {
            color: #fff;
            text-decoration: none;
            margin-left: 25px;
            transition: 0.3s;
        }

        nav a:hover {
            color: #ffd700;
        }

        /* HERO */
        .hero {
            text-align: center;
            padding: 40px 20px;
        }

        .hero h1 {
            font-size: 42px;
            margin-bottom: 15px;
        }

        .hero h1 span {
            color: #ffd700;
        }

        .hero p {
            font-size: 18px;
            color: #b0bec5;
        }

        /* FORM */
        .container {
            max-width: 1100px;
            margin: 0 auto;
            padding: 20px;
        }

        .id-box {
            background: rgba(255, 255, 255, 0.08);
            border-radius: 15px;
            padding: 30px;
            margin-bottom: 30px;
            display: flex;
            gap: 15px;
            flex-wrap: wrap;
        }

        .id-box input {
            flex: 1;
            min-width: 200px;
            padding: 14px;
            border: none;
            border-radius: 10px;
            background: rgba(255, 255, 255, 0.15);
            color: #fff;
            font-size: 16px;
        }

        .id-box input::placeholder {
            color: #b0bec5;
        }

        /* Full width phone input field style */
        .id-box #userPhone {
            flex: 1 1 100%;
        }

        /* DIAMOND CARDS */
        .section-title {
            font-size: 24px;
            margin-bottom: 20px;
            border-left: 4px solid #ffd700;
            padding-left: 12px;
        }

        .diamonds {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
            gap: 18px;
        }

        .card {
            background: rgba(255, 255, 255, 0.08);
            border: 2px solid transparent;
            border-radius: 15px;
            padding: 20px;
            text-align: center;
            cursor: pointer;
            transition: 0.3s;
        }

        .card:hover {
            transform: translateY(-5px);
            border-color: #4fc3f7;
        }

        .card.selected {
            border-color: #ffd700;
            background: rgba(255, 215, 0, 0.15);
        }

        .card .icon {
            font-size: 36px;
        }

        .card .amount {
            font-size: 20px;
            font-weight: bold;
            margin: 10px 0;
        }

        .card .price {
            color: #ffd700;
            font-size: 18px;
        }

        /* BUTTON */
        .btn {
            display: block;
            width: 100%;
            max-width: 400px;
            margin: 30px auto;
            padding: 16px;
            background: linear-gradient(90deg, #ffd700, #ffb300);
            color: #1a1a2e;
            border: none;
            border-radius: 12px;
            font-size: 18px;
            font-weight: bold;
            cursor: pointer;
            transition: 0.3s;
        }

        .btn:hover {
            opacity: 0.9;
            transform: scale(1.02);
        }

        /* MODAL */
        .modal {
            display: none;
            position: fixed;
            top: 0; left: 0;
            width: 100%; height: 100%;
            background: rgba(0, 0, 0, 0.7);
            justify-content: center;
            align-items: center;
            z-index: 200;
        }

        .modal-content {
            background: #16213e;
            padding: 30px;
            border-radius: 15px;
            max-width: 400px;
            text-align: center;
        }

        .modal-content h2 { color: #ffd700; margin-bottom: 15px; }
        .modal-content p { margin: 8px 0; }

        .close-btn {
            margin-top: 20px;
            padding: 10px 25px;
            background: #4fc3f7;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-weight: bold;
        }

        footer {
            text-align: center;
            padding: 25px;
            color: #b0bec5;
            margin-top: 40px;
        }
    </style>
</head>
<body>
    <header>
        <div class="logo">ML<span>Diamond</span></div>
        <nav>
            <a href="#">Башкы бет</a>
            <a href="#">Алмаз</a>
            <a href="#">Байланыш</a>
        </nav>
    </header>

    <section class="hero">
        <h1>Mobile Legends <span>Алмаз</span> сатып алуу</h1>
        <p>Тез, ишеничтүү жана арзан баада! 24/7 кызмат көрсөтөбүз.</p>
    </section>

    <div class="container">
        <!-- Маалыматтарды киргизүү формасы -->
        <div class="id-box">
            <input type="text" id="userId" placeholder="Колдонуучу ID (мисалы: 12345678)">
            <input type="text" id="serverId" placeholder="Сервер ID / Zone (мисалы: 2345)">
            <input type="text" id="userPhone" placeholder="Телефон номериңиз (мисалы: +996 555 112 233)">
        </div>

        <!-- Алмаздар -->
        <h2 class="section-title">Алмаз санын тандаңыз</h2>
        <div class="diamonds" id="diamondList"></div>

        <button class="btn" onclick="buy()">💳 Сатып алуу</button>
    </div>

    <!-- Modal -->
    <div class="modal" id="modal">
        <div class="modal-content">
            <h2>✅ Буйрутма кабыл алынды!</h2>
            <p>Биздин оператор жакында сиз менен байланышат.</p>
            <hr style="margin: 15px 0; border: 1px solid rgba(255,255,255,0.1);">
            <p id="mUser"></p>
            <p id="mServer"></p>
            <p id="mPhone"></p>
            <p id="mAmount"></p>
            <p id="mPrice"></p>
            <button class="close-btn" onclick="closeModal()">Жабуу</button>
        </div>
    </div>

    <footer>
        © 2026 ML Diamond Shop. Бардык укуктар корголгон.
    </footer>

    <script>
        // Алмаз пакеттери
        const packages = [
            { amount: 86,   price: 90 },
            { amount: 172,  price: 175 },
            { amount: 257,  price: 260 },
            { amount: 344,  price: 345 },
            { amount: 514,  price: 510 },
            { amount: 706,  price: 700 },
            { amount: 1412, price: 1380 },
            { amount: 2195, price: 2100 },
        ];

        let selected = null;
        const list = document.getElementById('diamondList');

        // Карталарды генерациялоо
        packages.forEach((p, i) => {
            const card = document.createElement('div');
            card.className = 'card';
            card.innerHTML = `
                <div class="icon">💎</div>
                <div class="amount">${p.amount} Diamond</div>
                <div class="price">${p.price} сом</div>
            `;
            card.onclick = () => selectCard(i, card);
            list.appendChild(card);
        });

        function selectCard(index, el) {
            document.querySelectorAll('.card').forEach(c => c.classList.remove('selected'));
            el.classList.add('selected');
            selected = packages[index];
        }

        function buy() {
            const userId = document.getElementById('userId').value.trim();
            const serverId = document.getElementById('serverId').value.trim();
            const userPhone = document.getElementById('userPhone').value.trim();

            if (!userId || !serverId || !userPhone) {
                alert('⚠️ Бардык талааларды (ID, Сервер жана Телефон номер) толтуруңуз!');
                return;
            }
            if (!selected) {
                alert('⚠️ Алмаз пакетин тандаңыз!');
                return;
            }

            // --- TELEGRAM БОТ ЖӨНӨТҮҮ СИСТЕМАСЫ ---
            const TELEGRAM_BOT_TOKEN = '8833600689:AAFksMqhmqq4AbJ9yWlGDt0vhJtfgahLF4s'; 
            
            // ⚠️ МУНУ ӨЗҮҢҮЗДҮН ЧАТ ID'ҢИЗГЕ АЛМАШТЫРЫҢЫЗ (Мисалы: 512345678)
            const TELEGRAM_CHAT_ID = 'БУЛ_ЖЕРГЕ_ӨЗҮҢҮЗДҮН_CHAT_ID_ЖАЗЫҢЫЗ'; 

            // Телефон номери кошулган жаңы билдирүү шаблону
            const message = `🔔 *ЖАҢЫ БУЙРУТМА!*\n\n👤 Колдонуучу ID: \`${userId}\`\n🌐 Сервер ID: \`${serverId}\`\n📞 Телефон: \`${userPhone}\`\n💎 Алмаз саны: *${selected.amount} Diamond*\n💰 Баасы: *${selected.price} сом*`;

            const url = `https://api.telegram.org/bot${TELEGRAM_BOT_TOKEN}/sendMessage`;

            fetch(url, {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({
                    chat_id: TELEGRAM_CHAT_ID,
                    text: message,
                    parse_mode: 'Markdown'
                })
            })
            .then(response => {
                if(response.ok) {
                    document.getElementById('mUser').textContent = 'Колдонуучу ID: ' + userId;
                    document.getElementById('mServer').textContent = 'Сервер: ' + serverId;
                    document.getElementById('mPhone').textContent = 'Телефон номер: ' + userPhone;
                    document.getElementById('mAmount').textContent = 'Алмаз: ' + selected.amount + ' 💎';
                    document.getElementById('mPrice').textContent = 'Баасы: ' + selected.price + ' сом';
                    document.getElementById('modal').style.display = 'flex';
                } else {
                    alert('⚠️ Ката кетти! Сиздин Chat ID туура эмес же ботту иштете элексиз.');
                }
            })
            .catch(error => {
                console.error('Ката:', error);
                alert('Байланыш катасы кетти.');
            });
        }

        function closeModal() {
            document.getElementById('modal').style.display = 'none';
            document.getElementById('userId').value = '';
            document.getElementById('serverId').value = '';
            document.getElementById('userPhone').value = '';
            document.querySelectorAll('.card').forEach(c => c.classList.remove('selected'));
            selected = null;
        }
    </script>
</body>
</html>
# -james_mlbb-
 'james_mlbb';html, ccs.js
