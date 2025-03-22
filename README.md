<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>İmtahan Balı</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            text-align: center;
            padding: 20px;
            background: #f4f4f4;
        }
        .container {
            max-width: 500px;
            margin: auto;
            background: #fff;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
        }
        h2 {
            color: #333;
        }
        .form-group {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-top: 10px;
        }
        label {
            font-weight: bold;
            width: 50%;
            text-align: right;
            padding-right: 10px;
        }
        input {
            width: 40%;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
            text-align: center;
        }
        button {
            padding: 10px;
            width: 100%;
            background: #007bff;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            margin-top: 20px;
        }
        button:hover {
            background: #0056b3;
        }
        h3 {
            margin-top: 15px;
            color: #28a745;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>İmtahan Balı</h2>
        <div class="form-group"><label>Azərbaycan dili A (3 Sual):</label><input type="number" id="test1_acik" min="0" max="3"></div>
        <div class="form-group"><label>Azərbaycan dili Q (22 Sual):</label><input type="number" id="test1_kapali" min="0" max="22"></div>
        
        <div class="form-group"><label>Riyaziyyat A (3 Sual):</label><input type="number" id="test2_acik" min="0" max="3"></div>
        <div class="form-group"><label>Riyaziyyat Q (22 Sual):</label><input type="number" id="test2_kapali" min="0" max="22"></div>
        
        <div class="form-group"><label>Xarici dil A (3 Sual):</label><input type="number" id="test3_acik" min="0" max="3"></div>
        <div class="form-group"><label>Xarici dil Q (22 Sual):</label><input type="number" id="test3_kapali" min="0" max="22"></div>
        
        <div class="form-group"><label>Tarix (15 Sual):</label><input type="number" id="test4_kapali" min="0" max="15"></div>
        
        <div class="form-group"><label>Ədəbiyyat (15 Sual):</label><input type="number" id="test5_kapali" min="0" max="15"></div>
        
        <button onclick="hesaplaPuan()">HESABLA</button>
        <h3>Toplam Bal: <span id="sonuc">0</span></h3>
    </div>

    <script>
        function hesaplaPuan() {
            function hesaplaTest(a, k) {
                return (2 * a + k) * 175 / 28;
            }
            
            function hesaplaKucukTest(k) {
                return k * 87.5 / 15;
            }
            
            function duzeltKapaliDogru(k, d) {
                let yanlis = k - d;
                let duzeltilmisDogru = d - (yanlis / 3);
                return Math.max(duzeltilmisDogru, 0);
            }
            
            let test1_puan = hesaplaTest(parseInt(document.getElementById("test1_acik").value) || 0, duzeltKapaliDogru(22, parseInt(document.getElementById("test1_kapali").value) || 0));
            let test2_puan = hesaplaTest(parseInt(document.getElementById("test2_acik").value) || 0, duzeltKapaliDogru(22, parseInt(document.getElementById("test2_kapali").value) || 0));
            let test3_puan = hesaplaTest(parseInt(document.getElementById("test3_acik").value) || 0, duzeltKapaliDogru(22, parseInt(document.getElementById("test3_kapali").value) || 0));
            let test4_puan = hesaplaKucukTest(duzeltKapaliDogru(15, parseInt(document.getElementById("test4_kapali").value) || 0));
            let test5_puan = hesaplaKucukTest(duzeltKapaliDogru(15, parseInt(document.getElementById("test5_kapali").value) || 0));
            
            let toplamPuan = test1_puan + test2_puan + test3_puan + test4_puan + test5_puan;
            toplamPuan = Math.min(toplamPuan, 700); // Maksimum puan sınırı ekledim
            
            document.getElementById("sonuc").textContent = toplamPuan.toFixed(2);
        }
    </script>
</body>
</html>
