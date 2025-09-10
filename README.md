<!DOCTYPE html>
<html lang="it">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Scala della Sonnolenza di Epworth - Questionario</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 800px;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.2);
            backdrop-filter: blur(10px);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
            color: white;
            padding: 30px;
            text-align: center;
        }

        .header h1 {
            font-size: 2.2rem;
            margin-bottom: 10px;
        }

        .header p {
            opacity: 0.9;
            font-size: 1.1rem;
        }

        .form-container {
            padding: 40px;
        }

        .section {
            margin-bottom: 40px;
            padding: 25px;
            background: #f8fafc;
            border-radius: 15px;
            border-left: 5px solid #4facfe;
        }

        .section h2 {
            color: #2d3748;
            margin-bottom: 20px;
            font-size: 1.4rem;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .section-icon {
            background: linear-gradient(45deg, #4facfe, #00f2fe);
            color: white;
            width: 30px;
            height: 30px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 0.9rem;
        }

        .form-row {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
            margin-bottom: 20px;
        }

        .form-group {
            margin-bottom: 20px;
        }

        .form-group.full-width {
            grid-column: 1 / -1;
        }

        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: #2d3748;
            font-size: 0.95rem;
        }

        input[type="text"], input[type="date"], input[type="password"] {
            width: 100%;
            padding: 12px 15px;
            border: 2px solid #e2e8f0;
            border-radius: 10px;
            font-size: 1rem;
            transition: all 0.3s ease;
            background: white;
        }

        input[type="text"]:focus, input[type="date"]:focus, input[type="password"]:focus {
            outline: none;
            border-color: #4facfe;
            box-shadow: 0 0 0 3px rgba(79, 172, 254, 0.1);
        }

        .epworth-question {
            background: white;
            padding: 20px;
            margin-bottom: 15px;
            border-radius: 12px;
            border: 2px solid #e2e8f0;
            transition: all 0.3s ease;
        }

        .epworth-question:hover {
            border-color: #4facfe;
            box-shadow: 0 5px 15px rgba(79, 172, 254, 0.1);
        }

        .question-text {
            font-weight: 600;
            color: #2d3748;
            margin-bottom: 15px;
            font-size: 1rem;
        }

        .radio-group {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 10px;
        }

        .radio-option {
            display: flex;
            align-items: center;
            padding: 10px 15px;
            background: #f7fafc;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.3s ease;
            border: 2px solid transparent;
        }

        .radio-option:hover {
            background: #edf2f7;
            border-color: #4facfe;
        }

        .radio-option input[type="radio"] {
            margin-right: 10px;
            transform: scale(1.2);
        }

        .radio-option.selected {
            background: linear-gradient(45deg, #4facfe, #00f2fe);
            color: white;
            border-color: #4facfe;
        }

        .score-display {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 20px;
            border-radius: 15px;
            text-align: center;
            margin: 20px 0;
            display: none;
        }

        .score-number {
            font-size: 3rem;
            font-weight: bold;
            margin: 10px 0;
        }

        .score-interpretation {
            font-size: 1.1rem;
            opacity: 0.9;
        }

        .submit-section {
            text-align: center;
            margin-top: 40px;
            padding: 30px;
            background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
            border-radius: 15px;
        }

        .submit-btn {
            background: linear-gradient(45deg, #ff6b6b, #ee5a24);
            color: white;
            border: none;
            padding: 15px 40px;
            font-size: 1.1rem;
            font-weight: bold;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 10px 30px rgba(238, 90, 36, 0.3);
        }

        .submit-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 15px 40px rgba(238, 90, 36, 0.4);
        }

        .submit-btn:disabled {
            background: #cbd5e0;
            cursor: not-allowed;
            transform: none;
            box-shadow: none;
        }

        .results-section {
            display: none;
            background: white;
            padding: 30px;
            border-radius: 15px;
            margin-top: 20px;
            border: 2px solid #4facfe;
        }

        .results-section h3 {
            color: #2d3748;
            margin-bottom: 20px;
            text-align: center;
        }

        .results-table {
            width: 100%;
            border-collapse: collapse;
            margin-bottom: 20px;
        }

        .results-table th,
        .results-table td {
            padding: 12px;
            text-align: left;
            border-bottom: 1px solid #e2e8f0;
        }

        .results-table th {
            background: #f7fafc;
            font-weight: 600;
        }

        .export-btn {
            background: linear-gradient(45deg, #4facfe, #00f2fe);
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 8px;
            cursor: pointer;
            margin: 5px;
            transition: all 0.3s ease;
        }

        .export-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(79, 172, 254, 0.3);
        }

        .required {
            color: #e53e3e;
        }

        .progress-bar {
            background: #e2e8f0;
            height: 6px;
            border-radius: 3px;
            margin: 20px 0;
            overflow: hidden;
        }

        .progress-fill {
            background: linear-gradient(90deg, #4facfe, #00f2fe);
            height: 100%;
            width: 0%;
            transition: width 0.3s ease;
        }

        .section {
            animation: fadeIn 0.6s ease forwards;
        }
            .form-row {
                grid-template-columns: 1fr;
            }
            
            .radio-group {
                grid-template-columns: 1fr;
            }
            
            .container {
                margin: 10px;
            }
            
            .form-container {
                padding: 20px;
            }
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .section {
            animation: fadeIn 0.6s ease forwards;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>📋 Scala della Sonnolenza di Epworth</h1>
            <p>Questionario per la valutazione della sonnolenza diurna</p>
        </div>

        <div class="form-container">
            <form id="epworthForm">
                <!-- Progress Bar -->
                <div class="progress-bar">
                    <div class="progress-fill" id="progressFill"></div>
                </div>

                <!-- Sezione Dati Personali -->
                <div class="section">
                    <h2>
                        <span class="section-icon">1</span>
                        Dati Personali
                    </h2>
                    <div class="form-row">
                        <div class="form-group">
                            <label for="cognome">Cognome <span class="required">*</span></label>
                            <input type="text" id="cognome" name="cognome" required>
                        </div>
                        <div class="form-group">
                            <label for="nome">Nome <span class="required">*</span></label>
                            <input type="text" id="nome" name="nome" required>
                        </div>
                    </div>
                    <div class="form-row">
                        <div class="form-group">
                            <label for="dataNascita">Data di Nascita <span class="required">*</span></label>
                            <input type="date" id="dataNascita" name="dataNascita" required>
                        </div>
                        <div class="form-group">
                            <label for="numeroSeriale">Numero Seriale <span class="required">*</span></label>
                            <input type="text" id="numeroSeriale" name="numeroSeriale" required>
                        </div>
                    </div>
                    <div class="form-row">
                        <div class="form-group">
                            <label for="pin">PIN <span class="required">*</span></label>
                            <input type="password" id="pin" name="pin" required>
                        </div>
                    </div>
                </div>

                <!-- Sezione Scala di Epworth -->
                <div class="section">
                    <h2>
                        <span class="section-icon">2</span>
                        Scala della Sonnolenza di Epworth
                    </h2>
                    <p style="margin-bottom: 25px; color: #4a5568; font-style: italic;">
                        Per ciascuna delle seguenti situazioni, indica quanto è probabile che tu ti assopisca o ti addormenti, non solo che ti senta stanco. Se non ti sei mai trovato in alcune di queste situazioni, prova a immaginare come potrebbero influenzarti.
                    </p>

                    <div id="epworthQuestions"></div>

                    <div class="score-display" id="scoreDisplay">
                        <h3>Il tuo punteggio:</h3>
                        <div class="score-number" id="scoreNumber">0</div>
                        <div class="score-interpretation" id="scoreInterpretation"></div>
                    </div>
                </div>

                <!-- Sezione Submit -->
                <div class="submit-section">
                    <button type="submit" class="submit-btn" id="submitBtn" disabled>
                        🚀 Completa Questionario
                    </button>
                    <p style="margin-top: 15px; color: white; opacity: 0.9;">
                        Assicurati di aver compilato tutti i campi obbligatori
                    </p>
                </div>
            </form>

            <!-- Sezione Risultati -->
            <div class="results-section" id="resultsSection">
                <h3>📊 Riepilogo Risultati</h3>
                <table class="results-table" id="resultsTable"></table>
                <div style="text-align: center;">
                    <button class="export-btn" onclick="exportToPDF()">📄 Esporta PDF</button>
                    <button class="export-btn" onclick="exportToCSV()">📊 Esporta CSV</button>
                    <button class="export-btn" onclick="printResults()">🖨️ Stampa</button>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Domande della Scala di Epworth
        const epworthQuestions = [
            "Seduto e leggendo",
            "Guardando la TV",
            "Seduto inattivo in un luogo pubblico (teatro, riunione, etc.)",
            "Come passeggero in auto per un'ora senza pause",
            "Disteso per riposare nel pomeriggio quando le circostanze lo permettono",
            "Seduto e parlando con qualcuno",
            "Seduto tranquillo dopo pranzo senza alcol",
            "In auto, fermo per pochi minuti nel traffico"
        ];

        const responseOptions = [
            { value: 0, text: "Mai mi addormenterei" },
            { value: 1, text: "Lieve probabilità di addormentarmi" },
            { value: 2, text: "Moderata probabilità di addormentarmi" },
            { value: 3, text: "Alta probabilità di addormentarmi" }
        ];

        let formData = {};
        let currentScore = 0;

        // Inizializzazione
        document.addEventListener('DOMContentLoaded', function() {
            generateEpworthQuestions();
            setupFormValidation();
            setupEventListeners();
        });

        function generateEpworthQuestions() {
            const container = document.getElementById('epworthQuestions');
            
            epworthQuestions.forEach((question, index) => {
                const questionDiv = document.createElement('div');
                questionDiv.className = 'epworth-question';
                questionDiv.innerHTML = `
                    <div class="question-text">${index + 1}. ${question}</div>
                    <div class="radio-group">
                        ${responseOptions.map(option => `
                            <label class="radio-option">
                                <input type="radio" name="q${index}" value="${option.value}" required>
                                <span>${option.text}</span>
                            </label>
                        `).join('')}
                    </div>
                `;
                container.appendChild(questionDiv);
            });
        }

        function setupEventListeners() {
            // Event listeners per radio buttons
            document.querySelectorAll('input[type="radio"]').forEach(radio => {
                radio.addEventListener('change', function() {
                    // Aggiorna styling delle opzioni
                    const parent = this.closest('.radio-group');
                    parent.querySelectorAll('.radio-option').forEach(option => {
                        option.classList.remove('selected');
                    });
                    this.closest('.radio-option').classList.add('selected');
                    
                    // Calcola punteggio
                    calculateScore();
                    updateProgress();
                    validateForm();
                });
            });

            // Event listeners per campi di input
            document.querySelectorAll('input[required]').forEach(input => {
                input.addEventListener('input', function() {
                    updateProgress();
                    validateForm();
                });
            });

            // Submit form
            document.getElementById('epworthForm').addEventListener('submit', handleSubmit);
        }

        function calculateScore() {
            let score = 0;
            epworthQuestions.forEach((_, index) => {
                const selectedRadio = document.querySelector(`input[name="q${index}"]:checked`);
                if (selectedRadio) {
                    score += parseInt(selectedRadio.value);
                }
            });
            
            currentScore = score;
            updateScoreDisplay();
        }

        function updateScoreDisplay() {
            const scoreDisplay = document.getElementById('scoreDisplay');
            const scoreNumber = document.getElementById('scoreNumber');
            const scoreInterpretation = document.getElementById('scoreInterpretation');
            
            scoreNumber.textContent = currentScore;
            
            let interpretation = '';
            if (currentScore <= 9) {
                interpretation = 'Normale - Sonnolenza diurna nella norma';
            } else if (currentScore <= 12) {
                interpretation = 'Lieve - Sonnolenza diurna lievemente elevata';
            } else if (currentScore <= 15) {
                interpretation = 'Moderata - Sonnolenza diurna moderata';
            } else {
                interpretation = 'Grave - Sonnolenza diurna eccessiva - Consulta un medico';
            }
            
            scoreInterpretation.textContent = interpretation;
            
            if (currentScore > 0) {
                scoreDisplay.style.display = 'block';
            }
        }

        function updateProgress() {
            const requiredFields = document.querySelectorAll('input[required]');
            const filledFields = Array.from(requiredFields).filter(field => {
                if (field.type === 'radio') {
                    return document.querySelector(`input[name="${field.name}"]:checked`);
                }
                return field.value.trim() !== '';
            });
            
            // Conta domande Epworth uniche
            const epworthCompleted = epworthQuestions.filter((_, index) => {
                return document.querySelector(`input[name="q${index}"]:checked`);
            }).length;
            
            const totalPersonalFields = 5; // cognome, nome, data, seriale, pin
            const totalEpworthQuestions = 8;
            const totalFields = totalPersonalFields + totalEpworthQuestions;
            const completedFields = (filledFields.length - epworthCompleted) + epworthCompleted;
            
            const progress = (completedFields / totalFields) * 100;
            document.getElementById('progressFill').style.width = progress + '%';
        }

        function validateForm() {
            const requiredFields = document.querySelectorAll('input[required]');
            let isValid = true;
            
            // Controlla campi personali
            const personalFields = ['cognome', 'nome', 'dataNascita', 'numeroSeriale', 'pin'];
            personalFields.forEach(fieldName => {
                const field = document.getElementById(fieldName);
                if (!field.value.trim()) {
                    isValid = false;
                }
            });
            
            // Controlla domande Epworth
            epworthQuestions.forEach((_, index) => {
                const selectedRadio = document.querySelector(`input[name="q${index}"]:checked`);
                if (!selectedRadio) {
                    isValid = false;
                }
            });
            
            document.getElementById('submitBtn').disabled = !isValid;
        }

        function setupFormValidation() {
            validateForm();
        }

        function handleSubmit(e) {
            e.preventDefault();
            
            // Raccoglie tutti i dati
            formData = {
                cognome: document.getElementById('cognome').value,
                nome: document.getElementById('nome').value,
                dataNascita: document.getElementById('dataNascita').value,
                numeroSeriale: document.getElementById('numeroSeriale').value,
                pin: document.getElementById('pin').value,
                risposte: {},
                punteggio: currentScore,
                dataCompilazione: new Date().toLocaleString('it-IT')
            };
            
            epworthQuestions.forEach((question, index) => {
                const selectedRadio = document.querySelector(`input[name="q${index}"]:checked`);
                formData.risposte[`domanda_${index + 1}`] = {
                    testo: question,
                    valore: parseInt(selectedRadio.value),
                    risposta: selectedRadio.nextElementSibling.textContent
                };
            });
            
            showResults();
        }

        function showResults() {
            const resultsSection = document.getElementById('resultsSection');
            const resultsTable = document.getElementById('resultsTable');
            
            // Interpretazione del punteggio
            let interpretazione = '';
            let colore = '';
            if (currentScore <= 9) {
                interpretazione = 'Normale';
                colore = '#10b981';
            } else if (currentScore <= 12) {
                interpretazione = 'Lieve';
                colore = '#f59e0b';
            } else if (currentScore <= 15) {
                interpretazione = 'Moderata';
                colore = '#f97316';
            } else {
                interpretazione = 'Grave - Consultare un medico';
                colore = '#ef4444';
            }
            
            resultsTable.innerHTML = `
                <tr>
                    <th colspan="2" style="text-align: center; background: linear-gradient(45deg, #4facfe, #00f2fe); color: white;">
                        RISULTATI QUESTIONARIO EPWORTH
                    </th>
                </tr>
                <tr>
                    <td><strong>Nome Completo:</strong></td>
                    <td>${formData.nome} ${formData.cognome}</td>
                </tr>
                <tr>
                    <td><strong>Data di Nascita:</strong></td>
                    <td>${new Date(formData.dataNascita).toLocaleDateString('it-IT')}</td>
                </tr>
                <tr>
                    <td><strong>Numero Seriale:</strong></td>
                    <td>${formData.numeroSeriale}</td>
                </tr>
                <tr>
                    <td><strong>Data Compilazione:</strong></td>
                    <td>${formData.dataCompilazione}</td>
                </tr>
                <tr>
                    <td><strong>Punteggio Totale:</strong></td>
                    <td style="font-size: 1.3rem; font-weight: bold; color: ${colore};">${currentScore}/24</td>
                </tr>
                <tr>
                    <td><strong>Interpretazione:</strong></td>
                    <td style="font-weight: bold; color: ${colore};">${interpretazione}</td>
                </tr>
            `;
            
            resultsSection.style.display = 'block';
            resultsSection.scrollIntoView({ behavior: 'smooth', block: 'start' });
        }

        // Funzioni di esportazione
        function exportToPDF() {
            const printContent = generatePrintableContent();
            const printWindow = window.open('', '_blank');
            printWindow.document.write(`
                <html>
                <head>
                    <title>Risultati Scala Epworth - ${formData.nome} ${formData.cognome}</title>
                    <style>
                        body { font-family: Arial, sans-serif; margin: 20px; }
                        .header { text-align: center; border-bottom: 2px solid #4facfe; padding-bottom: 10px; margin-bottom: 20px; }
                        .section { margin-bottom: 20px; }
                        table { width: 100%; border-collapse: collapse; margin-bottom: 20px; }
                        th, td { padding: 8px; text-align: left; border-bottom: 1px solid #ddd; }
                        th { background-color: #f2f2f2; }
                        .score { font-size: 1.2rem; font-weight: bold; }
                    </style>
                </head>
                <body>${printContent}</body>
                </html>
            `);
            printWindow.document.close();
            setTimeout(() => {
                printWindow.print();
                printWindow.close();
            }, 250);
        }

        function exportToCSV() {
            let csv = 'Campo,Valore\n';
            csv += `Nome,${formData.nome}\n`;
            csv += `Cognome,${formData.cognome}\n`;
            csv += `Data di Nascita,${formData.dataNascita}\n`;
            csv += `Numero Seriale,${formData.numeroSeriale}\n`;
            csv += `Data Compilazione,${formData.dataCompilazione}\n`;
            csv += `Punteggio Totale,${currentScore}\n`;
            csv += '\n';
            
            Object.entries(formData.risposte).forEach(([key, value]) => {
                csv += `"${value.testo}","${value.risposta} (${value.valore})"\n`;
            });
            
            const blob = new Blob([csv], { type: 'text/csv;charset=utf-8;' });
            const link = document.createElement('a');
            link.href = URL.createObjectURL(blob);
            link.download = `epworth_${formData.cognome}_${formData.nome}_${new Date().toISOString().split('T')[0]}.csv`;
            link.click();
        }

        function printResults() {
            const printContent = generatePrintableContent();
            const printWindow = window.open('', '_blank');
            printWindow.document.write(`
                <html>
                <head>
                    <title>Stampa Risultati</title>
                    <style>
                        body { font-family: Arial, sans-serif; margin: 20px; }
                        .header { text-align: center; border-bottom: 2px solid #000; padding-bottom: 10px; margin-bottom: 20px; }
                        table { width: 100%; border-collapse: collapse; margin-bottom: 20px; }
                        th, td { padding: 8px; text-align: left; border-bottom: 1px solid #000; }
                        th { background-color: #f0f0f0; }
                        @media print { body { margin: 0; } }
                    </style>
                </head>
                <body onload="window.print(); window.close();">${printContent}</body>
                </html>
            `);
            printWindow.document.close();
        }

        function generatePrintableContent() {
            let content = `
                <div class="header">
                    <h1>SCALA DELLA SONNOLENZA DI EPWORTH</h1>
                    <h2>Risultati Questionario</h2>
                </div>
                
                <div class="section">
                    <h3>Dati Paziente</h3>
                    <table>
                        <tr><td><strong>Nome:</strong></td><td>${formData.nome}</td></tr>
                        <tr><td><strong>Cognome:</strong></td><td>${formData.cognome}</td></tr>
                        <tr><td><strong>Data di Nascita:</strong></td><td>${new Date(formData.dataNascita).toLocaleDateString('it-IT')}</td></tr>
                        <tr><td><strong>Numero Seriale:</strong></td><td>${formData.numeroSeriale}</td></tr>
                        <tr><td><strong>Data Compilazione:</strong></td><td>${formData.dataCompilazione}</td></tr>
                    </table>
                </div>
                
                <div class="section">
                    <h3>Risultati</h3>
                    <table>
                        <tr><td><strong>Punteggio Totale:</strong></td><td class="score">${currentScore}/24</td></tr>
                    </table>
                </div>
                
                <div class="section">
                    <h3>Risposte Dettagliate</h3>
                    <table>
                        <tr><th>Situazione</th><th>Risposta</th><th>Punteggio</th></tr>`;
            
            Object.entries(formData.risposte).forEach(([key, value]) => {
                content += `<tr><td>${value.testo}</td><td>${value.risposta}</td><td>${value.valore}</td></tr>`;
            });
            
            content += `</table></div>`;
            return content;
        }
    </script>
</body>
</html>
