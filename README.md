<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Raeanne’s Cash Vixen Vault</title>
    <style>
        body {
            font-family: 'Poppins', Arial, sans-serif; /* Sleek, sexy font */
            margin: 0;
            padding: 10px;
            background: linear-gradient(135deg, #2d0047, #ff3399, #66ffcc); /* Deep purple to hot pink to teal */
            color: #fff;
            max-width: 375px;
            margin-left: auto;
            margin-right: auto;
            overflow-x: hidden;
            box-sizing: border-box;
            animation: bgGlow 8s infinite alternate;
        }
        h1 {
            font-size: 2em;
            text-align: center;
            color: #ff3399; /* Hot pink */
            text-shadow: 0 0 8px #66ffcc, 0 0 15px #ff66b3;
            margin: 10px 0;
            font-weight: 600;
            animation: titlePulse 2s infinite;
        }
        #current-date {
            text-align: center;
            font-size: 1em;
            color: #e6e6e6; /* Soft white */
            margin-bottom: 15px;
            text-shadow: 0 0 3px #000;
            font-weight: 400;
        }
        .container {
            display: flex;
            flex-direction: column;
            gap: 10px;
            width: 100%;
        }
        .card {
            background: rgba(0, 0, 0, 0.7);
            padding: 12px;
            border-radius: 10px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.4), inset 0 0 5px #ff3399;
            text-align: center;
            transition: transform 0.2s, box-shadow 0.2s;
            cursor: pointer;
            width: 100%;
            box-sizing: border-box;
        }
        .card:hover {
            transform: scale(1.03);
            box-shadow: 0 6px 16px rgba(0,0,0,0.5), inset 0 0 10px #66ffcc;
        }
        .card h3 {
            font-size: 1.3em;
            margin: 0;
            color: #fff;
            text-shadow: 0 0 5px #000;
            font-weight: 500;
        }
        .card p {
            font-size: 0.9em;
            margin: 4px 0;
            color: #f0f0f0; /* Light gray for readability */
            text-shadow: 0 0 3px #000;
        }
        .card.urgent {
            border: 3px solid #ff3399; /* Neon pink */
            padding: 14px;
            transform: scale(1.05);
            background: rgba(50, 0, 50, 0.8);
            box-shadow: 0 0 15px #ff3399, 0 0 25px #66ffcc, inset 0 0 8px #ff3399;
            animation: urgentPulse 0.7s infinite;
        }
        .card.near-due {
            border: 2px solid #66ffcc; /* Neon teal */
            padding: 13px;
            transform: scale(1.02);
            box-shadow: 0 0 10px #66ffcc, inset 0 0 5px #66ffcc;
            animation: nearGlow 1.2s infinite;
        }
        .card.small {
            padding: 10px;
            font-size: 0.8em;
        }
        .card.small h3 { font-size: 1.1em; }
        .card.completed {
            background: linear-gradient(135deg, #ffcc33, #ff9933); /* Gold to coral */
            border: 3px solid #ffcc33;
            box-shadow: 0 0 15px #ffcc33, inset 0 0 8px #ffcc33;
            animation: victoryGlow 1.5s infinite;
        }
        .card.completed h3::after {
            content: " 💋 SLAYED";
            color: #fff;
            font-size: 0.8em;
            text-shadow: 0 0 4px #000;
        }
        .section {
            margin: 15px 0;
            background: rgba(0, 0, 0, 0.65);
            padding: 12px;
            border-radius: 10px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.4), inset 0 0 5px #66ffcc;
            width: 100%;
            box-sizing: border-box;
            animation: fadeIn 0.8s ease-in;
        }
        .section h2 {
            font-size: 1.5em;
            color: #ff3399;
            text-align: center;
            margin: 8px 0;
            text-shadow: 0 0 6px #000;
            font-weight: 600;
        }
        canvas {
            max-width: 100%;
            margin: 10px 0;
            border: 1px solid #ff3399;
            border-radius: 5px;
            cursor: pointer;
        }
        .chart-popout {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 340px;
            padding: 12px;
            background: rgba(0, 0, 0, 0.9);
            border: 3px solid #ffcc33;
            box-shadow: 0 0 25px #ff3399;
            z-index: 1000;
            border-radius: 10px;
        }
        .chart-popout canvas {
            max-width: 100%;
        }
        .chart-popout h2 {
            font-size: 1.6em;
            margin-bottom: 8px;
        }
        .progress-bar {
            width: 100%;
            margin: 10px 0;
            background: rgba(255, 255, 255, 0.15);
            border-radius: 6px;
            overflow: hidden;
            box-shadow: 0 0 6px #ff3399;
        }
        .progress {
            height: 16px;
            text-align: center;
            color: #fff;
            font-size: 0.8em;
            transition: width 1s ease-in-out;
            text-shadow: 0 0 3px #000;
        }
        .progress.success { background: #ffcc33; }
        .progress.warning { background: #ff4500; }
        .sobriety-section {
            background: linear-gradient(135deg, #ffcc33, #ff9933);
            padding: 12px;
            border-radius: 10px;
            box-shadow: 0 0 15px #ffcc33, inset 0 0 8px #66ffcc;
            width: 100%;
            box-sizing: border-box;
        }
        .sobriety-section h2 {
            font-size: 1.6em;
            text-shadow: 0 0 6px #000;
        }
        .sobriety-section p {
            font-size: 0.9em;
            margin: 5px 0;
        }
        .checklist {
            margin-top: 10px;
            text-align: left;
            font-size: 0.9em;
            color: #f0f0f0;
        }
        .checklist-item {
            display: flex;
            align-items: center;
            margin: 4px 0;
        }
        .checklist-item input {
            margin-right: 6px;
        }
        @keyframes bgGlow {
            0% { background-position: 0% 0%; }
            100% { background-position: 100% 100%; }
        }
        @keyframes titlePulse {
            0% { text-shadow: 0 0 8px #66ffcc, 0 0 15px #ff66b3; }
            50% { text-shadow: 0 0 12px #66ffcc, 0 0 20px #ff66b3; }
            100% { text-shadow: 0 0 8px #66ffcc, 0 0 15px #ff66b3; }
        }
        @keyframes urgentPulse {
            0% { box-shadow: 0 0 10px #ff3399, 0 0 20px #66ffcc, inset 0 0 8px #ff3399; }
            50% { box-shadow: 0 0 20px #ff3399, 0 0 30px #66ffcc, inset 0 0 12px #ff3399; }
            100% { box-shadow: 0 0 10px #ff3399, 0 0 20px #66ffcc, inset 0 0 8px #ff3399; }
        }
        @keyframes nearGlow {
            0% { box-shadow: 0 0 8px #66ffcc, inset 0 0 5px #66ffcc; }
            50% { box-shadow: 0 0 15px #66ffcc, inset 0 0 8px #66ffcc; }
            100% { box-shadow: 0 0 8px #66ffcc, inset 0 0 5px #66ffcc; }
        }
        @keyframes victoryGlow {
            0% { box-shadow: 0 0 10px #ffcc33, inset 0 0 8px #ffcc33; }
            50% { box-shadow: 0 0 20px #ffcc33, inset 0 0 12px #ffcc33; }
            100% { box-shadow: 0 0 10px #ffcc33, inset 0 0 8px #ffcc33; }
        }
        @keyframes fadeIn {
            0% { opacity: 0; transform: translateY(10px); }
            100% { opacity: 1; transform: translateY(0); }
        }
    </style>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600&display=swap" rel="stylesheet">
</head>
<body>
    <h1>Raeanne’s Cash Vixen Vault</h1>
    <div id="current-date">Loading date...</div>
    <div class="container" id="bill-container"></div>

    <div class="section">
        <h2>💸 Cash Flow 💸</h2>
        <p>Income: $<span id="total-income">0</span></p>
        <p>Expenses: $<span id="total-expenses">0</span></p>
        <p>Net: $<span id="net-cash-flow">0</span></p>
        <canvas id="incomeExpenseChart"></canvas>
        <div class="checklist" id="bill-checklist"></div>
    </div>

    <div class="section">
        <h2>🍷 Spending Breakdown 🍷</h2>
        <canvas id="expensePieChart"></canvas>
    </div>

    <div class="section">
        <h2>✨ Goals ✨</h2>
        <p>Savings: $<span id="savings">5000</span> / $10,000</p>
        <div class="progress-bar"><div class="progress" id="savings-progress"></div></div>
        <p>Car Loan: $<span id="car-owed">1000</span> / $0</p>
        <div class="progress-bar"><div class="progress" id="car-progress"></div></div>
        <canvas id="goalsChart"></canvas>
    </div>

    <div class="section sobriety-section">
        <h2>🏔️ Colorado Countdown 🏔️</h2>
        <p>April 3: <span id="colorado-april">0</span> days</p>
        <p>June 25: <span id="colorado-june">0</span> days</p>
        <canvas id="tripsChart"></canvas>
    </div>

    <div class="section">
        <h2>💰 Tip Hustle 💰</h2>
        <p>Last Month: $<span id="last-month-tips">0</span></p>
        <p>This Month: $<span id="this-month-tips">0</span></p>
        <canvas id="tipsChart"></canvas>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <script>
        // Current date
        const today = new Date();
        document.getElementById('current-date').textContent = `Today: ${today.toDateString()}`;

        // Bill data
        const bills = [
            { name: "Car Payment", dueDay: 1, amount: 100, completed: false },
            { name: "Car Insurance", dueDay: 15, amount: 220, completed: false },
            { name: "Cellphone", dueDay: 20, amount: 115, completed: false },
            { name: "Gas", dueDay: 10, amount: 80, completed: false },
            { name: "Nails (Biweekly)", dueDay: 14, amount: 60, completed: false },
            { name: "Nails (Biweekly)", dueDay: 28, amount: 60, completed: false },
            { name: "Groceries (Biweekly)", dueDay: 1, amount: 150, completed: false },
            { name: "Groceries (Biweekly)", dueDay: 15, amount: 150, completed: false },
            { name: "Alcohol ($100/wk)", dueDay: 10, amount: 400, completed: false } // Monthly total
        ];

        // Income data
        const weeklyChecks = 400;
        const monthlyChecks = weeklyChecks * 4; // $1,600/month
        const tipData = {
            May: 2840,
            June: 6920,
            July: 4232,
            August: 2281,
            September: 5436,
            October: 5436,
            November: 4513,
            December: 3691,
            January: 3730,
            February: 3528,
            March: 853
        };
        const monthlyTipsAvg = Object.values(tipData).reduce((sum, val) => sum + val, 0) / 10;
        const monthlyIncome = monthlyChecks + monthlyTipsAvg;

        // Financial data
        const savings = 5000;
        const savingsGoal = 10000;
        const carOwed = 1000;

        // Days until due
        function daysUntilDue(dueDay) {
            const currentDay = today.getDate();
            const currentMonth = today.getMonth();
            const currentYear = today.getFullYear();
            let dueDate = new Date(currentYear, currentMonth, dueDay);
            if (currentDay > dueDay) dueDate.setMonth(currentMonth + 1);
            const diffTime = dueDate - today;
            return Math.ceil(diffTime / (1000 * 60 * 60 * 24));
        }

        // Sort bills by days until due
        bills.sort((a, b) => daysUntilDue(a.dueDay) - daysUntilDue(b.dueDay));

        // Render bills with interactivity
        const billContainer = document.getElementById('bill-container');
        bills.forEach(bill => {
            const daysLeft = daysUntilDue(bill.dueDay);
            const billDiv = document.createElement('div');
            billDiv.classList.add('card');
            if (daysLeft <= 3 && daysLeft >= 0) billDiv.classList.add('urgent');
            else if (daysLeft <= 7) billDiv.classList.add('near-due');
            if (bill.amount < 100 && daysLeft > 7) billDiv.classList.add('small');
            if (bill.completed) billDiv.classList.add('completed');
            billDiv.innerHTML = `
                <h3>${bill.name}</h3>
                <p>$${bill.amount}</p>
                <p>Due in ${daysLeft >= 0 ? daysLeft : "Overdue by " + Math.abs(daysLeft)} days</p>
            `;
            billDiv.addEventListener('click', () => {
                if (!billDiv.classList.contains('completed')) {
                    billDiv.classList.add('completed');
                    bill.completed = true;
                    updateChecklist();
                }
            });
            billContainer.appendChild(billDiv);
        });

        // Bill checklist
        function updateChecklist() {
            const checklist = document.getElementById('bill-checklist');
            checklist.innerHTML = '<h3>BILL SLAY LIST</h3>';
            bills.forEach(bill => {
                const item = document.createElement('div');
                item.classList.add('checklist-item');
                item.innerHTML = `
                    <input type="checkbox" ${bill.completed ? 'checked' : ''} disabled>
                    ${bill.name} - $${bill.amount}
                `;
                checklist.appendChild(item);
            });
        }
        updateChecklist();

        // Summary
        const totalExpenses = bills.reduce((sum, bill) => sum + bill.amount, 0);
        const netCashFlow = monthlyIncome - totalExpenses;
        document.getElementById('total-income').textContent = monthlyIncome.toFixed(2);
        document.getElementById('total-expenses').textContent = totalExpenses.toFixed(2);
        document.getElementById('net-cash-flow').textContent = netCashFlow.toFixed(2);

        // Goals Progress
        const savingsProgress = (savings / savingsGoal) * 100;
        const carProgress = ((carOwed - 1000) / carOwed) * 100; // Assuming original loan higher
        const monthsToApril = Math.ceil((new Date("2025-04-30") - today) / (1000 * 60 * 60 * 24 * 30));
        const savingsTargetMonthly = (savingsGoal - savings) / monthsToApril;

        document.getElementById('savings').textContent = savings.toFixed(2);
        document.getElementById('savings-progress').style.width = `${savingsProgress}%`;
        document.getElementById('savings-progress').textContent = `${savingsProgress.toFixed(1)}% ($${savingsTargetMonthly.toFixed(2)}/mo)`;
        document.getElementById('savings-progress').classList.add('success');

        document.getElementById('car-owed').textContent = carOwed.toFixed(2);
        document.getElementById('car-progress').style.width = `${100 - carProgress}%`;
        document.getElementById('car-progress').textContent = `${(100 - carProgress).toFixed(1)}% ($100/mo)`;
        document.getElementById('car-progress').classList.add('warning');

        // Colorado Trips Countdown
        const aprilTrip = new Date("2025-04-03");
        const juneTrip = new Date("2025-06-25");
        const daysToApril = Math.ceil((aprilTrip - today) / (1000 * 60 * 60 * 24));
        const daysToJune = Math.ceil((juneTrip - today) / (1000 * 60 * 60 * 24));
        document.getElementById('colorado-april').textContent = daysToApril;
        document.getElementById('colorado-june').textContent = daysToJune;

        // Tip Hustle
        const lastMonthTips = tipData[Object.keys(tipData)[Object.keys(tipData).length - 2]] || 0;
        const thisMonthTips = tipData[Object.keys(tipData)[Object.keys(tipData).length - 1]] || 0;
        document.getElementById('last-month-tips').textContent = lastMonthTips.toFixed(2);
        document.getElementById('this-month-tips').textContent = thisMonthTips.toFixed(2);

        // Charts
        const charts = [
            { id: 'incomeExpenseChart', title: 'Cash Flow', data: { labels: ['Income', 'Expenses'], datasets: [{ label: 'Monthly ($)', data: [monthlyIncome, totalExpenses], backgroundColor: ['#66ffcc', '#ff3399'], borderWidth: 1 }] }, type: 'bar' },
            { id: 'expensePieChart', title: 'Spending Breakdown', data: { labels: bills.map(b => b.name), datasets: [{ data: bills.map(b => b.amount), backgroundColor: ['#66ffcc', '#ff3399', '#ffcc33', '#ffd700', '#ff4500', '#2d0047', '#ff9933', '#ff8c00', '#e0e0e0'], borderWidth: 1 }] }, type: 'pie' },
            { id: 'goalsChart', title: 'Goals', data: { labels: ['Savings', 'Car Loan'], datasets: [{ label: 'Current ($)', data: [savings, carOwed], backgroundColor: ['#66ffcc', '#ff3399'], borderWidth: 1 }, { label: 'Target ($)', data: [savingsGoal, 0], backgroundColor: ['#33cc99', '#d63031'], borderWidth: 1 }] }, type: 'bar' },
            { id: 'tripsChart', title: 'Colorado Countdown', data: { labels: ['April 3', 'June 25'], datasets: [{ label: 'Days Left', data: [daysToApril, daysToJune], backgroundColor: ['#ffcc33', '#ff9933'], borderWidth: 1 }] }, type: 'bar' },
            { id: 'tipsChart', title: 'Tip Hustle', data: { labels: Object.keys(tipData), datasets: [{ label: 'Tips ($)', data: Object.values(tipData), borderColor: '#fff', backgroundColor: 'rgba(255, 255, 255, 0.3)', fill: true, tension: 0.3 }] }, type: 'line' }
        ];

        charts.forEach(chart => {
            const canvas = document.getElementById(chart.id);
            const ctx = canvas.getContext('2d');
            const chartInstance = new Chart(ctx, {
                type: chart.type,
                data: chart.data,
                options: { scales: chart.type === 'bar' || chart.type === 'line' ? { y: { beginAtZero: true } } : {} }
            });

            canvas.addEventListener('click', () => {
                const existingPopout = document.querySelector('.chart-popout');
                if (existingPopout) existingPopout.remove();

                const popout = document.createElement('div');
                popout.classList.add('chart-popout');
                popout.innerHTML = `<h2>${chart.title}</h2><canvas id="popout-${chart.id}"></canvas>`;
                document.body.appendChild(popout);

                const popoutCanvas = document.getElementById(`popout-${chart.id}`);
                const popoutCtx = popoutCanvas.getContext('2d');
                new Chart(popoutCtx, {
                    type: chart.type,
                    data: chart.data,
                    options: {
                        scales: chart.type === 'bar' || chart.type === 'line' ? { y: { beginAtZero: true } } : {},
                        plugins: { legend: { labels: { font: { size: 16 } } } },
                        animation: { duration: 1000, easing: 'easeInOutBounce' }
                    }
                });

                popout.addEventListener('click', () => popout.remove());
            });
        });
    </script>
</body>
</html>
