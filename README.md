<!DOCTYPE html>
<html lang="pt">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lista de Convidados - CCM</title>
    <style>
        * {
            box-sizing: border-box;
        }

        body {
            font-family: Arial, sans-serif;
            max-width: 800px;
            margin: 20px auto;
            padding: 0 15px;
            background-color: #0d0f12;
            color: #e0e0e0;
        }

        .header-container {
            text-align: center;
            padding: 15px 0;
            border-bottom: 3px solid;
            border-image: linear-gradient(to right, #1e88e5, #e53935) 1;
            margin-bottom: 15px;
        }

        .site-logo {
            max-width: 220px;
            height: auto;
            display: block;
            margin: 0 auto 15px auto;
            filter: drop-shadow(0 0 8px rgba(30, 136, 229, 0.4));
            transition: transform 0.3s ease;
        }

        .site-logo:hover {
            transform: scale(1.03);
        }

        h1 {
            text-align: center;
            margin: 0 0 5px 0;
            color: #ff3333;
            text-shadow: 0 0 10px rgba(255, 51, 51, 0.4);
            font-size: 32px;
            letter-spacing: 1.5px;
        }

        h3 {
            text-align: center;
            margin: 0 0 10px 0;
            color: #4fc3f7;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .guest-counter {
            display: inline-block;
            text-align: center;
            font-size: 14px;
            color: #ffffff;
            background: #1565c0;
            padding: 6px 16px;
            border-radius: 20px;
            font-weight: bold;
            border: 1px solid #ff3333;
            box-shadow: 0 0 8px rgba(255, 51, 51, 0.3);
        }

        .counter-wrapper {
            text-align: center;
            margin-bottom: 10px;
        }

        .search-box {
            position: sticky;
            top: 10px;
            z-index: 1000;
            margin: 15px 0 20px 0;
            text-align: center;
            background-color: rgba(13, 15, 18, 0.95);
            padding: 10px;
            border-radius: 10px;
            backdrop-filter: blur(5px);
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 8px;
        }

        .search-container {
            position: relative;
            width: 100%;
            max-width: 500px;
        }

        .search-box input {
            width: 100%;
            padding: 12px 35px 12px 15px;
            font-size: 16px;
            background-color: #161b22;
            border: 2px solid #1e88e5;
            border-radius: 8px;
            outline: none;
            transition: border-color 0.3s, box-shadow 0.3s;
            color: #ffffff;
            box-shadow: 0 4px 10px rgba(30, 136, 229, 0.2);
        }

        .search-box input:focus {
            border-color: #ff3333;
            box-shadow: 0 0 12px rgba(255, 51, 51, 0.5);
        }

        .clear-search {
            position: absolute;
            right: 12px;
            top: 50%;
            transform: translateY(-50%);
            background: none;
            border: none;
            font-size: 16px;
            color: #ff5252;
            cursor: pointer;
            display: none;
            padding: 4px;
            font-weight: bold;
        }

        .table-responsive {
            width: 100%;
            overflow-x: auto;
            -webkit-overflow-scrolling: touch;
            border-radius: 8px;
            box-shadow: 0 6px 15px rgba(0,0,0,0.7);
            border: 2px solid #1e88e5;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            background-color: #161b22;
            overflow: hidden;
        }

        th, td {
            padding: 12px 15px;
            text-align: left;
            border-bottom: 1px solid #263238;
        }

        th {
            background-color: #0d47a1;
            color: #ffffff;
            text-transform: uppercase;
            font-size: 14px;
            letter-spacing: 0.8px;
            border-bottom: 3px solid #ff3333;
        }

        tbody tr {
            background-color: #161b22;
            transition: background-color 0.2s, opacity 0.2s;
        }

        tbody tr:hover {
            background-color: #1c2536;
        }

        td.guest-name {
            outline: none;
            border-radius: 4px;
            transition: background-color 0.2s;
        }

        td.guest-name:focus {
            background-color: #0d2a4a;
            box-shadow: inset 0 0 0 2px #4fc3f7;
        }

        tbody tr.checked {
            background-color: #0a192f;
            color: #64b5f6;
        }

        tbody tr.checked td.guest-name {
            text-decoration: line-through;
            color: #90caf9;
        }

        .checkbox-col {
            width: 44px;
            text-align: center;
        }

        .checkbox-col input[type="checkbox"] {
            width: 20px;
            height: 20px;
            cursor: pointer;
            accent-color: #ff3333;
        }

        .footer-controls {
            text-align: center;
            margin-top: 20px;
            margin-bottom: 30px;
        }

        .btn-reset {
            background: none;
            border: 2px solid #ff3333;
            color: #ff5252;
            padding: 8px 16px;
            font-size: 13px;
            font-weight: bold;
            border-radius: 6px;
            cursor: pointer;
            opacity: 0.9;
            transition: all 0.3s ease;
        }

        .btn-reset:hover {
            opacity: 1;
            background-color: #ff3333;
            color: #ffffff;
            box-shadow: 0 0 10px rgba(255, 51, 51, 0.5);
        }

        @media (max-width: 600px) {
            body {
                margin: 10px auto;
                padding: 0 10px;
            }

            .site-logo {
                max-width: 160px;
            }

            h1 {
                font-size: 26px;
            }

            h3 {
                font-size: 15px;
            }

            th, td {
                padding: 10px 10px;
                font-size: 14px;
            }

            .search-box {
                top: 5px;
                padding: 8px 0;
            }

            .search-box input {
                font-size: 15px;
                padding: 10px 30px 10px 12px;
            }

            .checkbox-col {
                width: 36px;
            }
        }
    </style>
</head>
<body>

    <div class="header-container">
        <h2>CCM</h2>     
        <h3>Lista de Convidados</h3>
        <div class="counter-wrapper">
            <div class="guest-counter" id="guestCounter">Chegaram: 0 / Total: 0</div>
        </div>
    </div>

    <div class="search-box">
        <div class="search-container">
            <input type="text" id="searchInput" onkeyup="filterGuests()" placeholder="Pesquise pelo nome..." autocomplete="off" autocorrect="off">
            <button class="clear-search" id="clearSearchBtn" onclick="clearSearch()" title="Limpar pesquisa">✕</button>
        </div>
    </div>

    <div class="table-responsive">
        <table id="guestTable">
            <thead>
                <tr>
                    <th class="checkbox-col">✓</th>
                    <th>Nome do Convidado (clique para editar)</th>
                </tr>
            </thead>
            <tbody>
                <!-- Parte 1 -->
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Padre</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Catequista x 2</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Liomar e Sandra</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Emília e Ângela</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Maria A. e Angélica</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Lucília e Vitória</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Nhongo e esposa</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Madrinhos da Sónia</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Bispa Suzete e Irmã Helene</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Evangelina e Aurélia</td></tr>

                <!-- Parte 2 -->
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Vovó Carolina e Combilina</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Luísa e Elvira</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Guambe e Chirime</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Issufo - Laulinda e esposo</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Bernadete e Liojino</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Dias e Emília</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Beatriz e Jorge</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Celestina e Gracianda</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">José Taimo e esposa</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Maria e Alguíseco</td></tr>

                <!-- Parte 3 -->
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Pastor Eduardo e esposa</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Isabel e Pércia</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Toté e esposa Michag</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Lito e esposa</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Mito e esposa</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Esposa - Timóteo</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Filho e esposa Filomena</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Esposa - Elias</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Esposo - Gracinda</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Esposo - Guida</td></tr>

                <!-- Parte 4 -->
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Isabel e Fátima - 87154744</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Claudina e esposo</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Graziela e esposo</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Bernardo e esposa</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Zaida e esposo</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Fernando e esposa</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Aurora e Rosário</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Rosália Mutho e Vitónio</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Elisa e Liomar</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Lina madrinha</td></tr>

                <!-- Parte 5 -->
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Nguma e esposa</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Sónia e esposo</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Mãe e esposo</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Totá e esposa</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">BiDy e esposa</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Paulo e esposa</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Nana e esposa</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">... e esposo - Jeivitual</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Rossima e filha</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">DonVila</td></tr>

                <!-- Parte 6 -->
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Wilbramo e esposa</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Xibisso e esposa</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Vanito e esposa</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Candrinho e Goinho</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Felismina / Felismata Maria do Carmo</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Diácono e marido JI</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Sasá e esposa</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Fofito e esposa</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Lili e esposo</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Adélia e esposo</td></tr>

                <!-- Parte 7 -->
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Langa e esposa</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">João e Vandamo</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Nelinho e esposa</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Fráscoa e esposo</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Nelito e loque</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Mozalinda e Martindha</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Castigo e esposa</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Ti Jaime e esposa</td></tr>
            </tbody>
        </table>
    </div>

    <div class="footer-controls">
        <button class="btn-reset" onclick="resetList()">Limpar Todos os Cheques</button>
    </div>

    <script>
        function updateCounter() {
            const rows = document.querySelectorAll('#guestTable tbody tr');
            const checkedRows = document.querySelectorAll('#guestTable tbody tr.checked');
            const counterEl = document.getElementById('guestCounter');
            counterEl.textContent = `Chegaram: ${checkedRows.length} / Total: ${rows.length}`;
        }

        function toggleCheck(checkbox) {
            const row = checkbox.closest('tr');
            if (checkbox.checked) {
                row.classList.add('checked');
            } else {
                row.classList.remove('checked');
            }
            updateCounter();
            saveState();
        }

        function filterGuests() {
            const input = document.getElementById('searchInput');
            const filter = input.value.toLowerCase();
            const clearBtn = document.getElementById('clearSearchBtn');
            const table = document.getElementById('guestTable');
            const rows = table.getElementsByTagName('tr');

            clearBtn.style.display = filter.length > 0 ? 'block' : 'none';

            for (let i = 1; i < rows.length; i++) { // Começa em 1 para pular o cabeçalho (thead)
                const row = rows[i];
                const nameTd = row.querySelector('.guest-name');
                if (nameTd) {
                    const nameText = nameTd.textContent.toLowerCase();
                    if (nameText.includes(filter)) {
                        row.style.display = '';
                    } else {
                        row.style.display = 'none';
                    }
                }
            }
        }

        function clearSearch() {
            const input = document.getElementById('searchInput');
            input.value = '';
            filterGuests();
            input.focus();
        }

        function handleEnter(event) {
            if (event.key === 'Enter') {
                event.preventDefault();
                event.target.blur();
            }
        }

        function saveState() {
            updateCounter();
        }

        function resetList() {
            if (confirm('Deseja realmente limpar todas as marcações de presença?')) {
                const checkboxes = document.querySelectorAll('#guestTable input[type="checkbox"]');
                checkboxes.forEach(cb => {
                    cb.checked = false;
                    cb.closest('tr').classList.remove('checked');
                });
                updateCounter();
                saveState();
            }
        }

        document.addEventListener('DOMContentLoaded', () => {
            updateCounter();
        });
    </script>
</body>
</html>
