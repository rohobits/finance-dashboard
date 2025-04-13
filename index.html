<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Financial Dashboard</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 20px;
      background-color: #f5f5f5;
    }
    h1, h2 {
      text-align: center;
    }
    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 20px;
    }
    th, td {
      border: 1px solid #ccc;
      padding: 8px;
      text-align: left;
    }
    th {
      background-color: #4CAF50;
      color: white;
    }
    .chart-container {
      width: 100%;
      margin: 40px 0;
    }
    .filter-container {
      text-align: center;
      margin-top: 20px;
    }
    select {
      padding: 5px;
      margin: 0 10px;
    }
  </style>
</head>
<body>
  <h1>📊 Financial Dashboard</h1>

  <div class="filter-container">
    <label for="account-filter">Filter by Account:</label>
    <select id="account-filter">
      <option value="All">All</option>
    </select>
  </div>

  <h2>Transactions</h2>
  <table id="transactions-table"></table>

  <h2>Balance History</h2>
  <table id="balance-table"></table>

  <div class="chart-container">
    <canvas id="balance-chart"></canvas>
  </div>

  <div class="chart-container">
    <canvas id="category-pie-chart"></canvas>
  </div>

  <h2>Goals</h2>
  <table id="goals-table">
    <tr><th>Account</th><th>Target</th><th>Current Balance</th><th>Progress</th></tr>
  </table>

  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <script>
    const apiKey = 'AIzaSyCOWwWf8oy-6PFuWJs68pxxzx_wvkyeSak';
    const sheetId = '1gXFatgQqNwVEn3aatV3tjfl3WxXCo5VgwlxPodLT6fs';

    const fetchSheetData = async (range) => {
      const url = `https://sheets.googleapis.com/v4/spreadsheets/${sheetId}/values/${range}?key=${apiKey}`;
      const response = await fetch(url);
      const data = await response.json();
      return data.values;
    };

    const renderTable = (data, elementId) => {
      const table = document.getElementById(elementId);
      if (!data || data.length === 0) {
        table.innerHTML = '<tr><td>No data available</td></tr>';
        return;
      }
      let html = '<tr>' + data[0].map(header => `<th>${header}</th>`).join('') + '</tr>';
      for (let i = 1; i < data.length; i++) {
        html += '<tr>' + data[i].map(cell => `<td>${cell}</td>`).join('') + '</tr>';
      }
      table.innerHTML = html;
    };

    const renderBalanceChart = (balanceData) => {
      const dates = balanceData.slice(1).map(row => row[0]);
      const balances = balanceData.slice(1).map(row => parseFloat(row[2]) || 0);
      new Chart(document.getElementById('balance-chart'), {
        type: 'line',
        data: {
          labels: dates,
          datasets: [{
            label: 'Balance Over Time',
            data: balances,
            borderColor: 'rgba(75, 192, 192, 1)',
            backgroundColor: 'rgba(75, 192, 192, 0.2)',
            fill: true,
            tension: 0.3
          }]
        },
        options: {
          responsive: true,
          scales: {
            y: {
              beginAtZero: false
            }
          }
        }
      });
    };

    const renderCategoryPieChart = (transactions) => {
      const categoryIndex = 6; // Column H (auto category)
      const outflowIndex = 4; // Column F (outflow)
      const dataMap = {};

      for (let i = 1; i < transactions.length; i++) {
        const category = transactions[i][categoryIndex] || 'Uncategorized';
        const amount = parseFloat(transactions[i][outflowIndex]) || 0;
        if (!dataMap[category]) dataMap[category] = 0;
        dataMap[category] += amount;
      }

      const labels = Object.keys(dataMap);
      const values = Object.values(dataMap);

      new Chart(document.getElementById('category-pie-chart'), {
        type: 'pie',
        data: {
          labels: labels,
          datasets: [{
            label: 'Spending by Category',
            data: values,
            backgroundColor: labels.map((_, i) => `hsl(${i * 35 % 360}, 70%, 60%)`)
          }]
        },
        options: {
          responsive: true,
        }
      });
    };

    const renderGoalsTable = (goals, balances) => {
      const table = document.getElementById('goals-table');
      let html = '';
      for (let i = 1; i < goals.length; i++) {
        const [account, target] = goals[i];
        const targetAmount = parseFloat(target);
        const latestBalance = balances.reverse().find(row => row[1] === account);
        const balanceAmount = latestBalance ? parseFloat(latestBalance[2]) : 0;
        const progress = ((balanceAmount / targetAmount) * 100).toFixed(1);
        html += `<tr><td>${account}</td><td>${target}</td><td>${balanceAmount}</td><td>${progress}%</td></tr>`;
      }
      table.innerHTML += html;
    };

    const loadDashboard = async () => {
      const transactions = await fetchSheetData('Transactions (BTS)!B1:I');
      renderTable(transactions, 'transactions-table');
      renderCategoryPieChart(transactions);

      const accounts = [...new Set(transactions.slice(1).map(row => row[7]))];
      const accountFilter = document.getElementById('account-filter');
      accounts.forEach(acc => {
        const option = document.createElement('option');
        option.value = acc;
        option.textContent = acc;
        accountFilter.appendChild(option);
      });
      accountFilter.addEventListener('change', () => {
        const filtered = accountFilter.value === 'All' ? transactions : [transactions[0], ...transactions.slice(1).filter(row => row[7] === accountFilter.value)];
        renderTable(filtered, 'transactions-table');
        renderCategoryPieChart(filtered);
      });

      const balanceHistory = await fetchSheetData('Balance History (BTS)!A1:D');
      renderTable(balanceHistory, 'balance-table');
      renderBalanceChart(balanceHistory);

      const goals = await fetchSheetData('Goals!A1:B');
      renderGoalsTable(goals, balanceHistory.slice(1));
    };

    loadDashboard();
  </script>
</body>
</html>
