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

        tr.table-divider {
            background: linear-gradient(90deg, #3e0a0a 0%, #161b22 100%) !important;
        }

        tr.table-divider td {
            font-weight: bold;
            color: #ff5252;
            text-transform: uppercase;
            letter-spacing: 1px;
            font-size: 13px;
            border-top: 2px solid #d32f2f;
            border-bottom: 2px solid #d32f2f;
            padding: 10px 15px;
            text-shadow: 0 0 5px rgba(255, 82, 82, 0.3);
        }

        .no-result {
            display: none;
            text-align: center;
            padding: 20px;
            color: #ff8a80;
            font-style: italic;
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
        <img src="logo_CCM_responsivo (1).png" alt="Logo CCM" class="site-logo">
        <h3>Lista de Convidados</h3>
        <div class="counter-wrapper">
            <div class="guest-counter" id="guestCounter">Chegaram: 0 / Total: 0</div>
        </div>
    </div>

    <div class="search-box">
        <div class="search-container">
            <input type="text" id="searchInput" onkeyup="filterGuests()" placeholder="Pesquise pelo nome ou mesa..." autocomplete="off" autocorrect="off">
            <button class="clear-search" id="clearSearchBtn" onclick="clearSearch()" title="Limpar pesquisa">✕</button>
        </div>
    </div>

    <div class="table-responsive">
        <table id="guestTable">
            <thead>
                <tr>
                    <th class="checkbox-col">✓</th>
                    <th>Nome do Convidado (clique para editar)</th>
                    <th>Mesa</th>
                </tr>
            </thead>
            <tbody>
                <tr class="table-divider"><td colspan="3">MESA 1 - AURORA</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Cirilo e Esposa</td><td>Mesa 1</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Francisco e Esposa</td><td>Mesa 1</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Aninhas e Esposo</td><td>Mesa 1</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Belinha e Esposo</td><td>Mesa 1</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Alberto e Odete Tsamba</td><td>Mesa 1</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Luis Niquice e Esposa</td><td>Mesa 1</td></tr>

                <tr class="table-divider"><td colspan="3">MESA 2 - LUZ</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Augusto Miguel & Carlota Joao</td><td>Mesa 2</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Avó Cacilda & Avó Lucia</td><td>Mesa 2</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Avó Olga & Avó Tacho</td><td>Mesa 2</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Joana Portugal & Sefora Manhiça</td><td>Mesa 2</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Carlos Caetano & Antonieta Artiel</td><td>Mesa 2</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Rodrigo Alberto & Angelina Alberto</td><td>Mesa 2</td></tr>

                <tr class="table-divider"><td colspan="3">MESA 3 - INFINITO</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Norberto & Leónia</td><td>Mesa 3</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Ricardo & Aida</td><td>Mesa 3</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Anibal dos Anjos & Ana Amelia</td><td>Mesa 3</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Heitor Manhique e Maria Olga</td><td>Mesa 3</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Manuel Novele & Aurora Conjo</td><td>Mesa 3</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Luísa Novele</td><td>Mesa 3</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Isabel Conjo</td><td>Mesa 3</td></tr>

                <tr class="table-divider"><td colspan="3">MESA 4 - BRILHO</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Andre da Silva & Telma da Silva</td><td>Mesa 4</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Casimiro Manhique & Nilza Manhique</td><td>Mesa 4</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Moises Mabunda & Vilma Mabunda</td><td>Mesa 4</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Platiel & Esposa</td><td>Mesa 4</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Pedro Sitoe & Olivia Sitoe</td><td>Mesa 4</td></tr>

                <tr class="table-divider"><td colspan="3">MESA 5 - SOL</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Manuel Saide & Delfina Cheuane</td><td>Mesa 5</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Ascencio Mandra & Lisbet Mandra</td><td>Mesa 5</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Dercio Tivane & Jessica Tivane</td><td>Mesa 5</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Edson Ngonga & Leia Ngonga</td><td>Mesa 5</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Nando & Dinha</td><td>Mesa 5</td></tr>

                <tr class="table-divider"><td colspan="3">MESA 6 - LUA</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Florinda</td><td>Mesa 6</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Raquelina</td><td>Mesa 6</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Laurinda</td><td>Mesa 6</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Suzete</td><td>Mesa 6</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Cidalia & Ramiro</td><td>Mesa 6</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Eulalia & Rosário</td><td>Mesa 6</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Esmelinda</td><td>Mesa 6</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Atalia Bule</td><td>Mesa 6</td></tr>

                <tr class="table-divider"><td colspan="3">MESA 7 - ESTRELA</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Adnésio & Laura</td><td>Mesa 7</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Emilton Sumbane & Andreia Conjo</td><td>Mesa 7</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Augusto & Mária</td><td>Mesa 7</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Jair & Esposa</td><td>Mesa 7</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Jóse & Carmen</td><td>Mesa 7</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Leonel & Patrícia</td><td>Mesa 7</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Mário & Emilía</td><td>Mesa 7</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Mateus & Esposa</td><td>Mesa 7</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Welson & Ezaquinha</td><td>Mesa 7</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Paulino & Nilza</td><td>Mesa 7</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Yassmin & Rafael</td><td>Mesa 7</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Sidney</td><td>Mesa 7</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Loide de Carmo Jeque</td><td>Mesa 7</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Roberto</td><td>Mesa 7</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Vanildo</td><td>Mesa 7</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Walter Manhique</td><td>Mesa 7</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">José David</td><td>Mesa 7</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Edelsinha</td><td>Mesa 7</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Amarildo</td><td>Mesa 7</td></tr>

                <tr class="table-divider"><td colspan="3">MESA 8 - HARMONIA</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Acácio & Chiara</td><td>Mesa 8</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Canano & Jernita</td><td>Mesa 8</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Fidelia</td><td>Mesa 8</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Messias & Francelina</td><td>Mesa 8</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Nicolau & Cidalia</td><td>Mesa 8</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Rosa & Esposo</td><td>Mesa 8</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Wendy</td><td>Mesa 8</td></tr>

                <tr class="table-divider"><td colspan="3">MESA 9 - CELESTE</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Catarina Alberto</td><td>Mesa 9</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Ricardo Damao & Amelia Damao</td><td>Mesa 9</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Roberto Mioche & Fatima Abdala</td><td>Mesa 9</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Fernado Roberto & Esposa</td><td>Mesa 9</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Rosita & Jú</td><td>Mesa 9</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Dércia & Eldourado Alberto Rodrigo</td><td>Mesa 9</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Alberto Rodrigo</td><td>Mesa 9</td></tr>

                <tr class="table-divider"><td colspan="3">MESA 10 - ESPERANCA</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Adelaide e Virgilio</td><td>Mesa 10</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Sérgio Ndlaze & Tina</td><td>Mesa 10</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Márcia & Naura</td><td>Mesa 10</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Elito & Noémia</td><td>Mesa 10</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Zema</td><td>Mesa 10</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Ivan Novele</td><td>Mesa 10</td></tr>

                <tr class="table-divider"><td colspan="3">MESA 11 - ALEGRIA</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Lekhisso & Keyoni</td><td>Mesa 11</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Luana & Lenya</td><td>Mesa 11</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Miguel</td><td>Mesa 11</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Nguila</td><td>Mesa 11</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Anjo</td><td>Mesa 11</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Edwin</td><td>Mesa 11</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Elton & Generosa</td><td>Mesa 11</td></tr>

                <tr class="table-divider"><td colspan="3">MESA 12 - PARA SEMPRE</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Nelson Novele & Márcia Novele</td><td>Mesa 12</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Nércia Elísio & Edér Elíso</td><td>Mesa 12</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Herta</td><td>Mesa 12</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Nereid</td><td>Mesa 12</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Jéssica & Nkrumah</td><td>Mesa 12</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Karen e Hermeny</td><td>Mesa 12</td></tr>

                <tr class="table-divider"><td colspan="3">MESA 13 - AMOR</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Célia Quive</td><td>Mesa 13</td></tr>
                <tr><td class="checkbox-col"><input type="checkbox" onchange="toggleCheck(this)"></td><td class="guest-name" contenteditable="true" onblur="saveState()" onkeydown="handleEnter(event)">Gledcy</td><td>Mesa 13</td></tr>
            </tbody>
        </table>
        <div id="noResult" class="no-result">Nenhum convidado ou mesa encontrada.</div>
    </div>

    <div class="footer-controls">
        <button class="btn-reset" onclick="resetAll()">Desmarcar Todos</button>
    </div>

    <script>
        // Função para remover acentos e facilitar a busca
        function removeAccents(str) {
            return str.normalize("NFD").replace(/[\u0300-\u036f]/g, "").toLowerCase();
        }

        // Função de Pesquisa / Filtro em Tempo Real
        function filterGuests() {
            const input = document.getElementById('searchInput');
            const clearBtn = document.getElementById('clearSearchBtn');
            const filter = removeAccents(input.value.trim());
            const table = document.getElementById('guestTable');
            const rows = table.querySelectorAll('tbody tr');
            const noResult = document.getElementById('noResult');

            clearBtn.style.display = filter ? 'block' : 'none';

            let hasVisibleGuest = false;

            rows.forEach(row => {
                if (row.classList.contains('table-divider')) {
                    row.style.display = 'none'; // Inicialmente esconde os divisores de mesa na busca
                    return;
                }

                const cells = row.getElementsByTagName('td');
                if (cells.length > 1) {
                    const guestName = removeAccents(cells[1].textContent || cells[1].innerText);
                    const tableName = removeAccents(cells[2].textContent || cells[2].innerText);

                    if (guestName.includes(filter) || tableName.includes(filter)) {
                        row.style.display = '';
                        hasVisibleGuest = true;
                    } else {
                        row.style.display = 'none';
                    }
                }
            });

            // Se a busca estiver vazia, reexibe os divisores de mesa
            if (!filter) {
                rows.forEach(row => row.style.display = '');
                noResult.style.display = 'none';
            } else {
                noResult.style.display = hasVisibleGuest ? 'none' : 'block';
            }
        }

        // Limpar o campo de busca
        function clearSearch() {
            const input = document.getElementById('searchInput');
            input.value = '';
            filterGuests();
            input.focus();
        }

        // Marcar / Desmarcar Presença de Convidado
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

        // Atualizar Contador de Convidados
        function updateCounter() {
            const table = document.getElementById('guestTable');
            const totalRows = table.querySelectorAll('tbody tr:not(.table-divider)').length;
            const checkedRows = table.querySelectorAll('tbody tr.checked').length;
            const counterDiv = document.getElementById('guestCounter');

            counterDiv.textContent = `Chegaram: ${checkedRows} / Total: ${totalRows}`;
        }

        // Evitar quebras de linha indesejadas ao pressionar Enter na edição de nomes
        function handleEnter(event) {
            if (event.key === 'Enter') {
                event.preventDefault();
                event.target.blur();
            }
        }

        // Salvar estado atual (checkmarks e nomes editados) no LocalStorage do navegador
        function saveState() {
            const rows = document.querySelectorAll('#guestTable tbody tr:not(.table-divider)');
            const state = [];

            rows.forEach((row, index) => {
                const checkbox = row.querySelector('input[type="checkbox"]');
                const guestNameCell = row.querySelector('.guest-name');
                if (checkbox && guestNameCell) {
                    state.push({
                        index: index,
                        checked: checkbox.checked,
                        name: guestNameCell.innerText.trim()
                    });
                }
            });

            localStorage.setItem('ccm_guest_list_state', JSON.stringify(state));
        }

        // Carregar estado salvo do LocalStorage
        function loadState() {
            const savedState = localStorage.getItem('ccm_guest_list_state');
            if (!savedState) {
                updateCounter();
                return;
            }

            const state = JSON.parse(savedState);
            const rows = document.querySelectorAll('#guestTable tbody tr:not(.table-divider)');

            state.forEach(item => {
                if (rows[item.index]) {
                    const checkbox = rows[item.index].querySelector('input[type="checkbox"]');
                    const guestNameCell = rows[item.index].querySelector('.guest-name');

                    if (checkbox) {
                        checkbox.checked = item.checked;
                        if (item.checked) {
                            rows[item.index].classList.add('checked');
                        }
                    }
                    if (guestNameCell && item.name) {
                        guestNameCell.innerText = item.name;
                    }
                }
            });

            updateCounter();
        }

        // Desmarcar todos os convidados
        function resetAll() {
            if (confirm('Deseja realmente desmarcar a presença de todos os convidados?')) {
                const checkboxes = document.querySelectorAll('#guestTable input[type="checkbox"]');
                checkboxes.forEach(cb => {
                    cb.checked = false;
                    cb.closest('tr').classList.remove('checked');
                });
                updateCounter();
                saveState();
            }
        }

        // Inicializar a página
        window.addEventListener('DOMContentLoaded', () => {
            loadState();
        });
    </script>
</body>
</html>
