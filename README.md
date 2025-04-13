# Agr-calculator-

<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Age Calculator - Muzamil</title>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@700&family=Roboto&display=swap');

    body {
      font-family: 'Roboto', sans-serif;
      background: linear-gradient(135deg, #2b5876, #4e4376);
      color: #fff;
      text-align: center;
      padding: 30px;
    }

    .header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin-bottom: 20px;
    }

    .header img {
      width: 50px;
      height: 50px;
      border-radius: 50%;
      border: 2px solid #0ff;
      box-shadow: 0 0 10px #0ff;
    }

    .header h1 {
      font-family: 'Orbitron', sans-serif;
      font-size: 32px;
      color: #0ff;
      text-shadow: 2px 2px 10px #0ff, 0 0 20px #00f;
      animation: pulse 2s infinite ease-in-out;
      flex-grow: 1;
      margin: 0 10px;
    }

    @keyframes pulse {
      0% { text-shadow: 2px 2px 10px #0ff, 0 0 20px #00f; }
      50% { text-shadow: 2px 2px 20px #0ff, 0 0 40px #0ff; }
      100% { text-shadow: 2px 2px 10px #0ff, 0 0 20px #00f; }
    }

    .container {
      max-width: 500px;
      margin: auto;
      background: rgba(255, 255, 255, 0.1);
      padding: 20px;
      border-radius: 20px;
      box-shadow: 0 0 20px #000;
    }

    label {
      display: block;
      margin: 15px 0 5px;
      font-size: 18px;
    }

    input {
      padding: 10px;
      border: none;
      border-radius: 8px;
      font-size: 16px;
      width: 100%;
    }

    button {
      margin-top: 20px;
      padding: 12px 25px;
      font-size: 18px;
      background: #00f2ff;
      color: #000;
      border: none;
      border-radius: 10px;
      cursor: pointer;
      transition: 0.3s;
    }

    button:hover {
      background: #0ff;
      box-shadow: 0 0 10px #0ff, 0 0 20px #0ff;
    }

    .result {
      margin-top: 25px;
      background: rgba(0, 0, 0, 0.4);
      padding: 15px;
      border-radius: 15px;
      box-shadow: 0 0 10px #0ff;
      font-size: 16px;
    }
  </style>
</head>
<body>

  <div class="header">
    <!-- Left Logo -->
    <img src="https://res.cloudinary.com/dxjkbpmgm/image/upload/v1744384921/IMG_20250411_202120_wx6x6n.png" alt="Left Logo">
    
    <!-- Title -->
    <h1>Muzamil's Age Calculator</h1>
    
    <!-- Right Logo -->
    <img src="https://res.cloudinary.com/dxjkbpmgm/image/upload/v1744384921/IMG_20250411_202120_wx6x6n.png" alt="Right Logo">
  </div>

  <div class="container">
    <label>Date of Birth:</label>
    <input type="date" id="dob">
    
    <label>Current Date:</label>
    <input type="date" id="currentDate">
    
    <button onclick="calculateAge()">Calculate</button>
    
    <div class="result" id="result"></div>
  </div>

  <script>
    function calculateAge() {
      const dob = new Date(document.getElementById("dob").value);
      const now = new Date(document.getElementById("currentDate").value);
      if (!dob || !now || isNaN(dob.getTime()) || isNaN(now.getTime())) {
        alert("Please enter both dates.");
        return;
      }

      let diff = now - dob;
      let ageDate = new Date(diff);
      let years = ageDate.getUTCFullYear() - 1970;
      let months = now.getMonth() - dob.getMonth() + (12 * (now.getFullYear() - dob.getFullYear()));
      if (now.getDate() < dob.getDate()) months--;

      let days = Math.floor(diff / (1000 * 60 * 60 * 24));
      let weeks = Math.floor(days / 7);
      let hours = Math.floor(diff / (1000 * 60 * 60));
      let minutes = Math.floor(diff / (1000 * 60));
      let seconds = Math.floor(diff / 1000);

      let extraMonths = months % 12;
      let extraDays = now.getDate() - dob.getDate();
      if (extraDays < 0) {
        let prevMonth = new Date(now.getFullYear(), now.getMonth(), 0);
        extraDays += prevMonth.getDate();
        extraMonths--;
      }

      document.getElementById("result").innerHTML = `
        <strong>Result:</strong><br><br>
        ${years} years ${extraMonths} months ${extraDays} days<br><br>
        or ${months} months ${extraDays} days<br>
        or ${weeks} weeks ${days % 7} days<br>
        or ${days} days<br>
        or ${hours} hours<br>
        or ${minutes} minutes<br>
        or ${seconds} seconds
      `;
    }
  </script>

</body>

