<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <title>نموذج تقرير المناوبة</title>
  <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600&display=swap" rel="stylesheet">
  <style>
    body {
      font-family: 'Cairo', sans-serif;
      background: #f4f6f9;
      color: #333;
      padding: 30px;
      max-width: 800px;
      margin: auto;
      border-radius: 10px;
      box-shadow: 0 0 20px rgba(0,0,0,0.1);
    }

    h2 {
      background: #004c97;
      color: white;
      padding: 15px;
      text-align: center;
      border-radius: 8px;
    }

    label {
      font-weight: bold;
      display: block;
      margin-top: 15px;
    }

    input, select, textarea {
      width: 100%;
      padding: 10px;
      margin-top: 5px;
      border: 1px solid #ccc;
      border-radius: 6px;
      font-family: 'Cairo', sans-serif;
    }

    textarea {
      resize: vertical;
    }

    .button {
      background-color: #007BFF;
      color: white;
      padding: 12px 25px;
      border: none;
      border-radius: 6px;
      font-size: 16px;
      cursor: pointer;
      margin-top: 20px;
    }

    .button:hover {
      background-color: #0056b3;
    }

    .add-button {
      background-color: #28a745;
      margin-top: 10px;
    }

    .add-button:hover {
      background-color: #218838;
    }
  </style>
</head>
<body>

  <h2>نموذج تقرير المناوبة</h2>

  <label>📅 التاريخ:</label>
  <input type="text" id="date" readonly>

  <label>🕒 الفترة:</label>
  <select id="shift">
    <option value="صباحية">صباحية</option>
    <option value="مسائية">مسائية</option>
  </select>

  <label>✅ عدد الفرق الأساسية:</label>
  <input type="number" id="mainTeams">

  <label>🔄 عدد فرق الأوفر لاب:</label>
  <input type="number" id="overlapTeams">

  <label>❌ عدد الفرق غير المتوفرة:</label>
  <input type="number" id="unavailableTeams">

  <label>📝 السبب:</label>
  <textarea id="unavailableReason" rows="2"></textarea>

  <label>🚨 بلاغات التدخل:</label>
  <div id="interventions">
    <input type="text" class="intervention" placeholder="اكتب بلاغ تدخل">
  </div>
  <button class="button add-button" onclick="addIntervention()">➕ إضافة بلاغ</button>

  <label>🚗 عدد المركبات العاملة:</label>
  <input type="number" id="activeVehicles">

  <label>🅿️ عدد مركبات الاحتياط:</label>
  <input type="number" id="reserveVehicles">

  <label>🛠️ عدد المركبات المتعطلة:</label>
  <input type="number" id="brokenVehicles">

  <label>📍 ملاحظات المركبات المتعطلة وموقعها:</label>
  <textarea id="brokenNotes" rows="2"></textarea>

  <label>🗒️ ملاحظات عامة:</label>
  <textarea id="generalNotes" rows="3"></textarea>

  <label>👤 اسم المناوب الأول:</label>
  <input type="text" id="staff1">

  <label>👤 اسم المناوب الثاني:</label>
  <input type="text" id="staff2">

  <button class="button" onclick="sendWhatsApp()">📤 إرسال عبر واتساب</button>

  <script>
    document.getElementById("date").value = new Date().toLocaleDateString('ar-EG');

    function addIntervention() {
      var div = document.createElement("div");
      div.innerHTML = '<input type="text" class="intervention" placeholder="اكتب بلاغ تدخل">';
      document.getElementById("interventions").appendChild(div);
    }

    function sendWhatsApp() {
      let text = "📋 تقرير المناوبة:\n";
      text += "📅 التاريخ: " + document.getElementById("date").value + "\n";
      text += "🕒 الفترة: " + document.getElementById("shift").value + "\n";
      text += "✅ عدد الفرق الأساسية: " + document.getElementById("mainTeams").value + "\n";
      text += "🔄 فرق الأوفر لاب: " + document.getElementById("overlapTeams").value + "\n";
      text += "❌ غير المتوفرة: " + document.getElementById("unavailableTeams").value + "\n";
      text += "📝 السبب: " + document.getElementById("unavailableReason").value + "\n";

      let interventions = document.querySelectorAll(".intervention");
      text += "🚨 بلاغات التدخل:\n";
      interventions.forEach((input, index) => {
        if (input.value.trim() !== "")
          text += (index + 1) + "- " + input.value + "\n";
      });

      text += "🚗 المركبات العاملة: " + document.getElementById("activeVehicles").value + "\n";
      text += "🅿️ الاحتياط: " + document.getElementById("reserveVehicles").value + "\n";
      text += "🛠️ المتعطلة: " + document.getElementById("brokenVehicles").value + "\n";
      text += "📍 ملاحظات الأعطال: " + document.getElementById("brokenNotes").value + "\n";
      text += "🗒️ ملاحظات عامة: " + document.getElementById("generalNotes").value + "\n";
      text += "👥 المناوبين:\n";
      text += "1- " + document.getElementById("staff1").value + "\n";
      text += "2- " + document.getElementById("staff2").value + "\n";

      var url = "https://wa.me/?text=" + encodeURIComponent(text);
      window.open(url, '_blank');
    }
  </script>

</body>
</html>
