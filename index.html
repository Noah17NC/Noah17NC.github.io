<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gestion de Présence</title>
    <link rel="icon" href="../design/logo-pronote-menu.png" type="image/png">
    <link href="https://maxcdn.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Roboto', sans-serif;
            background-color: #f8f9fa;
        }
        .header, .footer {
            background-color: #007bff;
            color: white;
            padding: 10px 0;
            text-align: center;
        }
        table {
            width: 100%;
            margin: auto;
            border-collapse: collapse;
        }
        th, td {
            border: 1px solid #ddd;
            padding: 12px;
            text-align: center;
        }
        th {
            background-color: #0056b3;
            color: white;
        }
        .present {
            background-color: #d4edda !important;
        }
        .absent {
            background-color: #f8d7da !important;
        }
        #menu, #table-container {
            display: none;
        }
        #menu img {
            display: block;
            margin: 20px auto;
            max-width: 200px;
        }
        #groupSelect {
            margin-left: 20px;
        }
        .container {
            margin-top: 20px;
        }
        .text-center {
            text-align: center;
        }
        #barcodeInput {
            outline: none;
        }
    </style>
</head>
<body>
    <div class="header">
        <h1>Gestion de Présence</h1>
    </div>
    <div class="container">
        <div class="text-center mb-4">
            <input type="file" id="fileInput" accept=".xlsx, .xls" class="form-control-file">
        </div>
        
        <div id="menu" class="text-center">
            <img src="../design/logodulycée.jpg" alt="Logo" class="img-fluid mb-3">
            <h2>Sélectionnez une Classe</h2>
            <select id="classSelect" class="form-control d-inline-block w-auto mb-2">
                <option value="">-- Sélectionnez une classe --</option>
            </select>
            <button class="btn btn-primary" onclick="showClass()">Afficher la Classe</button>
        </div>

        <div id="table-container">
            <h3 id="classTitle" class="text-center mb-4"></h3>
            <table class="table table-bordered table-striped">
                <thead>
                    <tr>
                        <th>Nom</th>
                        <th>Code-Barres</th>
                        <th>Présence</th>
                    </tr>
                </thead>
                <tbody id="studentTable">
                </tbody>
            </table>
            <div class="text-center mb-4">
                <input type="text" id="barcodeInput" class="form-control w-auto d-inline-block" placeholder="Scannez le code-barres ici" tabindex="0" autofocus>
                <select id="groupSelect" class="form-control d-inline-block w-auto ml-2" onchange="updateTable();">
                    <option value="all">Tous les élèves</option>
                </select>
                <button class="btn btn-success ml-2" onclick="validerAppel()">Valider l'Appel</button>
                <button class="btn btn-secondary ml-2" onclick="showMenu()">Revenir au Menu</button>
            </div>
        </div>
    </div>
    <div class="footer">
        <p>&copy; 2024 Gestion de Présence</p>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.16.2/xlsx.full.min.js"></script>
    <script>
        let classes = {};
        let currentClass = null;
        let currentGroup = 'all';

        document.getElementById('fileInput').addEventListener('change', handleFile, false);

        function handleFile(event) {
            const file = event.target.files[0];
            const reader = new FileReader();
            
            reader.onload = function(event) {
                const data = new Uint8Array(event.target.result);
                const workbook = XLSX.read(data, {type: 'array'});
                processWorkbook(workbook);
            };
            
            reader.readAsArrayBuffer(file);
        }

        function processWorkbook(workbook) {
            const firstSheet = workbook.Sheets[workbook.SheetNames[0]];
            const jsonData = XLSX.utils.sheet_to_json(firstSheet, {header: 1});
            
            let currentClassName = null;
            let currentGroupName = null;

            jsonData.forEach(row => {
                if (row[0] && row[0].toLowerCase().startsWith('classe')) {
                    currentClassName = row[0];
                    classes[currentClassName] = {};
                } else if (row[0] && row[0].toLowerCase().startsWith('groupe')) {
                    currentGroupName = row[0];
                    classes[currentClassName][currentGroupName] = [];
                } else if (currentClassName && currentGroupName) {
                    classes[currentClassName][currentGroupName].push({
                        name: row[0],
                        id: row[1].toString().trim(), // Normaliser l'ID
                        present: false
                    });
                }
            });

            populateClassSelect();
            showMenu();
        }

        function populateClassSelect() {
            const classSelect = document.getElementById('classSelect');
            classSelect.innerHTML = '<option value="">-- Sélectionnez une classe --</option>';
            Object.keys(classes).forEach(className => {
                const option = document.createElement('option');
                option.value = className;
                option.textContent = className;
                classSelect.appendChild(option);
            });
        }

        function populateGroupSelect() {
            const groupSelect = document.getElementById('groupSelect');
            groupSelect.innerHTML = '<option value="all">Tous les élèves</option>';
            Object.keys(classes[currentClass]).forEach(groupName => {
                const option = document.createElement('option');
                option.value = groupName;
                option.textContent = groupName;
                groupSelect.appendChild(option);
            });
        }

        function showMenu() {
            document.getElementById('menu').style.display = 'block';
            document.getElementById('table-container').style.display = 'none';
        }

        function showClass() {
            const classSelect = document.getElementById('classSelect');
            const selectedClass = classSelect.value;

            if (selectedClass) {
                currentClass = selectedClass;
                document.getElementById('classTitle').textContent = selectedClass;
                populateGroupSelect();
                updateTable();
                document.getElementById('menu').style.display = 'none';
                document.getElementById('table-container').style.display = 'block';
                focusBarcodeInput(); // Focus sur le champ de code-barres
            }
        }

        function updateTable() {
            const studentTable = document.getElementById('studentTable');
            const groupSelect = document.getElementById('groupSelect');
            currentGroup = groupSelect.value;

            studentTable.innerHTML = '';
            const groups = classes[currentClass];
            const students = currentGroup === 'all'
                ? Object.values(groups).flat()
                : groups[currentGroup];
            
            students.forEach((student, index) => {
                const row = document.createElement('tr');
                row.classList.toggle('present', student.present);
                row.classList.toggle('absent', !student.present);
                row.innerHTML = `
                    <td>${student.name}</td>
                    <td>${student.id}</td>
                    <td><input type="checkbox" ${student.present ? 'checked' : ''} data-index="${index}" onchange="togglePresence(this)"></td>
                `;
                studentTable.appendChild(row);
            });

            focusBarcodeInput(); // Focus sur le champ de code-barres après la mise à jour de la table
        }

        function handleBarcodeScan(value) {
            const normalizedValue = value.trim(); // Normaliser le code-barres scanné
            const students = currentGroup === 'all'
                ? Object.values(classes[currentClass]).flat()
                : classes[currentClass][currentGroup];

            const student = students.find(s => s.id === normalizedValue); // Comparaison avec la valeur normalisée
            if (student) {
                student.present = true;
                updateTable();
            } else {
                alert('Élève non trouvé !');
            }
        }

        document.getElementById('barcodeInput').addEventListener('keypress', (event) => {
            if (event.key === 'Enter') {
                const barcodeValue = event.target.value;
                if (barcodeValue) {
                    handleBarcodeScan(barcodeValue);
                    event.target.value = ''; // Réinitialiser le champ après le scan
                }
            }
        });

        function togglePresence(checkbox) {
            const index = checkbox.dataset.index;
            const students = currentGroup === 'all'
                ? Object.values(classes[currentClass]).flat()
                : classes[currentClass][currentGroup];
            students[index].present = checkbox.checked;
            updateTable();
        }

        function validerAppel() {
            const students = currentGroup === 'all'
                ? Object.values(classes[currentClass]).flat()
                : classes[currentClass][currentGroup];
            const presentCount = students.filter(student => student.present).length;
            const absentCount = students.length - presentCount;
            alert(`Nombre d'élèves présents : ${presentCount}, absents : ${absentCount}`);
        }

        // Gérer le focus sur le champ de code-barres à chaque clic sur le document
        document.addEventListener('click', (event) => {
            if (event.target.tagName !== 'INPUT' && event.target.id !== 'groupSelect') {
                focusBarcodeInput(); // Rendre le champ de code-barres focus
            }
        });

        // Re-focus uniquement après que le groupe soit changé
        document.getElementById('groupSelect').addEventListener('change', focusBarcodeInput);

        function focusBarcodeInput() {
            const barcodeInput = document.getElementById('barcodeInput');
            barcodeInput.focus();
        }
    </script>
</body>
</html>
