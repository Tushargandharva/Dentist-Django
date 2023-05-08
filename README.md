<script>
<!DOCTYPE html>
<html>
  <head>
    <title>Dashboard</title>
    <style>
      body {
        margin: 0;
        padding: 0;
        background-color: #f8f8f8;
        font-family: sans-serif;
      }
      .container {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        align-items: center;
        padding: 20px;
      }
      .box {
        width: calc(33.33% - 20px);
        height: 100px;
        border-radius: 10px;
        background-color: white;
        margin: 10px;
        box-shadow: 0 0 5px rgba(0, 0, 0, 0.3);
        display: flex;
        justify-content: center;
        align-items: center;
        cursor: pointer;
        transition: all 0.2s ease-in-out;
      }
      .box:hover {
        transform: scale(1.05);
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
      }
      .box1 {
        background-color: #e74c3c;
      }
      .box2 {
        background-color: #3498db;
      }
      .box3 {
        background-color: #2ecc71;
      }
      .box p {
        font-size: 24px;
        font-weight: bold;
        color: white;
        text-align: center;
      }
      .table-container {
        margin-top: 20px;
        padding: 20px;
        background-color: white;
        border-radius: 10px;
        box-shadow: 0 0 5px rgba(0, 0, 0, 0.3);
      }
      table {
        border-collapse: collapse;
        width: 100%;
      }
      th, td {
        border: 1px solid #ccc;
        padding: 8px;
        text-align: left;
      }
      th {
        background-color: #f1f1f1;
        font-weight: bold;
      }
      .red {
        background-color: #e74c3c;
      }
      .green {
        background-color: #2ecc71;
      }
      .refresh {
        border: none;
        background-color: #3498db;
        color: white;
        padding: 10px;
        border-radius: 10px;
        font-size: 16px;
        cursor: pointer;
        transition: all 0.2s ease-in-out;
      }
      .refresh:hover {
        background-color: #2980b9;
      }
    </style>
  </head>
  <body>
    <div class="container">
      <div class="box box1">
        <p>Total Files</p>
        <p id="totalFiles"></p>
      </div>
      <div class="box box2">
        <p>Total Received Files</p>
        <p id="totalReceived"></p>
      </div>
      <div class="box box3">
        <p>Total Not Received Files</p>
        <p id="totalNotReceived"></p>
      </div>
      <br>
      <br>
      <input type="file" id="csvFile">
      <br>
      <br>
      <table id="data"></table>

    
	    
      const fileInput = document.getElementById("csvFile");
      const dataTable = document.getElementById("data");

      fileInput.addEventListener("change", () => {
        const file = fileInput.files[0];
        const reader = new FileReader();
        reader.readAsText(file);
        reader.onload = () => {
          const csv = reader.result;
          const rows = csv.split("\n");
          let header = true;
          let html = "";
          for (let row of rows) {
            if (header) {
              html += "<tr><th>" + row.split(",").join("</th><th>") + "</th></tr>";
              header = false;
            } else {
              const values = row.split(",");
              const name = values[0];
              const count = parseInt(values[1]);
              const statusClass = count < 3 ? "red" : "green";
              html += "<tr><td>" + name + "</td><td>" + count + "</td><td class='" + statusClass + "'></td></tr>";
            }
          }
          dataTable.innerHTML = html;
        };
      });
    </script>
  </body>
</html>
