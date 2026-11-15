<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Omar Meister App - SHK Prüfungstrainer</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap');
        body {
            font-family: 'Inter', sans-serif;
            -webkit-tap-highlight-color: transparent;
        }
        /* Versteckt Scrollbars bei horizontalen Filter-Leisten auf dem iPhone */
        .no-scrollbar::-webkit-scrollbar {
            display: none;
        }
        .no-scrollbar {
            -ms-overflow-style: none;
            scrollbar-width: none;
        }
    </style>
</head>
<body class="bg-slate-100 text-slate-800 min-h-screen flex flex-col items-center p-2.5 sm:p-6">

    <!-- Haupt-Container -->
    <div class="w-full max-w-lg bg-white rounded-3xl shadow-xl border border-slate-200/70 overflow-hidden flex flex-col my-auto">
        
        <!-- Header Card -->
        <header class="bg-gradient-to-br from-blue-600 via-blue-700 to-indigo-800 text-white p-6 text-center shadow-inner">
            <h1 class="text-2xl sm:text-3xl font-extrabold tracking-tight">Omar Meister App</h1>
            <p class="text-[11px] sm:text-xs text-blue-100 mt-1.5 uppercase tracking-widest font-semibold">
                ANLAGENMECHANIKER SHK PRÜFUNGSTRAINER
            </p>
        </header>

        <!-- Haupt-Navigation (Tabs) -->
        <nav class="flex border-b border-slate-200 bg-slate-50/90 p-2 gap-2">
            <button onclick="switchTab('quiz')" id="btn-quiz" class="flex-1 py-3 px-4 rounded-2xl text-sm font-bold transition-all bg-blue-600 text-white shadow-sm active:scale-[0.98]">
                🎯 Quiz-Trainer
            </button>
            <button onclick="switchTab('editor')" id="btn-editor" class="flex-1 py-3 px-4 rounded-2xl text-sm font-bold transition-all text-slate-600 hover:bg-slate-200/70 active:scale-[0.98]">
                📝 Notizen & Editor
            </button>
        </nav>

        <!-- Hauptbereich -->
        <main class="p-4 sm:p-6 flex-1 flex flex-col">

            <!-- SEKTION 1: QUIZ-TRAINER -->
            <section id="section-quiz" class="flex flex-col flex-1">
                
                <!-- Abteilungs-Auswahl (Horizontal scrollbar auf dem iPhone) -->
                <div class="mb-3.5">
                    <span class="block text-[11px] font-bold uppercase tracking-wider text-slate-400 mb-2">1. Abteilung wählen:</span>
                    <div id="dept-filter-container" class="flex gap-2 overflow-x-auto no-scrollbar pb-1">
                        <button onclick="setDepartment('alle')" id="dept-alle" class="shrink-0 py-2 px-3.5 rounded-xl text-xs font-bold border-2 border-blue-600 bg-blue-50 text-blue-800 transition-all active:scale-95">
                            🏛️ Alle (100)
                        </button>
                        <button onclick="setDepartment('Heizung & Wärmepumpen')" id="dept-Heizung & Wärmepumpen" class="shrink-0 py-2 px-3.5 rounded-xl text-xs font-bold border border-slate-200 bg-white text-slate-700 hover:bg-slate-50 transition-all active:scale-95">
                            🔥 Heizung & WP (18)
                        </button>
                        <button onclick="setDepartment('Sanitär & Trinkwasser')" id="dept-Sanitär & Trinkwasser" class="shrink-0 py-2 px-3.5 rounded-xl text-xs font-bold border border-slate-200 bg-white text-slate-700 hover:bg-slate-50 transition-all active:scale-95">
                            💧 Sanitär & Wasser (18)
                        </button>
                        <button onclick="setDepartment('Gas & Abgas')" id="dept-Gas & Abgas" class="shrink-0 py-2 px-3.5 rounded-xl text-xs font-bold border border-slate-200 bg-white text-slate-700 hover:bg-slate-50 transition-all active:scale-95">
                            ⛽ Gas & Abgas (17)
                        </button>
                        <button onclick="setDepartment('Lüftung & Klima')" id="dept-Lüftung & Klima" class="shrink-0 py-2 px-3.5 rounded-xl text-xs font-bold border border-slate-200 bg-white text-slate-700 hover:bg-slate-50 transition-all active:scale-95">
                            🌬️ Lüftung & Klima (16)
                        </button>
                        <button onclick="setDepartment('Elektro & Regelung')" id="dept-Elektro & Regelung" class="shrink-0 py-2 px-3.5 rounded-xl text-xs font-bold border border-slate-200 bg-white text-slate-700 hover:bg-slate-50 transition-all active:scale-95">
                            ⚡ Elektro & Regelung (16)
                        </button>
                        <button onclick="setDepartment('Werkstoffe & Normen')" id="dept-Werkstoffe & Regelung" class="hidden"></button>
                        <button onclick="setDepartment('Werkstoffe & Normen')" id="dept-Werkstoffe & Normen" class="shrink-0 py-2 px-3.5 rounded-xl text-xs font-bold border border-slate-200 bg-white text-slate-700 hover:bg-slate-50 transition-all active:scale-95">
                            🔧 Werkstoffe & Normen (15)
                        </button>
                    </div>
                </div>

                <!-- Schwierigkeitslevel-Auswahl -->
                <div class="mb-4">
                    <span class="block text-[11px] font-bold uppercase tracking-wider text-slate-400 mb-2">2. Schwierigkeitsgrad:</span>
                    <div class="grid grid-cols-4 gap-1.5">
                        <button onclick="setDifficulty('alle')" id="diff-alle" class="py-2 px-2 rounded-xl text-xs font-bold border-2 border-blue-600 bg-blue-50 text-blue-800 transition-all active:scale-95 text-center">
                            Alle
                        </button>
                        <button onclick="setDifficulty('leicht')" id="diff-leicht" class="py-2 px-2 rounded-xl text-xs font-bold border border-slate-200 bg-white text-slate-700 hover:bg-slate-50 transition-all active:scale-95 text-center">
                            🟢 Leicht
                        </button>
                        <button onclick="setDifficulty('mittel')" id="diff-mittel" class="py-2 px-2 rounded-xl text-xs font-bold border border-slate-200 bg-white text-slate-700 hover:bg-slate-50 transition-all active:scale-95 text-center">
                            🟡 Mittel
                        </button>
                        <button onclick="setDifficulty('schwer')" id="diff-schwer" class="py-2 px-2 rounded-xl text-xs font-bold border border-slate-200 bg-white text-slate-700 hover:bg-slate-50 transition-all active:scale-95 text-center">
                            🔴 Schwer
                        </button>
                    </div>
                </div>

                <!-- Fortschritt, Level-Badge, Zufalls-Mix & Punktestand -->
                <div class="flex flex-wrap justify-between items-center gap-2 mb-4 text-xs font-semibold">
                    <div class="flex items-center gap-1.5">
                        <span id="question-counter" class="bg-slate-100 px-3 py-1 rounded-full text-slate-700">Frage 1 von 100</span>
                        <span id="level-badge" class="px-2.5 py-1 rounded-full text-[11px] font-bold bg-emerald-100 text-emerald-800">🟢 Leicht</span>
                    </div>
                    <div class="flex items-center gap-1.5">
                        <button onclick="shuffleQuestions()" title="Fragen mischen" class="bg-indigo-50 hover:bg-indigo-100 text-indigo-700 border border-indigo-200 px-2.5 py-1 rounded-full font-bold transition-all active:scale-95">
                            🔀 Mix
                        </button>
                        <span id="score-display" class="bg-blue-100 text-blue-800 px-3 py-1 rounded-full font-bold">Richtig: 0</span>
                    </div>
                </div>

                <!-- Vorlesefunktion & Stimmenauswahl -->
                <div class="mb-5 space-y-2.5 bg-slate-50 p-3.5 rounded-2xl border border-slate-200/80">
                    <button onclick="textVorlesen('frage')" class="flex items-center justify-center gap-2 w-full py-3 px-4 bg-blue-600 hover:bg-blue-700 text-white font-semibold rounded-xl text-sm transition-all shadow-sm active:scale-[0.98]">
                        <span class="text-base">🔊</span> Frage vorlesen
                    </button>
                    
                    <!-- Saubere Stimmenauswahl -->
                    <div class="flex items-center justify-between gap-2 bg-white px-3.5 py-2.5 rounded-xl border border-slate-200">
                        <label for="voice-profile" class="text-xs font-semibold text-slate-600 whitespace-nowrap">Stimme:</label>
                        <select id="voice-profile" class="w-full bg-transparent text-xs text-slate-800 font-bold focus:outline-none cursor-pointer">
                            <option value="male" selected>👨 Männlich (Markus)</option>
                            <option value="female">👩 Weiblich (Anna)</option>
                        </select>
                    </div>

                    <!-- Hilfreicher iOS-Hinweis -->
                    <p class="text-[11px] leading-snug text-slate-500 px-1">
                        💡 <span class="font-semibold text-slate-600">iPhone-Tipp:</span> Falls keine tiefe Männerstimme geladen ist, installiere sie unter <span class="italic">Einstellungen &gt; Bedienungshilfen &gt; Gesprochene Inhalte &gt; Stimmen &gt; Deutsch</span> (z. B. „Markus“ oder „Martin“).
                    </p>
                </div>

                <!-- Themen-Tag & Fragetext -->
                <div class="mb-4">
                    <span id="topic-tag" class="inline-block text-[11px] font-bold uppercase tracking-wider text-blue-600 mb-1">Heizung & Wärmepumpen</span>
                    <div id="question-box" class="text-base sm:text-lg font-bold text-slate-900 leading-snug">
                        <!-- Frage wird sofort per JS eingefügt -->
                    </div>
                </div>

                <!-- Antwortmöglichkeiten -->
                <div id="options-container" class="space-y-2.5 mb-5">
                    <!-- Optionen werden sofort per JS eingefügt -->
                </div>

                <!-- Feedback & Erklärung -->
                <div id="quiz-feedback" class="hidden rounded-2xl transition-all mb-4"></div>

                <!-- Nächste Frage Button -->
                <button id="next-btn" onclick="naechsteFrage()" style="display: none;" class="w-full py-3.5 bg-blue-600 hover:bg-blue-700 active:scale-[0.98] text-white font-bold rounded-2xl shadow-md transition-all mt-auto">
                    Nächste Frage ➔
                </button>
            </section>

            <!-- SEKTION 2: NOTIZEN & EDITOR -->
            <section id="section-editor" class="hidden flex flex-col flex-1">
                <div class="mb-3">
                    <h2 class="text-base font-bold text-slate-900">Persönliche Notizen & Formeln</h2>
                    <p class="text-xs text-slate-500 mt-0.5">Deine Merkhilfen werden lokal und dauerhaft auf deinem Gerät gespeichert.</p>
                </div>
                <textarea id="user-notes" placeholder="Schreibe hier deine eigenen Formeln (z. B. MAG-Vordruck p0, Volumenstrom, Gefälle), Merksätze oder Prüfungstipps hinein..." class="w-full flex-1 min-h-[260px] p-4 text-sm rounded-2xl border border-slate-200 bg-slate-50/60 focus:bg-white focus:outline-none focus:ring-2 focus:ring-blue-500/50 focus:border-blue-500 resize-none font-sans leading-relaxed"></textarea>
                
                <div class="flex items-center justify-between mt-4">
                    <button onclick="notizSpeichern()" class="py-3 px-6 bg-blue-600 hover:bg-blue-700 active:scale-[0.98] text-white text-sm font-bold rounded-2xl shadow-sm transition-all">
                        💾 Notiz speichern
                    </button>
                    <span id="save-status" class="text-xs font-bold text-emerald-700 bg-emerald-100 px-3.5 py-1.5 rounded-full opacity-0 transition-opacity">
                        ✅ Gespeichert!
                    </span>
                </div>
            </section>

        </main>

        <!-- Footer -->
        <footer class="p-3.5 bg-slate-50 text-center text-[11px] font-medium text-slate-400 border-t border-slate-100">
            Omar Meister App • SHK Gesellen- & Meistervorbereitung
        </footer>

    </div>

    <!-- JavaScript Anwendungslogik (direkte Ausführung ohne Wartezeit) -->
    <script>
        // Vollständiger SHK-Prüfungskatalog mit exakt 100 Fachfragen in 6 Abteilungen
        const fragenKatalog = [
            // =========================================================================
            // ABTEILUNG 1: HEIZUNG & WÄRMEPUMPEN (18 Fragen: 6 Leicht, 6 Mittel, 6 Schwer)
            // =========================================================================
            {
                id: 1,
                abteilung: "Heizung & Wärmepumpen",
                level: "leicht",
                frage: "Welche Hauptaufgabe erfüllt ein Membran-Ausdehnungsgefäß (MAG) in einer geschlossenen Heizungsanlage?",
                optionen: [
                    "Es filtert Rost- und Schlammteilchen aus dem Heizungswasser",
                    "Es nimmt die Wärmeausdehnung des Wassers auf und hält den Anlagendruck stabil",
                    "Es erhöht die Vorlauftemperatur bei Außentemperaturen unter -10 °C",
                    "Es schaltet die Umwälzpumpe im Sommerbetrieb ab"
                ],
                richtig: 1,
                erklaerung: "Beim Erwärmen dehnt sich Wasser aus. Das MAG fängt dieses Ausdehnungsvolumen über eine flexible Membran gegen ein Stickstoffpolster auf, sodass das Sicherheitsventil nicht anspricht."
            },
            {
                id: 2,
                abteilung: "Heizung & Wärmepumpen",
                level: "leicht",
                frage: "Welcher Ansprechdruck ist bei Sicherheitsventilen in geschlossenen Kleinkessel-Heizungsanlagen (Wohngebäude) üblich?",
                optionen: ["1,0 bar", "2,5 bar oder 3,0 bar", "6,0 bar", "10,0 bar"],
                richtig: 1,
                erklaerung: "In standardmäßigen geschlossenen Warmwasser-Heizungsanlagen für Wohnhäuser werden meist Sicherheitsventile mit einem Ansprechdruck von 2,5 bar oder 3,0 bar eingesetzt."
            },
            {
                id: 3,
                abteilung: "Heizung & Wärmepumpen",
                level: "leicht",
                frage: "In welcher Einheit wird die Wärmeleistung (Nennwärmeleistung) eines Heizkessels oder Heizkörpers angegeben?",
                optionen: ["Kilowattstunde (kWh)", "Kilowatt (kW) bzw. Watt (W)", "Kubikmeter pro Stunde (m³/h)", "Kelvin (K)"],
                richtig: 1,
                erklaerung: "Die Leistung wird in Watt (W) bzw. Kilowatt (kW) angegeben. Die Kilowattstunde (kWh) hingegen ist die Einheit für die verbrauchte oder erzeugte Wärmemenge (Energie)."
            },
            {
                id: 4,
                abteilung: "Heizung & Wärmepumpen",
                level: "leicht",
                frage: "Was bewirkt ein automatischer Schnellentlüfter am höchsten Punkt einer Heizungsanlage?",
                optionen: [
                    "Er füllt automatisch fehlendes Trinkwasser nach",
                    "Er scheidet angesammelte Luft und Gase selbsttätig aus dem Heizungswasser ab",
                    "Er drosselt den Volumenstrom bei geschlossenen Thermostatventilen",
                    "Er misst die Rücklauftemperatur"
                ],
                richtig: 1,
                erklaerung: "Luft im Heizungssystem verhindert die Zirkulation, verursacht Fließgeräusche und fördert Korrosion. Schnellentlüfter lassen Luftblasen über ein Schwimmerventil entweichen."
            },
            {
                id: 5,
                abteilung: "Heizung & Wärmepumpen",
                level: "leicht",
                frage: "Welche Aufgabe hat ein Schlamm- und Magnetitabscheider im Rücklauf einer modernen Heizungsanlage?",
                optionen: [
                    "Er enthärtet das Trinkwasser vor dem Speicher",
                    "Er schützt Hocheffizienzpumpen und Wärmetauscher vor Verschleiß durch Schmutz und Eisenoxidpartikel",
                    "Er erhöht den Systemdruck um 0,5 bar",
                    "Er wandelt Wechselstrom in Gleichstrom um"
                ],
                richtig: 1,
                erklaerung: "Hocheffizienzpumpen besitzen Permanentmagnete, die Magnetit (schwarzes Eisenoxid) anziehen und blockieren können. Ein Magnetitabscheider hält diese Partikel zurück."
            },
            {
                id: 6,
                abteilung: "Heizung & Wärmepumpen",
                level: "leicht",
                frage: "Was versteht man in der Heizungstechnik unter der ‚Spreizung‘?",
                optionen: [
                    "Den Abstand zwischen zwei Heizkörperhaltern",
                    "Die Temperaturdifferenz zwischen Vorlauf- und Rücklauftemperatur in Kelvin (K)",
                    "Den Druckunterschied vor und nach der Umwälzpumpe",
                    "Die maximale Länge eines Fußbodenheizkreises"
                ],
                richtig: 1,
                erklaerung: "Die Spreizung (ΔT = T_Vorlauf - T_Rücklauf) gibt an, um wie viele Kelvin sich das Heizungswasser beim Durchströmen der Heizflächen abkühlt (z. B. 55 °C Vorlauf / 45 °C Rücklauf = 10 K)."
            },
            {
                id: 7,
                abteilung: "Heizung & Wärmepumpen",
                level: "mittel",
                frage: "In welcher Reihenfolge durchläuft das Kältemittel die vier Hauptkomponenten einer Kompressions-Wärmepumpe?",
                optionen: [
                    "Verdampfer ➔ Verdichter ➔ Verflüssiger ➔ Expansionsventil",
                    "Verdichter ➔ Verdampfer ➔ Expansionsventil ➔ Verflüssiger",
                    "Verflüssiger ➔ Verdichter ➔ Verdampfer ➔ Expansionsventil",
                    "Expansionsventil ➔ Verdampfer ➔ Verflüssiger ➔ Verdichter"
                ],
                richtig: 0,
                erklaerung: "Im Verdampfer nimmt das Kältemittel Umweltwärme auf, der Verdichter komprimiert es auf ein höheres Temperaturniveau, im Verflüssiger gibt es Wärme an das Heizsystem ab und im Expansionsventil wird der Druck wieder abgebaut."
            },
            {
                id: 8,
                abteilung: "Heizung & Wärmepumpen",
                level: "mittel",
                frage: "Was sagt die Jahresarbeitszahl (JAZ) einer Wärmepumpe aus?",
                optionen: [
                    "Die maximale Vorlauftemperatur im Winter",
                    "Das Verhältnis der über ein ganzes Jahr abgegebenen Heizwärme zur eingesetzten elektrischen Energie",
                    "Die Anzahl der Betriebsstunden des Verdichters pro Jahr",
                    "Den Schallleistungspegel der Außeneinheit"
                ],
                richtig: 1,
                erklaerung: "Eine JAZ von 4,0 bedeutet, dass die Wärmepumpe im Jahresdurchschnitt aus 1 kWh elektrischem Strom 4 kWh nutzbare Heizwärme erzeugt hat."
            },
            {
                id: 9,
                abteilung: "Heizung & Wärmepumpen",
                level: "mittel",
                frage: "Warum ist der hydraulische Abgleich bei einer Heizungsanlage (insbesondere bei Brennwertkesseln und Wärmepumpen) unverzichtbar?",
                optionen: [
                    "Damit alle Heizkörper gleich schnell warm werden, keine Strömungsgeräusche entstehen und die Rücklauftemperatur niedrig bleibt",
                    "Damit das Sicherheitsventil im Sommer nicht austrocknet",
                    "Um den Gasanschlussdruck von 20 mbar auf 50 mbar zu erhöhen",
                    "Weil sonst der Schornsteinfeger die Anlage sofort stilllegt"
                ],
                richtig: 0,
                erklaerung: "Ohne hydraulischen Abgleich werden pumpennahe Heizkörper überversorgt und weit entfernte bleiben kalt. Der Abgleich begrenzt die Wassermengen exakt auf den berechneten Wärmebedarf."
            },
            {
                id: 10,
                abteilung: "Heizung & Wärmepumpen",
                level: "mittel",
                frage: "Was beschreibt der Kv-Wert eines Thermostat- oder Strangregulierventils?",
                optionen: [
                    "Den Wasserdurchfluss in m³/h bei einem Druckverlust von genau 1 bar",
                    "Die maximale Umgebungstemperatur des Fühlerelements",
                    "Die zulässige Fließgeschwindigkeit in m/s",
                    "Das Gewicht des Ventilkörpers in Kilogramm"
                ],
                richtig: 0,
                erklaerung: "Der Kv-Wert gibt an, wie viele Kubikmeter Wasser pro Stunde durch das Ventil fließen, wenn die Druckdifferenz über dem Ventil exakt 1 bar (100 kPa) beträgt."
            },
            {
                id: 11,
                abteilung: "Heizung & Wärmepumpen",
                level: "mittel",
                frage: "Welche Aufgabe hat ein Überströmventil in älteren Heizungsanlagen ohne geregelte Pumpe, und warum sollte es bei Hocheffizienzpumpen meist geschlossen bleiben?",
                optionen: [
                    "Es hält einen Mindestvolumenstrom aufrecht; bei geregelten Pumpen würde es jedoch warmes Vorlaufwasser direkt in den Rücklauf leiten und die Effizienz verschlechtern",
                    "Es ersetzt das Membran-Ausdehnungsgefäß bei großen Anlagen",
                    "Es mischt Kaltwasser in den Heizungsvorlauf",
                    "Es entlüftet den Pufferspeicher automatisch"
                ],
                richtig: 0,
                erklaerung: "Ein geöffnetes Überströmventil hebt die Rücklauftemperatur an (schlecht für Brennwertnutzen und Wärmepumpen-COP). Moderne Pumpen regeln ihre Drehzahl selbstständig herunter."
            },
            {
                id: 12,
                abteilung: "Heizung & Wärmepumpen",
                level: "mittel",
                frage: "Welche typische Spreizung (ΔT) wird bei der Auslegung einer Fußbodenheizung angestrebt?",
                optionen: ["5 K bis 8 K", "20 K bis 25 K", "30 K bis 40 K", "0,5 K"],
                richtig: 0,
                erklaerung: "Fußbodenheizungen arbeiten als Flächenheizung mit niedrigen Vorlauftemperaturen (ca. 30–35 °C) und einer geringen Spreizung von meist 5 bis 8 Kelvin, um eine gleichmäßige Oberflächentemperatur zu erreichen."
            },
            {
                id: 13,
                abteilung: "Heizung & Wärmepumpen",
                level: "schwer",
                frage: "Eine Heizungsanlage hat eine statische Höhe von 15 Metern (vom MAG bis zum höchsten Heizkörper). Welcher Vordruck (p0) muss am MAG im kalten, drucklosen Zustand eingestellt werden?",
                optionen: [
                    "1,2 bar",
                    "1,5 bar",
                    "1,7 bis 1,8 bar (p_st = 1,5 bar + 0,2 bis 0,3 bar Zuschlag)",
                    "2,5 bar"
                ],
                richtig: 2,
                erklaerung: "15 m Wassersäule entsprechen 1,5 bar statischem Druck. Um Unterdruck und Lufteintritt am höchsten Punkt sicher zu vermeiden, werden 0,2 bis 0,3 bar addiert (p0 = 1,7–1,8 bar)."
            },
            {
                id: 14,
                abteilung: "Heizung & Wärmepumpen",
                level: "schwer",
                frage: "Warum muss der kalte Anlagendruck (Fülldruck p_A) einer Heizungsanlage etwa 0,3 bar höher sein als der Vordruck (p0) des MAG?",
                optionen: [
                    "Damit das Sicherheitsventil regelmäßig durchgespült wird",
                    "Damit sich im MAG eine Wasservorlage bildet, die geringfügige Wasserverluste oder Entlüftungen ausgleicht",
                    "Weil die Umwälzpumpe mindestens 2 bar Vordruck benötigt",
                    "Um den Siedepunkt des Wassers auf 150 °C anzuheben"
                ],
                richtig: 1,
                erklaerung: "Durch p_A = p0 + 0,3 bar strömt schon im kalten Zustand eine kleine Wassermenge (Wasservorlage) ins MAG. Kühlt die Anlage ab, bleibt der Druck stabil über p0."
            },
            {
                id: 15,
                abteilung: "Heizung & Wärmepumpen",
                level: "schwer",
                frage: "Welche besonderen Sicherheitsanforderungen gelten bei der Außenaufstellung einer Monoblock-Wärmepumpe mit dem natürlichen Kältemittel R290 (Propan)?",
                optionen: [
                    "Im Schutzbereich dürfen sich keine Zündquellen, Kellerfenster, Lichtschächte oder Bodeneinläufe befinden, da R290 hochentzündlich (A3) und schwerer als Luft ist",
                    "R290 ist unbrennbar, benötigt aber einen eigenen Schornstein",
                    "Die Wärmepumpe muss zwingend im Heizungskeller aufgestellt werden",
                    "R290 darf nur bei Außentemperaturen über +5 °C betrieben werden"
                ],
                richtig: 0,
                erklaerung: "R290 (Propan) gehört zur Sicherheitsklasse A3 (hochentzündlich) und sinkt bei einer Leckage zu Boden. Daher ist ein definierter Schutzbereich um die Außeneinheit frei von Öffnungen zu tieferliegenden Räumen zu halten."
            },
            {
                id: 16,
                abteilung: "Heizung & Wärmepumpen",
                level: "schwer",
                frage: "Ein Kunde berichtet: Bei +10 °C Außentemperatur ist die Raumtemperatur ideal, aber bei -12 °C Frost wird es im Haus zu kalt. Wie korrigierst du die Heizkurve?",
                optionen: [
                    "Die Parallelverschiebung (Niveau) absenken",
                    "Die Steilheit (Neigung) der Heizkurve erhöhen",
                    "Die Steilheit der Heizkurve verringern",
                    "Die Sommer-/Winter-Umschalttemperatur auf 25 °C stellen"
                ],
                richtig: 1,
                erklaerung: "Stimmt die Temperatur in der Übergangszeit, sinkt sie aber bei starkem Frost ab, steigt die Vorlauftemperatur bei fallender Außentemperatur nicht stark genug an – die Steilheit muss erhöht werden."
            },
            {
                id: 17,
                abteilung: "Heizung & Wärmepumpen",
                level: "schwer",
                frage: "Welche Anforderung stellt die VDI 2035 Blatt 1 an das Füll- und Ergänzungswasser moderner Heizungsanlagen mit Aluminium-Silizium-Wärmetauschern?",
                optionen: [
                    "Enthärtetes/entsalztes Wasser (niedrige Gesamthärte und elektrische Leitfähigkeit) sowie Einhaltung des zulässigen pH-Wert-Fensters (ca. 8,2–8,5)",
                    "Möglichst hartes Trinkwasser (> 20 °dH), um Kalkschutzschichten aufzubauen",
                    "Zugabe von mindestens 50 % Frostschutzmittel in jedem Einfamilienhaus",
                    "Ein pH-Wert unter 5,0 zur Vermeidung von Algenbildung"
                ],
                richtig: 0,
                erklaerung: "Nach VDI 2035 führt unaufbereitetes hartes Wasser zu Kalkbelägen (Wärmedämmung, Überhitzung) und zu hohe Leitfähigkeit bzw. falsche pH-Werte (> 8,5 bei Aluminium) zu starker Korrosion."
            },
            {
                id: 18,
                abteilung: "Heizung & Wärmepumpen",
                level: "schwer",
                frage: "Wozu dient eine hydraulische Weiche in einer Heizungsanlage mit mehreren gemischten und ungemischten Heizkreisen?",
                optionen: [
                    "Sie entkoppelt den Erzeugerkreis hydraulisch vom Verbraucherkreis, sodass sich die Pumpen nicht gegenseitig beeinflussen",
                    "Sie ersetzt das Dreiwege-Mischventil in der Fußbodenheizung",
                    "Sie dient als Trinkwasser-Pufferspeicher für die Dusche",
                    "Sie reduziert den Gasverbrauch um pauschal 40 %"
                ],
                richtig: 0,
                erklaerung: "Wenn Kesselpumpe und Heizkreispumpen unterschiedliche Volumenströme fördern, verhindert die hydraulische Weiche als druckarmer Verteiler gegenseitige Störungen und Kavitation."
            },

            // =========================================================================
            // ABTEILUNG 2: SANITÄR & TRINKWASSER (18 Fragen: 6 Leicht, 6 Mittel, 6 Schwer)
            // =========================================================================
            {
                id: 19,
                abteilung: "Sanitär & Trinkwasser",
                level: "leicht",
                frage: "Welche Funktion hat ein Geruchsverschluss (Siphon) unter einem Waschbecken oder einer Dusche?",
                optionen: [
                    "Er filtert Haare aus dem Abwasser",
                    "Er bildet durch das Sperrwasser eine gasdichte Barriere gegen Kanalgase aus der Entwässerungsleitung",
                    "Er erhöht die Fließgeschwindigkeit im Fallrohr",
                    "Er verhindert den Rückstau bei Starkregen"
                ],
                richtig: 1,
                erklaerung: "Das im Bogen stehende Sperrwasser (mindestens 50 mm Sperrwasserhöhe) verschließt die Rohrleitung gasdicht, sodass keine übelriechenden oder gesundheitsschädlichen Kanalgase in den Raum gelangen."
            },
            {
                id: 20,
                abteilung: "Sanitär & Trinkwasser",
                level: "leicht",
                frage: "Warum müssen Trinkwasserleitungen für Kaltwasser (PWC) gegen Erwärmung gedämmt werden?",
                optionen: [
                    "Damit das Wasser im Winter im Wohnzimmer nicht gefriert",
                    "Um eine Erwärmung über 25 °C (Legionellenwachstum) und Tauwasserbildung an der Rohroberfläche zu verhindern",
                    "Damit der Wasserdruck nicht abfällt",
                    "Um Kalkablagerungen im Kaltwasserrohr zu beschleunigen"
                ],
                richtig: 1,
                erklaerung: "Kaltwasser soll nach DIN 1988-200 unter 25 °C bleiben. Ohne Dämmung erwärmt es sich in Schächten (Verkeimungsgefahr) und feuchte Raumluft kondensiert am kalten Rohr (Durchfeuchtung)."
            },
            {
                id: 21,
                abteilung: "Sanitär & Trinkwasser",
                level: "leicht",
                frage: "Welche Aufgabe hat der Druckminderer direkt hinter der Wasserzähleranlage?",
                optionen: [
                    "Er reduziert den hohen Versorgungsdruck aus dem Straßennetz auf einen gleichmäßigen, materialschonenden Ruhedruck (meist 3–4 bar)",
                    "Er misst den Warmwasserverbrauch in Kubikmetern",
                    "Er verhindert das Einfrieren der Hauptwasserleitung",
                    "Er reichert das Trinkwasser mit Sauerstoff an"
                ],
                richtig: 0,
                erklaerung: "Ein zu hoher Netzdruck (z. B. 8 bar) verursacht Fließgeräusche, erhöhten Wasserverbrauch und beschädigt Armaturen sowie Sicherheitsventile. Der Druckminderer regelt ihn konstant herunter."
            },
            {
                id: 22,
                abteilung: "Sanitär & Trinkwasser",
                level: "leicht",
                frage: "Warum darf die Ablaufleitung eines Sicherheitsventils am Trinkwassererwärmer niemals fest und dicht mit der Abwasserleitung verbunden werden?",
                optionen: [
                    "Damit das tropfende Ausdehnungswasser sichtbar ist (Funktionskontrolle) und keine Abwasserkeime ins Trinkwasser zurückgesaugt werden können",
                    "Weil Kunststoffrohre kein heißes Wasser vertragen",
                    "Damit der Druck im Speicher schneller sinkt",
                    "Weil sonst der Siphon überläuft"
                ],
                richtig: 0,
                erklaerung: "Der freie Auslauf über einen Ablauftrichter stellt sicher, dass man ein hängendes Ventil sofort erkennt und zwischen Trinkwasseranlage und Schmutzwasser eine sichere Trennung besteht."
            },
            {
                id: 23,
                abteilung: "Sanitär & Trinkwasser",
                level: "leicht",
                frage: "Was versteht man in der Trinkwasserinstallation unter dem Begriff ‚Stagnation‘?",
                optionen: [
                    "Das regelmäßige Spülen aller Zapfstellen",
                    "Den Stillstand von Wasser in Rohrleitungen über einen längeren Zeitraum (z. B. mehr als 72 Stunden)",
                    "Die Zirkulation von Warmwasser im Kreislauf",
                    "Das Entleeren der Anlage vor dem Winter"
                ],
                richtig: 1,
                erklaerung: "Bei Stagnation wird das Wasser nicht ausgetauscht, erwärmt sich auf Umgebungstemperatur und bietet Bakterien (wie Legionellen oder Pseudomonaden) ideale Vermehrungsbedingungen."
            },
            {
                id: 24,
                abteilung: "Sanitär & Trinkwasser",
                level: "leicht",
                frage: "Wie hoch muss die Sperrwasserhöhe bei standardmäßigen Geruchsverschlüssen in der Gebäudeentwässerung nach DIN EN 12056 mindestens sein?",
                optionen: ["10 mm", "25 mm", "50 mm", "150 mm"],
                richtig: 2,
                erklaerung: "Die Mindestsperrwasserhöhe beträgt 50 mm, damit geringfügige Druckschwankungen im Entwässerungssystem den Geruchsverschluss nicht sofort leersaugen."
            },
            {
                id: 25,
                abteilung: "Sanitär & Trinkwasser",
                level: "mittel",
                frage: "Welche Temperaturen schreibt das DVGW-Arbeitsblatt W 551 für Großanlagen zur Trinkwassererwärmung (Speicher > 400 Liter) vor?",
                optionen: [
                    "Speicheraustritt mind. 60 °C; Zirkulationsrücklauf darf um max. 5 K abkühlen (mind. 55 °C)",
                    "Speicheraustritt mind. 48 °C; Zirkulationsrücklauf mind. 40 °C",
                    "Speicheraustritt maximal 50 °C zum Verbrühungsschutz",
                    "Zirkulationspumpe muss nachts 10 Stunden abgeschaltet werden"
                ],
                richtig: 0,
                erklaerung: "Zwischen 25 °C und 50 °C vermehren sich Legionellen optimal. Ab 60 °C sterben sie ab. Daher müssen am Speicheraustritt mind. 60 °C und im Zirkulationsrücklauf mind. 55 °C gehalten werden."
            },
            {
                id: 26,
                abteilung: "Sanitär & Trinkwasser",
                level: "mittel",
                frage: "Welches Mindestgefälle wird für erdverlegte Schmutzwasser-Grundleitungen (DN 100) nach DIN 1986-100 gefordert?",
                optionen: [
                    "0,2 % (2 mm pro Meter)",
                    "1,0 % bis 2,0 % (1 bis 2 cm pro Meter, mind. 1 : DN)",
                    "8,0 % (8 cm pro Meter)",
                    "Bei glatten KG-Rohren ist kein Gefälle erforderlich"
                ],
                richtig: 1,
                erklaerung: "Bei DN 100 beträgt das Mindestgefälle 1:100 = 1 % (1 cm pro Meter), üblich sind 1–2 %. Ist das Gefälle zu groß, fließt das Wasser zu schnell ab und Feststoffe bleiben liegen."
            },
            {
                id: 27,
                abteilung: "Sanitär & Trinkwasser",
                level: "mittel",
                frage: "Wozu dienen Lüftungsleitungen (Hauptlüftung über Dach) in einem Schmutzwasser-Fallleitungssystem?",
                optionen: [
                    "Zum Druckausgleich beim Spülen, damit Geruchsverschlüsse weder leergesaugt (Unterdruck) noch ausgeblasen (Überdruck) werden",
                    "Zur Beheizung des Dachbodens",
                    "Zur Ableitung von Regenwasser in das Schmutzwassernetz",
                    "Zur Schalldämmung der Wasserzähler"
                ],
                richtig: 0,
                erklaerung: "Fällt eine große Wassermenge (z. B. WC-Spülung) im Fallrohr nach unten, entsteht dahinter Unterdruck und davor Überdruck. Die Lüftung über Dach gleicht diesen Druck sofort aus."
            },
            {
                id: 28,
                abteilung: "Sanitär & Trinkwasser",
                level: "mittel",
                frage: "Was besagt die ‚3-Liter-Regel‘ nach DVGW W 551 bei Warmwasserleitungen ohne Zirkulation?",
                optionen: [
                    "Das Wasservolumen in der Leitung zwischen Trinkwassererwärmer und entferntester Zapfstelle darf maximal 3 Liter betragen",
                    "Ein Warmwasserspeicher darf maximal 3 Liter Inhalt haben",
                    "Pro Minute dürfen höchstens 3 Liter Warmwasser aus dem Duschkopf fließen",
                    "Die Zirkulationspumpe darf maximal 3 Watt Leistung aufnehmen"
                ],
                richtig: 0,
                erklaerung: "Beträgt der Leitungsinhalt höchstens 3 Liter, wird das abgekühlte Wasser beim Öffnen der Armatur schnell ausgespült, sodass keine Zirkulationsleitung zwingend erforderlich ist."
            },
            {
                id: 29,
                abteilung: "Sanitär & Trinkwasser",
                level: "mittel",
                frage: "Welche Dämmstärken gelten nach Gebäudeenergiegesetz (GEG) für Warmwasser- und Zirkulationsleitungen im unbeheizten Keller?",
                optionen: [
                    "100 % Dämmschichtdicke (entspricht dem Innendurchmesser der Leitung, z. B. 20 mm bei DN 20)",
                    "Grundsätzlich nur 4 mm Schutzschlauch",
                    "Keine Dämmung erforderlich",
                    "Mindestens 200 mm Mineralwolle"
                ],
                richtig: 0,
                erklaerung: "Nach GEG müssen Warmwasser- und Zirkulationsleitungen in unbeheizten Räumen mit 100 % Dämmschichtdicke (bezogen auf Wärmeleitfähigkeit 0,035 W/(m·K)) gedämmt werden, um Auskühlung und Legionellenbildung zu verhindern."
            },
            {
                id: 30,
                abteilung: "Sanitär & Trinkwasser",
                level: "mittel",
                frage: "Was ist die Rückstauebene in der Grundstücksentwässerung nach DIN 1986-100?",
                optionen: [
                    "Die höchste Stelle, bis zu der das Abwasser im öffentlichen Kanal bei Starkregen ansteigen kann (in der Regel die Straßenoberkante an der Anschlussstelle)",
                    "Die Sohle des tiefsten Kellerraums",
                    "Die Höhe des Dachfirstes",
                    "Der Wasserstand im Hauswasserzähler"
                ],
                richtig: 0,
                erklaerung: "Alle Entwässerungsgegenstände (z. B. Keller-WC, Waschmaschine), die unterhalb der Rückstauebene liegen, müssen gegen Rückstau aus dem Kanal (z. B. durch Hebeanlage oder Rückstauverschluss) gesichert werden."
            },
            {
                id: 31,
                abteilung: "Sanitär & Trinkwasser",
                level: "schwer",
                frage: "Welche Sicherungseinrichtung nach DIN EN 1717 ist zum Schutz des Trinkwassers erforderlich, wenn eine Heizungsanlage (Flüssigkeitskategorie 3 oder 4 mit Inhibitoren) fest angeschlossen wird?",
                optionen: [
                    "Ein einfacher Rückflussverhinderer (Typ EA)",
                    "Ein Systemtrenner (z. B. Typ BA für Kategorie 4 bzw. Typ CA für Kategorie 3)",
                    "Ein Rohrunterbrecher Typ DC",
                    "Ein Schmutzfänger mit Magnetstab"
                ],
                richtig: 1,
                erklaerung: "Heizungswasser mit Zusätzen (Inhibitoren/Frostschutz) gehört zur Flüssigkeitskategorie 4. Nach DIN EN 1717 ist zum Schutz des Trinkwassers mindestens ein Systemtrenner Typ BA mit kontrollierbarer Mitteldruckzone vorgeschrieben."
            },
            {
                id: 32,
                abteilung: "Sanitär & Trinkwasser",
                level: "schwer",
                frage: "Wie muss eine nicht mehr genutzte Trinkwasserleitung (Totleitung) nach DIN 1988-200 fachgerecht außer Betrieb genommen werden?",
                optionen: [
                    "Einfach das Absperrventil schließen und einen Stopfen aufschrauben",
                    "Unmittelbar an der durchströmten Haupt- oder Verteilleitung abtrennen (T-Stück ausbauen und durch Kupplung ersetzen)",
                    "Mit Druckluft ausblasen und das Ventil offen lassen",
                    "Nur mit einem Hinweisschild ‚Außer Betrieb‘ versehen"
                ],
                richtig: 1,
                erklaerung: "Abgesperrte Stichleitungen (Totleitungen) sind Brutstätten für Legionellen und kontaminieren das gesamte Netz. Sie müssen direkt am Abzweig der durchströmten Leitung rückgebaut werden."
            },
            {
                id: 33,
                abteilung: "Sanitär & Trinkwasser",
                level: "schwer",
                frage: "Was versteht man bei der Dimensionierung von Trinkwasserleitungen nach DIN 1988-300 unter dem ‚Spitzendurchfluss‘ (Vs)?",
                optionen: [
                    "Die Summe aller Berechnungsdurchflüsse (ΣVR) aller im Gebäude eingebauten Armaturen",
                    "Den maximal zu erwartenden Gleichzeitigkeits-Volumenstrom unter Berücksichtigung der Nutzungswahrscheinlichkeit",
                    "Den Durchfluss bei einem Rohrbruch",
                    "Die Mindestfließmenge des Wasserzählers"
                ],
                richtig: 1,
                erklaerung: "Da in einem Gebäude niemals alle Zapfstellen gleichzeitig voll geöffnet sind, wird aus dem Summendurchfluss (ΣVR) mittels Gleichzeitigkeitskurven der realistische Spitzendurchfluss (Vs) berechnet."
            },
            {
                id: 34,
                abteilung: "Sanitär & Trinkwasser",
                level: "schwer",
                frage: "Welche Flüssigkeitskategorie nach DIN EN 1717 beschreibt Wasser, das eine Gesundheitsgefährdung für Menschen durch die Anwesenheit einer oder mehrerer giftiger oder besonders giftiger Stoffe darstellt (z. B. Heizungswasser mit Inhibitoren)?",
                optionen: ["Kategorie 1", "Kategorie 2", "Kategorie 3", "Kategorie 4"],
                richtig: 3,
                erklaerung: "Kategorie 1 = Trinkwasser; Kategorie 2 = geschmacklich/temperaturverändert; Kategorie 3 = gesundheitsgefährdend (z. B. reines Heizungswasser ohne Zusätze); Kategorie 4 = giftige/krebserregende Stoffe (z. B. Heizungswasser mit Inhibitoren); Kategorie 5 = Krankheitserreger (z. B. Regenwasser/Fäkalien)."
            },
            {
                id: 35,
                abteilung: "Sanitär & Trinkwasser",
                level: "schwer",
                frage: "Wann ist für einen fäkalienhaltigen Ablauf (WC) unterhalb der Rückstauebene nach DIN 1986-100 ausnahmsweise ein Rückstauverschluss statt einer Hebeanlage zulässig?",
                optionen: [
                    "Nur bei untergeordneter Nutzung (z. B. Einlieger-WC im Keller), wenn ein weiteres WC oberhalb der Rückstauebene vorhanden ist und der Benutzerkreis klein ist",
                    "Immer, wenn das Abwasserrohr mindestens DN 150 hat",
                    "Niemals, für WCs sind Rückstauverschlüsse generell verboten",
                    "Nur in Gewerbe- und Industriebetrieben"
                ],
                richtig: 0,
                erklaerung: "Grundsätzlich gilt für Räume unterhalb der Rückstauebene die Hebeanlage als Standard. Ein automatischer Rückstauverschluss (Typ 3) ist nur zulässig, wenn kein wesentlicher Sachwert gefährdet ist, oben ein weiteres WC existiert und bei Rückstau auf das Keller-WC verzichtet werden kann."
            },
            {
                id: 36,
                abteilung: "Sanitär & Trinkwasser",
                level: "schwer",
                frage: "Warum werden in modernen Trinkwasser-Stockwerksleitungen häufig Reihen- oder Ringleitungen statt klassischer T-Stück-Verteilungen installiert?",
                optionen: [
                    "Um durch das Durchschleifen von selten genutzten Zapfstellen (z. B. Gäste-WC) zu häufig genutzten (z. B. WC/Waschtisch) einen regelmäßigen Wasseraustausch sicherzustellen",
                    "Weil T-Stücke in Deutschland verboten sind",
                    "Um den Fließdruck an der letzten Armatur auf 10 bar zu steigern",
                    "Weil dadurch keine Rohrschellen mehr benötigt werden"
                ],
                richtig: 0,
                erklaerung: "In Reihen- oder Ringleitungen wird das Wasser bei jeder Nutzung der Hauptarmatur automatisch durch die gesamte Leitung gespült – Stagnation wird konstruktiv vermieden."
            },

            // =========================================================================
            // ABTEILUNG 3: GAS & ABGAS (17 Fragen: 6 Leicht, 6 Mittel, 5 Schwer)
            // =========================================================================
            {
                id: 37,
                abteilung: "Gas & Abgas",
                level: "leicht",
                frage: "Welche Prüfdrücke gelten nach DVGW-TRGI bei der Prüfung einer neu verlegten Gasleitung (Betriebsdruck bis 100 mbar)?",
                optionen: [
                    "Belastungsprüfung: mind. 3 bar (oder 1 bar je nach Bauteil) • Dichtheitsprüfung: 150 mbar",
                    "Belastungsprüfung: 50 mbar • Dichtheitsprüfung: 20 mbar",
                    "Belastungsprüfung: 10 bar • Dichtheitsprüfung: 5 bar",
                    "Es reicht eine Sichtprüfung mit Seifenwasser"
                ],
                richtig: 0,
                erklaerung: "Nach DVGW-TRGI wird zuerst die Belastungsprüfung (Festigkeit, meist 3 bar bzw. 1 bar bei eingebauten Armaturen) und danach die Dichtheitsprüfung mit 150 mbar durchgeführt."
            },
            {
                id: 38,
                abteilung: "Gas & Abgas",
                level: "leicht",
                frage: "Wie hoch ist der übliche Anschlussdruck (Fließdruck) von Erdgas im Niederdrucknetz am Hausanschluss?",
                optionen: ["20 mbar (zulässiger Bereich ca. 18–25 mbar)", "150 mbar", "1,5 bar", "4,0 bar"],
                richtig: 0,
                erklaerung: "Im deutschen Erdgas-Niederdrucknetz beträgt der Nenn-Anschlussdruck nach dem Gas-Druckregelgerät 20 mbar."
            },
            {
                id: 39,
                abteilung: "Gas & Abgas",
                level: "leicht",
                frage: "Welche Aufgabe hat der Gasströmungswächter (GS) in einer Gasinstallation?",
                optionen: [
                    "Er sperrt die Gaszufuhr selbsttätig ab, wenn der Volumenstrom durch eine Beschädigung oder Manipulation der Leitung unzulässig ansteigt",
                    "Er misst den monatlichen Gasverbrauch für den Versorger",
                    "Er erwärmt das Erdgas im Winter vor dem Brenner",
                    "Er mischt dem Erdgas den typischen Warngeruch (Odorierung) bei"
                ],
                richtig: 0,
                erklaerung: "Der Gasströmungswächter ist eine aktive Sicherheitseinrichtung: Reißt eine Leitung ab oder wird ein Stopfen entfernt, schließt der GS durch den plötzlichen Druckabfall sofort."
            },
            {
                id: 40,
                abteilung: "Gas & Abgas",
                level: "leicht",
                frage: "Warum wird Erdgas (das von Natur aus geruchlos ist) vom Gasnetzbetreiber odoriert?",
                optionen: [
                    "Damit austretendes Gas bereits bei geringen Konzentrationen weit unterhalb der unteren Explosionsgrenze (UEG) durch den Geruchssinn wahrgenommen wird",
                    "Um den Heizwert des Gases zu erhöhen",
                    "Um Korrosion in Kupferrohren zu verhindern",
                    "Damit die Flamme blau statt gelb brennt"
                ],
                richtig: 0,
                erklaerung: "Odoriermittel verleihen dem Gas einen intensiven Warngeruch (ähnlich faulen Eiern/Lösungsmittel), sodass Leckagen lange vor Erreichen eines zündfähigen Gas-Luft-Gemisches bemerkt werden."
            },
            {
                id: 41,
                abteilung: "Gas & Abgas",
                level: "leicht",
                frage: "Was unterscheidet eine raumluftabhängige (Art B) von einer raumluftunabhängigen (Art C) Gasfeuerstätte?",
                optionen: [
                    "Art B entnimmt die Verbrennungsluft dem Aufstellraum; Art C bezieht die Verbrennungsluft über ein dichtes System (z. B. LAS) direkt von außen",
                    "Art B läuft mit Flüssiggas, Art C nur mit Erdgas",
                    "Art B benötigt keinen Schornstein",
                    "Art C darf nur im Freien montiert werden"
                ],
                richtig: 0,
                erklaerung: "Raumluftunabhängige Geräte (Art C, z. B. Brennwertthermen mit Luft-Abgas-System LAS) sind dicht gegenüber dem Aufstellraum und ziehen ihre Luft direkt von draußen."
            },
            {
                id: 42,
                abteilung: "Gas & Abgas",
                level: "leicht",
                frage: "Welche Farbe haben Gasleitungen und Gasarmaturen in Gebäuden zur eindeutigen Kennzeichnung in der Regel?",
                optionen: ["Gelb", "Blau", "Grün", "Violett"],
                richtig: 0,
                erklaerung: "Nach DIN 2403 ist Gelb die Kennfarbe für brennbare Gase (wie Erdgas oder Flüssiggas)."
            },
            {
                id: 43,
                abteilung: "Gas & Abgas",
                level: "mittel",
                frage: "Welcher maximale Abgasverlust (qA) ist nach 1. BImSchV für bestehende Gas- und Ölheizkessel bis 25 kW Nennwärmeleistung zulässig?",
                optionen: ["Maximal 9 %", "Maximal 10 %", "Maximal 11 %", "Maximal 14 %"],
                richtig: 2,
                erklaerung: "Nach 1. BImSchV gelten als Obergrenze für den Abgasverlust: 4–25 kW = max. 11 %, >25–50 kW = max. 10 %, >50 kW = max. 9 %."
            },
            {
                id: 44,
                abteilung: "Gas & Abgas",
                level: "mittel",
                frage: "Was prüft der Schornsteinfeger bzw. Servicetechniker bei der ‚Ringspaltmessung‘ an einem raumluftunabhängigen Brennwertgerät mit Luft-Abgas-System (LAS)?",
                optionen: [
                    "Ob der Sauerstoffgehalt (O2) im Zuluft-Ringspalt auf eine Undichtigkeit des inneren Abgasrohres hinweist",
                    "Die Wandstärke des äußeren Kunststoffrohres",
                    "Den Wasserdruck im Ausdehnungsgefäß",
                    "Die elektrische Spannung an der Ionisationselektrode"
                ],
                richtig: 0,
                erklaerung: "Ist das innere Abgasrohr im LAS undicht, gelangt Abgas in die angesaugte Verbrennungsluft im Ringspalt – der O2-Gehalt im Ringspalt sinkt deutlich unter 20,6 % (bzw. CO2 steigt an)."
            },
            {
                id: 45,
                abteilung: "Gas & Abgas",
                level: "mittel",
                frage: "Wie viel Verbrennungsluft benötigt ein atmosphärischer Gasbrenner etwa für die vollständige Verbrennung von 1 m³ Erdgas?",
                optionen: [
                    "Ca. 1 m³ Luft",
                    "Ca. 10 m³ Luft (plus Luftüberschuss)",
                    "Ca. 50 m³ Luft",
                    "Erdgas verbrennt ohne Sauerstoff"
                ],
                richtig: 1,
                erklaerung: "Für 1 m³ Erdgas werden stöchiometrisch rund 9,5 bis 10 m³ Luft benötigt. Mit dem nötigen Luftüberschuss (λ ≈ 1,2–1,3) sind es etwa 11–13 m³ Luft pro m³ Gas."
            },
            {
                id: 46,
                abteilung: "Gas & Abgas",
                level: "mittel",
                frage: "Wann gilt eine bestehende Gasleitung bei der Gebrauchsfähigkeitsprüfung nach DVGW-TRGI als ‚uneingeschränkt gebrauchsfähig‘?",
                optionen: [
                    "Wenn die Leckrate unter 1 Liter pro Stunde (l/h) bei Betriebsdruck liegt",
                    "Wenn die Leckrate zwischen 1 l/h und 5 l/h liegt",
                    "Wenn die Leckrate unter 50 l/h liegt",
                    "Wenn kein Gasgeruch im Keller wahrnehmbar ist"
                ],
                richtig: 0,
                erklaerung: "Nach TRGI: Leckrate < 1 l/h = uneingeschränkt gebrauchsfähig; 1 bis < 5 l/h = vermindert gebrauchsfähig (Instandsetzung binnen 4 Wochen); ≥ 5 l/h = nicht gebrauchsfähig (sofortige Außerbetriebnahme)."
            },
            {
                id: 47,
                abteilung: "Gas & Abgas",
                level: "mittel",
                frage: "Warum ist der gleichzeitige Betrieb einer raumluftabhängigen Gasfeuerstätte (z. B. Gasherd oder Gastherme Art B) und einer Abluft-Dunstabzugshaube ohne Sicherheitsschaltung lebensgefährlich?",
                optionen: [
                    "Die Dunstabzugshaube erzeugt im Raum Unterdruck, wodurch giftige Abgase inklusive Kohlenmonoxid (CO) aus dem Schornstein in den Wohnraum zurückgesaugt werden können",
                    "Die Dunstabzugshaube kühlt das Abgas im Schornstein zu stark ab",
                    "Der Gaszähler dreht sich dadurch rückwärts",
                    "Die Flamme am Gasherd wird zu heiß"
                ],
                richtig: 0,
                erklaerung: "Erzeugt eine Abluftanlage mehr als 4 Pa Unterdruck, kehrt sich der Schornsteinzug um – tödliches Kohlenmonoxid strömt in die Wohnung. Abhilfe schafft z. B. ein Fensterkontaktschalter."
            },
            {
                id: 48,
                abteilung: "Gas & Abgas",
                level: "mittel",
                frage: "Welche Aufgabe hat die thermische Absperreinrichtung (TAE) vor Gaszählern und Gasgeräten?",
                optionen: [
                    "Sie schließt bei einem Gebäudebrand (ab ca. 92–100 °C) selbsttätig und verhindert das Ausströmen von Gas ins Feuer",
                    "Sie regelt die Vorlauftemperatur des Heizkessels",
                    "Sie schaltet das Gerät bei Frost ab",
                    "Sie verhindert den Rückfluss von Kondensat"
                ],
                richtig: 0,
                erklaerung: "Bei Erreichen der Auslösetemperatur schmilzt ein Lotglied in der TAE, sodass ein Federventil die Gasleitung dauerhaft absperrt."
            },
            {
                id: 49,
                abteilung: "Gas & Abgas",
                level: "schwer",
                frage: "Warum liegt der Abgas-Taupunkt bei der Verbrennung von Erdgas H (ca. 57 °C) höher als bei Heizöl EL (ca. 47 °C)?",
                optionen: [
                    "Weil Erdgas (CH4) im Verhältnis zum Kohlenstoff mehr Wasserstoff enthält, wodurch bei der Verbrennung mehr Wasserdampf entsteht",
                    "Weil Erdgas mit höherem Druck verbrannt wird",
                    "Weil Heizöl keinen Wasserstoff enthält",
                    "Weil Erdgaskessel immer kleinere Schornsteine haben"
                ],
                richtig: 0,
                erklaerung: "Je höher der Wasserstoffanteil im Brennstoff, desto höher der Wasserdampf-Partialdruck im Abgas – und desto früher (bei höheren Temperaturen) kondensiert der Wasserdampf."
            },
            {
                id: 50,
                abteilung: "Gas & Abgas",
                level: "schwer",
                frage: "Welcher freie Querschnitt wird nach DVGW-TRGI für Verbrennungsluft-Öffnungen (z. B. Überströmöffnungen in Türen oder Außenluftöffnungen) bei raumluftabhängigen Gasgeräten bis 50 kW mindestens gefordert?",
                optionen: [
                    "Mindestens 150 cm² (oder 2 × 75 cm²)",
                    "Mindestens 10 cm²",
                    "Mindestens 500 cm²",
                    "Mindestens 1.000 cm²"
                ],
                richtig: 0,
                erklaerung: "Nach DVGW-TRGI sind für Verbrennungsluftöffnungen bis 50 kW Nennwärmeleistung mindestens 150 cm² freier Querschnitt (bei zwei Öffnungen je mindestens 75 cm²) erforderlich."
            },
            {
                id: 51,
                abteilung: "Gas & Abgas",
                level: "schwer",
                frage: "Welche Eigenschaft von Flüssiggas (Propan/Butan) erfordert bei der Installation in Räumen unter Erdgleiche besondere Vorsichtsmaßnahmen?",
                optionen: [
                    "Flüssiggas ist etwa 1,5- bis 2-mal schwerer als Luft und sammelt sich bei Leckagen am Boden sowie in Kellern und Schächten",
                    "Flüssiggas steigt sofort an die Zimmerdecke",
                    "Flüssiggas ist nicht brennbar, verdrängt aber den Stickstoff",
                    "Flüssiggas löst Kupferrohre chemisch auf"
                ],
                richtig: 0,
                erklaerung: "Im Gegensatz zu Erdgas (leichter als Luft) sinkt Flüssiggas zu Boden und bildet dort explosive Gas-Luft-Gemische. Deshalb sind Absperrarmaturen und Rohrverbindungen unter Erdgleiche streng reglementiert."
            },
            {
                id: 52,
                abteilung: "Gas & Abgas",
                level: "schwer",
                frage: "Warum muss das saure Kondensat aus Öl-Brennwertkesseln (und bei größeren Gas-Brennwertanlagen > 200 kW) nach ATV-DVWK-A 251 vor der Einleitung in die Kanalisation neutralisiert werden?",
                optionen: [
                    "Weil der niedrige pH-Wert (ca. 2–4 bei Öl, ca. 4–5 bei Gas) Beton- und Gussrohre der Kanalisation angreift und zerstört",
                    "Weil das Kondensat sonst im Siphon gefriert",
                    "Weil Kondensat brennbar ist",
                    "Um den Trinkwasser-pH-Wert zu senken"
                ],
                richtig: 0,
                erklaerung: "Das Kondensat enthält schweflige Säure, Salpetersäure bzw. Kohlensäure. In einer Neutralisationsbox (z. B. mit Magnesiumoxid-Granulat) wird der pH-Wert auf über 6,5 angehoben."
            },
            {
                id: 53,
                abteilung: "Gas & Abgas",
                level: "schwer",
                frage: "Was versteht man unter der ‚Wobbe-Zahl‘ eines Brenngases?",
                optionen: [
                    "Ein Maß für die Austauschbarkeit von Brenngasen hinsichtlich der Wärmebelastung eines Gasbrenners bei gleichem Anschlussdruck",
                    "Die maximale Temperatur der Zündflamme",
                    "Den Schwefelgehalt im Erdgas",
                    "Die Strömungsgeschwindigkeit im Schornstein"
                ],
                richtig: 0,
                erklaerung: "Gase mit gleicher Wobbe-Zahl (Quotient aus Heizwert/Brennwert und der Wurzel aus der relativen Dichte) liefern an derselben Brennerdüse bei gleichem Druck die gleiche Wärmebelastung."
            },

            // =========================================================================
            // ABTEILUNG 4: LÜFTUNG & KLIMA (16 Fragen: 5 Leicht, 6 Mittel, 5 Schwer)
            // =========================================================================
            {
                id: 54,
                abteilung: "Lüftung & Klima",
                level: "leicht",
                frage: "Warum ist in modernen, luftdicht gedämmten Gebäuden eine kontrollierte Wohnraumlüftung (KWL) besonders wichtig?",
                optionen: [
                    "Weil über Undichtigkeiten an Fenstern kaum noch Luftaustausch stattfindet und sonst Feuchtigkeit und Schimmel entstehen",
                    "Weil dichte Fenster den Wasserdruck im Bad senken",
                    "Damit die Heizkörper schneller abkühlen",
                    "Weil sonst der Schornstein nicht zieht"
                ],
                richtig: 0,
                erklaerung: "Durch die luftdichte Gebäudehülle nach GEG wird Feuchtigkeit (durch Duschen, Kochen, Atmen) nicht mehr unkontrolliert abgeführt – ohne gezielte Lüftung droht Schimmelpilzbefall."
            },
            {
                id: 55,
                abteilung: "Lüftung & Klima",
                level: "leicht",
                frage: "Welche Aufgabe hat der Wärmerückgewinnungs-Wärmetauscher (WRG) in einer zentralen Lüftungsanlage?",
                optionen: [
                    "Er überträgt die Wärme der verbrauchten Abluft auf die kalte, frische Außenluft, ohne dass sich beide Luftströme vermischen",
                    "Er kühlt die Abluft mit Trinkwasser ab",
                    "Er filtert Feinstaub aus der Raumluft",
                    "Er erzeugt Strom für die Ventilatoren"
                ],
                richtig: 0,
                erklaerung: "Kreuz-Gegenstrom-Wärmetauscher gewinnen bis zu 90 % der Wärme aus der Abluft zurück und sparen so erheblich Heizenergie."
            },
            {
                id: 56,
                abteilung: "Lüftung & Klima",
                level: "leicht",
                frage: "In welcher Einheit wird der Luftvolumenstrom einer Lüftungsanlage üblicherweise angegeben?",
                optionen: ["Kubikmeter pro Stunde (m³/h)", "Liter pro Sekunde (l/s) nur bei Gas", "Pascal (Pa)", "Kilowatt (kW)"],
                richtig: 0,
                erklaerung: "In der Lüftungstechnik wird der Volumenstrom standardmäßig in m³/h (Kubikmeter pro Stunde) angegeben."
            },
            {
                id: 57,
                abteilung: "Lüftung & Klima",
                level: "leicht",
                frage: "Wie verläuft die Luftströmung in einer korrekt geplanten Wohnungslüftung?",
                optionen: [
                    "Zuluft in Aufenthaltsräume (Wohn-, Schlaf-, Kinderzimmer) ➔ Überströmbereich (Flur) ➔ Abluft aus Feucht-/Geruchsräumen (Bad, WC, Küche)",
                    "Zuluft ins Bad und WC ➔ Abluft aus dem Schlafzimmer",
                    "Zuluft und Abluft ausschließlich im Flur",
                    "Abluft nur im Keller"
                ],
                richtig: 0,
                erklaerung: "Frische Luft strömt in die Wohn- und Schlafräume, fließt über Türspalte (Überströmöffnungen) in den Flur und wird in Küche, Bad und WC abgesaugt, damit sich Gerüche und Feuchte nicht in der Wohnung verteilen."
            },
            {
                id: 58,
                abteilung: "Lüftung & Klima",
                level: "leicht",
                frage: "Warum müssen Luftfilter in einer Lüftungsanlage regelmäßig kontrolliert und gewechselt werden?",
                optionen: [
                    "Weil verschmutzte Filter den Druckverlust erhöhen (mehr Stromverbrauch), den Luftvolumenstrom senken und hygienische Probleme verursachen",
                    "Damit das Kältemittel nicht entweicht",
                    "Weil sonst der Wärmetauscher einfriert",
                    "Damit die Raumtemperatur nicht über 30 °C steigt"
                ],
                richtig: 0,
                erklaerung: "Zugesetzte Filter zwingen die Ventilatoren zu höherer Drehzahl, senken die Luftqualität und können bei Feuchtigkeit verkeimen."
            },
            {
                id: 59,
                abteilung: "Lüftung & Klima",
                level: "mittel",
                frage: "Welche vier Lüftungsstufen legt die DIN 1946-6 für die Wohnungslüftung fest?",
                optionen: [
                    "Lüftung zum Feuchteschutz, Reduzierte Lüftung, Nennlüftung und Intensivlüftung",
                    "Nachtlüftung, Taglüftung, Stoßlüftung und Dauerlüftung",
                    "Stufe 1 (Frost), Stufe 2 (Eco), Stufe 3 (Komfort), Stufe 4 (Turbo)",
                    "Sommerbetrieb, Winterbetrieb, Übergangsbetrieb, Urlaubsbetrieb"
                ],
                richtig: 0,
                erklaerung: "Die DIN 1946-6 definiert: 1. Feuchteschutz (nutzerunabhängiger Bautenschutz), 2. Reduzierte Lüftung (Abwesenheit), 3. Nennlüftung (Normalbetrieb) und 4. Intensivlüftung (Lastspitzen)."
            },
            {
                id: 60,
                abteilung: "Lüftung & Klima",
                level: "mittel",
                frage: "Welche Aufgabe hat eine Brandschutzklappe (BSK) in einer Lüftungsleitung, die durch eine Brandwand führt?",
                optionen: [
                    "Sie schließt im Brandfall (z. B. durch Schmelzlot bei 72 °C oder Rauchmelder) selbsttätig und verhindert die Ausbreitung von Feuer und Rauch in den nächsten Brandabschnitt",
                    "Sie regelt den Luftvolumenstrom bei starkem Wind",
                    "Sie verhindert Kondensatbildung im Lüftungskanal",
                    "Sie dämpft Ventilatorgeräusche um 50 dB"
                ],
                richtig: 0,
                erklaerung: "Durchdringt eine Lüftungsleitung feuerwiderstandsfähige Wände oder Decken (F90), muss eine zugelassene Brandschutzklappe den Luftweg im Brandfall feuer- und rauchdicht verschließen."
            },
            {
                id: 61,
                abteilung: "Lüftung & Klima",
                level: "mittel",
                frage: "Warum müssen Außenluft- und Fortluftleitungen einer zentralen Lüftungsanlage innerhalb der beheizten Gebäudehülle diffusionsdicht (dampfdicht) gedämmt werden?",
                optionen: [
                    "Weil in den kalten Rohren im Winter sonst Raumluftfeuchtigkeit auf der Rohraußenseite kondensiert und zu Bauschäden führt",
                    "Um den Luftdruck im Kanal zu erhöhen",
                    "Damit keine Mäuse in das Rohr gelangen",
                    "Weil Kunststoffrohre sonst UV-Strahlung abgeben"
                ],
                richtig: 0,
                erklaerung: "Außenluft (-10 °C) und Fortluft (ca. 0 °C) sind deutlich kälter als die warme Raumluft (+21 °C). Ohne geschlossenzellige, dampfdichte Dämmung bildet sich sofort Schwitzwasser."
            },
            {
                id: 62,
                abteilung: "Lüftung & Klima",
                level: "mittel",
                frage: "Was leistet ein Enthalpie-Wärmetauscher im Vergleich zu einem Standard-Wärmetauscher in einer Lüftungsanlage?",
                optionen: [
                    "Er überträgt neben der Wärme auch einen Teil der Luftfeuchtigkeit aus der Abluft auf die trockene Winter-Zuluft",
                    "Er kühlt die Zuluft im Sommer aktiv wie eine Klimaanlage",
                    "Er verbrennt Geruchsstoffe katalytisch",
                    "Er arbeitet ohne Stromanschluss"
                ],
                richtig: 0,
                erklaerung: "Durch eine spezielle Polymermembran lässt der Enthalpie-Wärmetauscher Wasserdampfmoleküle passieren (hygienisch getrennt von Gerüchen) und beugt so zu trockener Heizungsluft im Winter vor."
            },
            {
                id: 63,
                abteilung: "Lüftung & Klima",
                level: "mittel",
                frage: "Wie berechnet sich der benötigte Luftvolumenstrom (V̇) bei einer gegebenen Strömungsgeschwindigkeit (v) und Kanalquerschnittsfläche (A)?",
                optionen: [
                    "V̇ = A × v (Volumenstrom = Querschnittsfläche × Strömungsgeschwindigkeit)",
                    "V̇ = A / v",
                    "V̇ = v² × A",
                    "V̇ = A + v"
                ],
                richtig: 0,
                erklaerung: "Die Kontinuitätsgleichung besagt: Volumenstrom V̇ [m³/s] = Fläche A [m²] × Geschwindigkeit v [m/s] (multipliziert mit 3600 ergibt m³/h)."
            },
            {
                id: 64,
                abteilung: "Lüftung & Klima",
                level: "mittel",
                frage: "Was versteht man unter dem ‚Coandă-Effekt‘ bei Zuluft-Deckenauslässen?",
                optionen: [
                    "Das Anlegen des eingeblasenen Luftstrahls an die Zimmerdecke, wodurch sich die Zuluft zugfrei mit der Raumluft vermischt, bevor sie in den Aufenthaltsbereich absinkt",
                    "Das Rückströmen von Abluft in den Ventilator",
                    "Die Vereisung des Wärmetauschers bei Minusgraden",
                    "Die Schallübertragung über Lüftungsrohre (Telefonie-Schall)"
                ],
                richtig: 0,
                erklaerung: "Dank des Coandă-Effekts strömt die kühle Zuluft zunächst an der Decke entlang und wärmt sich durch Induktion auf, sodass keine unangenehme Zugluft entsteht."
            },
            {
                id: 65,
                abteilung: "Lüftung & Klima",
                level: "schwer",
                frage: "Was passiert mit der relativen Luftfeuchtigkeit (φ), wenn kalte Außenluft (z. B. 0 °C, 80 % relative Feuchte) ohne Befeuchtung auf 21 °C Raumtemperatur erwärmt wird?",
                optionen: [
                    "Die relative Luftfeuchtigkeit sinkt stark ab (auf ca. 20 %), weil warme Luft deutlich mehr Wasserdampf aufnehmen kann als kalte Luft",
                    "Die relative Luftfeuchtigkeit steigt auf 100 % an",
                    "Die relative Luftfeuchtigkeit bleibt exakt bei 80 %",
                    "Der absolute Wassergehalt in g/kg verdoppelt sich"
                ],
                richtig: 0,
                erklaerung: "Die absolute Wassermenge (in g/kg trockener Luft) bleibt beim reinen Erwärmen gleich. Da das maximale Wasseraufnahmevermögen der Luft bei 21 °C aber viel höher ist, sinkt die relative Feuchte dramatisch."
            },
            {
                id: 66,
                abteilung: "Lüftung & Klima",
                level: "schwer",
                frage: "Welche Information lässt sich direkt aus dem Mollier-h,x-Diagramm für feuchte Luft ablesen?",
                optionen: [
                    "Der Zusammenhang zwischen Temperatur, absolutem Wassergehalt (x), relativer Luftfeuchtigkeit (φ), spezifischer Enthalpie (h) und Taupunkttemperatur",
                    "Der Druckverlust in Kupferrohrleitungen",
                    "Die Heizlast eines Gebäudes nach DIN EN 12831",
                    "Die Schallleistung von Axialventilatoren"
                ],
                richtig: 0,
                erklaerung: "Das Mollier-h,x-Diagramm ist das zentrale Werkzeug der Klimatechnik zur Berechnung von Luftbehandlungsprozessen (Erwärmen, Kühlen, Entfeuchten, Befeuchten, Mischen)."
            },
            {
                id: 67,
                abteilung: "Lüftung & Klima",
                level: "schwer",
                frage: "Was bedeutet der GWP-Wert (Global Warming Potential) bei Kältemitteln in Klimaanlagen und Wärmepumpen?",
                optionen: [
                    "Er gibt an, wie stark 1 kg des Kältemittels im Vergleich zu 1 kg CO2 (GWP = 1) über 100 Jahre zum Treibhauseffekt beiträgt",
                    "Er beschreibt die maximale Kühlleistung in Kilowatt",
                    "Er gibt den Siedepunkt des Kältemittels bei 1 bar an",
                    "Er misst die elektrische Leitfähigkeit des Kompressoröls"
                ],
                richtig: 0,
                erklaerung: "Nach der EU-F-Gase-Verordnung werden Kältemittel mit hohem GWP (z. B. R410A mit GWP 2088) schrittweise durch Kältemittel mit niedrigem GWP (z. B. R32 mit GWP 675 oder R290 mit GWP 3) ersetzt."
            },
            {
                id: 68,
                abteilung: "Lüftung & Klima",
                level: "schwer",
                frage: "Wozu dient ein Sommer-Bypass in einer zentralen Lüftungsanlage mit Wärmerückgewinnung?",
                optionen: [
                    "Er leitet die kühle Nachtluft im Sommer am Wärmetauscher vorbei direkt ins Haus, um die Räume passiv abzukühlen",
                    "Er schaltet die Filter im Sommer ab",
                    "Er verdoppelt die Drehzahl des Abluftventilators",
                    "Er leitet Regenwasser in den Kondensatablauf"
                ],
                richtig: 0,
                erklaerung: "Ist es nachts draußen kühler als im aufgeheizten Haus, würde der Wärmetauscher die kühle Außenluft unerwünscht aufwärmen. Der Bypass umgeht den Wärmetauscher."
            },
            {
                id: 69,
                abteilung: "Lüftung & Klima",
                level: "schwer",
                frage: "Was ist ‚Telefonieschall‘ in einer Lüftungsanlage und wie wird er wirksam verhindert?",
                optionen: [
                    "Die Schallübertragung von einem Raum in den Nachbarraum über gemeinsam genutzte Lüftungsrohre; verhindert wird er durch Telefonieschalldämpfer zwischen den Räumen",
                    "Das Brummen des Netztrafos in der Regelung",
                    "Das Pfeifen der Dunstabzugshaube bei Sturm",
                    "Das Klappern der Rückschlagklappe"
                ],
                richtig: 0,
                erklaerung: "Hängen zwei benachbarte Räume am selben Luftstrang, wirkt das Rohr wie ein Sprachrohr. Spezielle Telefonieschalldämpfer unterbrechen diese Schallbrücke."
            },

            // =========================================================================
            // ABTEILUNG 5: ELEKTRO & REGELUNG (16 Fragen: 5 Leicht, 6 Mittel, 5 Schwer)
            // =========================================================================
            {
                id: 70,
                abteilung: "Elektro & Regelung",
                level: "leicht",
                frage: "Welche Farbe hat die Isolierung des Schutzleiters (PE) in elektrischen Anlagen?",
                optionen: ["Grün-Gelb", "Blau", "Braun", "Schwarz"],
                richtig: 0,
                erklaerung: "Der Schutzleiter (PE) ist international eindeutig durch die Farbkombination Grün-Gelb gekennzeichnet und darf für keinen anderen Zweck verwendet werden."
            },
            {
                id: 71,
                abteilung: "Elektro & Regelung",
                level: "leicht",
                frage: "Warum müssen metallische Heizungs-, Wasser- und Gasrohre an die Haupterdungsschiene (Schutzpotentialausgleich) angeschlossen werden?",
                optionen: [
                    "Um im Fehlerfall gefährliche Berührungsspannungen zwischen verschiedenen leitfähigen Teilen im Gebäude zu verhindern",
                    "Um Kalkablagerungen elektrisch abzubauen",
                    "Damit die Heizungsregelung keine eigene Stromversorgung braucht",
                    "Um den Wasserdruck zu stabilisieren"
                ],
                richtig: 0,
                erklaerung: "Der Schutzpotentialausgleich bringt alle metallischen Rohrleitungen auf dasselbe elektrische Potential wie die Erde."
            },
            {
                id: 72,
                abteilung: "Elektro & Regelung",
                level: "leicht",
                frage: "An welcher Himmelsrichtung eines Gebäudes muss der Außentemperaturfühler einer witterungsgeführten Heizungsregelung montiert werden?",
                optionen: [
                    "Auf der Nord- bzw. Nordostseite (geschützt vor direkter Sonneneinstrahlung und Fremdwärmequellen)",
                    "Auf der Südseite direkt in der Sonne",
                    "Direkt über einem geöffneten Kellerfenster oder Abluftgitter",
                    "Im unbeheizten Dachboden"
                ],
                richtig: 0,
                erklaerung: "Trifft direkte Sonne auf den Fühler, denkt die Regelung, es sei draußen warm, und regelt die Heizung herunter, obwohl die Nordseite des Hauses friert."
            },
            {
                id: 73,
                abteilung: "Elektro & Regelung",
                level: "leicht",
                frage: "Welche Aufgabe hat der Fehlerstrom-Schutzschalter (RCD / FI-Schalter)?",
                optionen: [
                    "Er schaltet den Stromkreis innerhalb von Millisekunden allpolig ab, sobald ein gefährlicher Fehlerstrom (z. B. über einen Menschen oder ein defektes Gehäuse) zur Erde abfließt",
                    "Er schützt Leitungen ausschließlich vor Überlastung durch zu viele Verbraucher",
                    "Er regelt die Drehzahl der Zirkulationspumpe",
                    "Er misst den Stromverbrauch der Wärmepumpe"
                ],
                richtig: 0,
                erklaerung: "Der RCD vergleicht hin- und rückfließenden Strom. Bei einer Differenz (meist ≥ 30 mA im Personenschutz) löst er sofort aus und schützt vor tödlichem Stromschlag."
            },
            {
                id: 74,
                abteilung: "Elektro & Regelung",
                level: "leicht",
                frage: "Welche Funktion hat der Heizungs-Notschalter außerhalb des Heizungsraumes?",
                optionen: [
                    "Er ermöglicht im Gefahrenfall (z. B. Brand oder Ölaustritt) das sichere allpolige Abschalten der Heizungsanlage, ohne den Heizungsraum betreten zu müssen",
                    "Er schaltet im Sommer die Warmwasserbereitung ab",
                    "Er entlüftet den Heizkessel",
                    "Er startet den Schornsteinfeger-Messbetrieb"
                ],
                richtig: 0,
                erklaerung: "Bei Öl- und größeren Gasfeuerstätten ist außerhalb des Aufstellraumes ein leicht zugänglicher, gekennzeichneter Notschalter vorgeschrieben."
            },
            {
                id: 75,
                abteilung: "Elektro & Regelung",
                level: "mittel",
                frage: "Wie lauten die ‚Fünf Sicherheitsregeln‘ der Elektrotechnik in der richtigen Reihenfolge vor Beginn von Arbeiten an elektrischen Anlagen?",
                optionen: [
                    "1. Freischalten, 2. Gegen Wiedereinschalten sichern, 3. Spannungsfreiheit feststellen, 4. Erden und kurzschließen, 5. Benachbarte unter Spannung stehende Teile abdecken oder abschranken",
                    "1. Spannungsfreiheit messen, 2. Sicherung ausschalten, 3. Handschuhe anziehen, 4. Erden, 5. Einschalten",
                    "1. FI-Schalter testen, 2. Werkzeug isolieren, 3. Freischalten, 4. Abdecken, 5. Messen",
                    "1. Erden, 2. Freischalten, 3. Spannungsfreiheit prüfen, 4. Sichern, 5. Abdecken"
                ],
                richtig: 0,
                erklaerung: "Die Fünf Sicherheitsregeln (DIN VDE 0105-100) sind lebensrettend und müssen vor jeder Arbeit an elektrischen Komponenten strikt eingehalten werden."
            },
            {
                id: 76,
                abteilung: "Elektro & Regelung",
                level: "mittel",
                frage: "Was unterscheidet einen Temperaturregler (TR) von einem Sicherheitstemperaturbegrenzer (STB) im Heizkessel?",
                optionen: [
                    "Der TR schaltet im Normalbetrieb selbsttätig ein und aus; der STB schaltet im Störfall verriegelnd ab und darf erst nach Abkühlung manuell entriegelt werden",
                    "Der TR arbeitet mechanisch, der STB immer hydraulisch",
                    "Der TR sitzt im Schornstein, der STB am Heizkörper",
                    "Beide Bauteile haben exakt dieselbe Funktion"
                ],
                richtig: 0,
                erklaerung: "Der STB ist eine reine Sicherheitseinrichtung: Löst er aus (meist bei 100–110 °C), bleibt der Brenner dauerhaft gesperrt, bis ein Fachmann oder Betreiber den Entriegelungsknopf nach Abkühlung drückt."
            },
            {
                id: 77,
                abteilung: "Elektro & Regelung",
                level: "mittel",
                frage: "Wie arbeitet ein typischer PT1000-Temperaturfühler in einer Heizungs- oder Solarregelung?",
                optionen: [
                    "Er verändert seinen elektrischen Widerstand proportional zur Temperatur (bei 0 °C beträgt der Widerstand exakt 1000 Ohm)",
                    "Er erzeugt bei Wärme eine elektrische Spannung von 230 Volt",
                    "Er schaltet bei 1000 °C ab",
                    "Er misst den Wasserdruck in Pascal"
                ],
                richtig: 0,
                erklaerung: "PT1000 steht für Platin-Messwiderstand mit 1000 Ω bei 0 °C. Steigt die Temperatur, steigt auch der elektrische Widerstand definiert an (PTC-Verhalten)."
            },
            {
                id: 78,
                abteilung: "Elektro & Regelung",
                level: "mittel",
                frage: "Wie wird die Drehzahl moderner Hocheffizienz-Umwälzpumpen von einer Heizungsregelung meist stufenlos angesteuert?",
                optionen: [
                    "Über ein PWM-Signal (Pulsweitenmodulation) oder ein analoges 0–10 V Steuersignal",
                    "Durch Verändern der Netzfrequenz von 50 Hz auf 500 Hz",
                    "Über ein mechanisches Gestänge",
                    "Durch Drosseln des Kugelhahns vor der Pumpe"
                ],
                richtig: 0,
                erklaerung: "Über eine separate Steuerleitung (PWM oder 0–10 V) gibt die Regelung der Pumpenelektronik exakt die benötigte Drehzahl vor."
            },
            {
                id: 79,
                abteilung: "Elektro & Regelung",
                level: "mittel",
                frage: "Welche Schutzart (IP-Code) ist für elektrische Betriebsmittel im Bereich 1 unmittelbar über einer Badewanne oder Dusche nach DIN VDE 0100-701 mindestens erforderlich?",
                optionen: ["IPX0 (kein Schutz)", "Mindestens IPX4 (Schutz gegen allseitiges Spritzwasser)", "IP20", "IP11"],
                richtig: 1,
                erklaerung: "In Feuchträumen und Badezimmern (Bereich 1) müssen fest installierte elektrische Betriebsmittel mindestens gegen allseitiges Spritzwasser (IPX4) geschützt sein."
            },
            {
                id: 80,
                abteilung: "Elektro & Regelung",
                level: "mittel",
                frage: "Was ist der grundlegende Unterschied zwischen einer ‚Steuerung‘ und einer ‚Regelung‘ in der Gebäudetechnik?",
                optionen: [
                    "Eine Regelung misst ständig die Ist-Größe (z. B. Raumtemperatur), vergleicht sie mit dem Sollwert und gleicht Störgrößen aus (geschlossener Wirkungskreis); eine Steuerung hat keine Rückkopplung",
                    "Eine Steuerung ist immer digital, eine Regelung immer analog",
                    "Eine Regelung funktioniert nur ohne Strom",
                    "Es gibt keinen Unterschied"
                ],
                richtig: 0,
                erklaerung: "Ein Thermostatventil ist ein Regler (misst Raumtemperatur und drosselt bei Fremdwärme wie Sonneneinstrahlung). Eine reine Außentemperaturführung ohne Raumfühler ist dagegen eine Steuerung."
            },
            {
                id: 81,
                abteilung: "Elektro & Regelung",
                level: "schwer",
                frage: "Wie funktioniert die Flammenüberwachung mittels Ionisationselektrode bei einem modernen Gasbrenner?",
                optionen: [
                    "Die Gasflamme leitet elektrischen Strom und wirkt wie ein Gleichrichter: Aus der angelegten Wechselspannung entsteht ein messbarer Gleichstromanteil (Ionisationsstrom)",
                    "Die Elektrode misst die Helligkeit der Flamme mit einer Fotozelle",
                    "Die Elektrode erhitzt ein Bimetall",
                    "Die Elektrode misst den Gasdruck vor der Düse"
                ],
                richtig: 0,
                erklaerung: "Durch die hohen Temperaturen in der Flamme werden Gasmoleküle ionisiert (elektrisch leitfähig). Aufgrund der unterschiedlichen Elektrodenflächen von Brenner und Fühlerstab entsteht ein Gleichrichtereffekt, den der Feuerungsautomat erkennt."
            },
            {
                id: 82,
                abteilung: "Elektro & Regelung",
                level: "schwer",
                frage: "Wie arbeitet ein Dreiwege-Mischer mit einem 3-Punkt-Stellantrieb in einem Fußbodenheizkreis?",
                optionen: [
                    "Der Stellantrieb erhält über zwei getrennte Steuerleitungen Impulse für ‚Auf‘ (wärmer) oder ‚Zu‘ (kälter) und hält seine Position, wenn kein Signal anliegt",
                    "Er kennt nur die Stellungen 0 % und 100 %",
                    "Er wird über den Wasserdruck verstellt",
                    "Er arbeitet mit drei verschiedenen Netzspannungen (12 V, 24 V, 230 V)"
                ],
                richtig: 0,
                erklaerung: "Bei der 3-Punkt-Regelung hat der Motor drei Anschlüsse: Neutralleiter (N), Phase für ‚Mischer auf‘ und Phase für ‚Mischer zu‘. So wird die gewünschte Vorlauftemperatur exakt eingemischt."
            },
            {
                id: 83,
                abteilung: "Elektro & Regelung",
                level: "schwer",
                frage: "Warum müssen in vielen Installationsbereichen der Haus- und Wärmepumpentechnik allstromsensitive Fehlerstrom-Schutzschalter (RCD Typ B) statt einfacher Typ-A-Schalter eingesetzt werden?",
                optionen: [
                    "Weil Inverter-Verdichter und Frequenzumrichter glatte Gleichfehlerströme erzeugen können, die einen herkömmlichen RCD Typ A ‚erblinden‘ lassen (Sättigung des Summenstromwandlers)",
                    "Weil Typ A nur für 12-Volt-Anlagen zugelassen ist",
                    "Weil Typ B gleichzeitig als Wasserzähler dient",
                    "Weil Typ B keinen Neutralleiter benötigt"
                ],
                richtig: 0,
                erklaerung: "Drehzahlgeregelte Wärmepumpen und Pumpen arbeiten mit Frequenzumrichtern. Im Fehlerfall können glatte Gleichfehlerströme auftreten, die nur ein RCD Typ B (oder Typ F bei einphasigen Umrichtern) sicher erkennt."
            },
            {
                id: 84,
                abteilung: "Elektro & Regelung",
                level: "schwer",
                frage: "Welcher Fehler liegt wahrscheinlich vor, wenn ein PT1000-Fühler im Regler-Display einen Wert von ‚-50 °C‘ oder ‚999 °C‘ (Kurzschluss/Unterbrechung) anzeigt?",
                optionen: [
                    "Kabelbruch (unendlich hoher Widerstand) oder Kurzschluss in der Fühlerleitung bzw. ein defektes Fühlerelement",
                    "Die Heizungspumpe läuft rückwärts",
                    "Der Gasdruck ist zu hoch",
                    "Das Membran-Ausdehnungsgefäß ist voll Wasser"
                ],
                richtig: 0,
                erklaerung: "Ein extrem niedriger Widerstand (0 Ω = Kurzschluss) wird vom Regler als unrealistisch tiefe Temperatur interpretiert; ein unendlich hoher Widerstand (Kabelbruch) als extrem hohe Temperatur."
            },
            {
                id: 85,
                abteilung: "Elektro & Regelung",
                level: "schwer",
                frage: "Was bewirkt ein ‚hydraulischer Kurzschluss‘ über einen falsch angeschlossenen Dreiwege-Mischer?",
                optionen: [
                    "Das heiße Vorlaufwasser strömt ungenutzt direkt in den Kesselrücklauf, während der Heizkreis kalt bleibt",
                    "Der FI-Schalter löst sofort aus",
                    "Das Sicherheitsventil öffnet bei 1 bar",
                    "Der Gaszähler läuft doppelt so schnell"
                ],
                richtig: 0,
                erklaerung: "Werden Vorlauf-, Rücklauf- und Mischanschluss (A, B, AB) am Mischer vertauscht, pumpt die Heizkreispumpe im Kreis durch den Bypass statt durch die Heizflächen."
            },

            // =========================================================================
            // ABTEILUNG 6: WERKSTOFFE & NORMEN (15 Fragen: 5 Leicht, 5 Mittel, 5 Schwer)
            // =========================================================================
            {
                id: 86,
                abteilung: "Werkstoffe & Normen",
                level: "leicht",
                frage: "Was besagt die ‚Fließregel‘ bei der Kombination von Kupfer- und verzinkten Stahlrohren in Trinkwasseranlagen?",
                optionen: [
                    "In Fließrichtung darf Kupfer nicht vor verzinktem Stahl eingebaut werden, da sonst Kontaktkorrosion (Lochfraß) am Stahlrohr entsteht",
                    "Kupferrohre dürfen immer nur unterhalb von Stahlrohren verlegt werden",
                    "Verzinkter Stahl darf nur für Gasleitungen verwendet werden",
                    "Beide Werkstoffe dürfen niemals im selben Gebäude vorkommen"
                ],
                richtig: 0,
                erklaerung: "Kupfer-Ionen werden vom Wasser mitgerissen und schlagen sich auf dem unedleren Zink nieder. Es bilden sich Lokalelemente, die das verzinkte Stahlrohr durchfressen."
            },
            {
                id: 87,
                abteilung: "Werkstoffe & Normen",
                level: "leicht",
                frage: "Welche Dichtmittel sind für metallene Gewindeverbindungen in der Gas- und Trinkwasserinstallation nach DIN EN 751 zugelassen?",
                optionen: [
                    "Hanf in Verbindung mit zugelassener Gewindedichtpaste oder PTFE-Dichtband bzw. -Dichtfaden",
                    "Sanitärsilikon und Isolierband",
                    "Leinölfirnis und Zeitungspapier",
                    "Schraubensicherungslack aus dem Fahrzeugbau"
                ],
                richtig: 0,
                erklaerung: "Nach DIN EN 751-1/-2/-3 sind nichtaushärtende Dichtmittel (Hanf + Paste nach EN 751-2) sowie PTFE-Bänder/-Fäden (EN 751-3) zugelassen. Bei Gas ist Hanf in vielen Netzgebieten bzw. bei Flüssiggas jedoch eingeschränkt (dort PTFE oder anaerobe Dichtmittel)."
            },
            {
                id: 88,
                abteilung: "Werkstoffe & Normen",
                level: "leicht",
                frage: "Welche Aufgabe hat die rote/grüne/gelbe Folien-Kennzeichnung (z. B. ‚unverpresst undicht‘) auf modernen Pressfittings?",
                optionen: [
                    "Sie zeigt bei der Druckprobe durch gezielte Undichtigkeit sofort an, wenn ein Fitting versehentlich nicht verpresst wurde, und fällt nach dem Verpressen ab",
                    "Sie schützt das Rohr vor UV-Strahlung",
                    "Sie ersetzt die Rohrdämmung",
                    "Sie verhindert Kalkablagerungen im Fitting"
                ],
                richtig: 0,
                erklaerung: "Vergessene Pressverbindungen würden bei der Druckprobe oft zunächst dicht halten und erst später im Betrieb abrutschen. Durch Zwangsundichtigkeit (spezieller Dichtring + Kontrollfolie) fällt dies sofort auf."
            },
            {
                id: 89,
                abteilung: "Werkstoffe & Normen",
                level: "leicht",
                frage: "Warum besitzen Mehrschichtverbundrohre (z. B. PE-Xb / Al / PE-Xb) eine dünne Aluminiumschicht in der Rohrwand?",
                optionen: [
                    "Sie sorgt für 100 % Sauerstoffdichtheit, Formstabilität (Biegefestigkeit) und reduziert die Wärmeausdehnung erheblich",
                    "Sie leitet elektrischen Strom für die Heizungsregelung",
                    "Sie ersetzt den Potentialausgleich",
                    "Sie macht das Rohr durchsichtig"
                ],
                richtig: 0,
                erklaerung: "Reine Kunststoffrohre dehnen sich bei Wärme stark aus und lassen ohne Sperrschicht Sauerstoff diffundieren. Der Aluminiumkern macht das Rohr formstabil und sauerstoffdicht."
            },
            {
                id: 90,
                abteilung: "Werkstoffe & Normen",
                level: "leicht",
                frage: "Warum müssen Rohrschellen in Wohngebäuden mit einer Gummieinlage (Schallschutzeinlage) ausgestattet sein?",
                optionen: [
                    "Zur Körperschallentkopplung, damit Fließ- und Pumpen-Geräusche nicht auf Wände und Decken übertragen werden (DIN 4109)",
                    "Damit das Rohr nicht durchrostet",
                    "Um die Wärmeausdehnung komplett zu blockieren",
                    "Damit die Schelle nicht abrutscht"
                ],
                richtig: 0,
                erklaerung: "Nach DIN 4109 (Schallschutz im Hochbau) verhindern elastische Einlagen in Rohrschellen die Übertragung von Körperschall in das Mauerwerk."
            },
            {
                id: 91,
                abteilung: "Werkstoffe & Normen",
                level: "mittel",
                frage: "Warum ist das Weichlöten von Kupferrohren bei Gasleitungen nach DVGW-TRGI verboten?",
                optionen: [
                    "Weil Weichlot (Schmelztemperatur < 450 °C) im Brandfall schnell schmilzt, die Verbindung sich löst und Gas unkontrolliert ins Feuer strömt",
                    "Weil Weichlot von Erdgas chemisch aufgelöst wird",
                    "Weil Weichlote zu teuer sind",
                    "Weil Kupferrohre nur geschweißt werden dürfen"
                ],
                richtig: 0,
                erklaerung: "In der Gasinstallation sind für Kupferrohre nur mechanisch und thermisch hochbelastbare Verbindungen zulässig: Pressverbindungen (mit gelber Gas-Kennzeichnung / HNBR-Dichtring) oder Hartlöten (ab 450 °C)."
            },
            {
                id: 92,
                abteilung: "Werkstoffe & Normen",
                level: "mittel",
                frage: "Warum darf ein Pressfitting (z. B. M-Kontur oder V-Kontur) niemals mit einer unpassenden Pressbacke (z. B. TH-Kontur) verpresst werden?",
                optionen: [
                    "Weil der Dichtring nicht korrekt verformt wird und die mechanische Haltekraft nicht erreicht wird – es besteht akute Gefahr des Abrutschens unter Druck",
                    "Weil sonst die Pressmaschine überhitzt",
                    "Weil sich die Farbe des Fittings ändert",
                    "Es gibt keinen Unterschied zwischen den Konturen"
                ],
                richtig: 0,
                erklaerung: "Jedes Presssystem ist exakt auf seine Kontur (M, V, TH, U usw.) abgestimmt. Falsche Pressbacken führen zu Undichtigkeiten oder zum plötzlichen Lösen der Verbindung."
            },
            {
                id: 93,
                abteilung: "Werkstoffe & Normen",
                level: "mittel",
                frage: "Was versteht man unter ‚Sauerstoffdiffusion‘ bei älteren Kunststoffrohren (ohne EVOH-Sperrschicht) in Fußbodenheizungen?",
                optionen: [
                    "Durch die Rohrwand dringt Luftsauerstoff in das Heizungswasser ein, was zu starker Korrosion an Stahlbauteilen (Kessel, Pumpen) und Verschlammung führt",
                    "Das Heizungswasser verdunstet durch das Rohr",
                    "Die Raumluft wird mit Sauerstoff angereichert",
                    "Das Rohr wird durch den Sauerstoff weich"
                ],
                richtig: 0,
                erklaerung: "Nicht sauerstoffdichte Kunststoffrohre nach DIN 4726 lassen kontinuierlich Sauerstoff ins Heizwasser. Abhilfe schafft eine Systemtrennung über einen Plattenwärmetauscher."
            },
            {
                id: 94,
                abteilung: "Werkstoffe & Normen",
                level: "mittel",
                frage: "Warum muss bei der Verlegung langer gerader Rohrleitungen (z. B. Warmwasser- oder Heizungssteigleitungen) ein Dehnungsausgleicher (U-Bogen, L-Schenkel oder Kompensator) eingeplant werden?",
                optionen: [
                    "Um die thermische Längenausdehnung bei Erwärmung spannungsfrei aufzunehmen, damit Rohre und Fittings nicht abreißen oder ausknicken",
                    "Um die Fließgeschwindigkeit zu bremsen",
                    "Damit das Wasser länger warm bleibt",
                    "Um Luftblasen zu sammeln"
                ],
                richtig: 0,
                erklaerung: "Ein 10 m langes Kunststoff- oder Kupferrohr dehnt sich bei 50 K Temperaturerhöhung um mehrere Millimeter bis Zentimeter aus. Festpunkte und Gleitschellen lenken diese Dehnung gezielt in den Biegeschenkel."
            },
            {
                id: 95,
                abteilung: "Werkstoffe & Normen",
                level: "mittel",
                frage: "Welche Bedeutung hat die Farbkennzeichnung der Dichtringe in Pressfittings (z. B. Schwarz = EPDM, Gelb = HNBR, Grün = FKM)?",
                optionen: [
                    "Sie gibt den zulässigen Einsatzbereich an: EPDM für Trinkwasser/Heizung, HNBR für Gas, FKM (Viton) für hohe Temperaturen (Solar) und Öle",
                    "Sie dient nur der optischen Verschönerung",
                    "Sie gibt den Rohrdurchmesser in Millimetern an",
                    "Alle Dichtringe bestehen aus demselben Material"
                ],
                richtig: 0,
                erklaerung: "EPDM ist für Trinkwasser und Heizung ideal, wird aber durch Gas oder Öl zerstört. Deshalb sind für Gas spezielle HNBR-Dichtringe (gelbe Markierung) vorgeschrieben."
            },
            {
                id: 96,
                abteilung: "Werkstoffe & Normen",
                level: "schwer",
                frage: "Welche Art der Korrosion tritt bei Kupferrohren häufig in den ersten Betriebsmonaten auf, wenn bei der Montage Flussmittelreste im Rohr verblieben sind oder kaltes Wasser lange stagniert?",
                optionen: [
                    "Lochfraßkorrosion Typ II (Kaltwasser-Lochkorrosion)",
                    "Spannungsrisskorrosion durch Frost",
                    "Kavitationskorrosion",
                    "Elektrolytische Außenkorrosion durch Sonnenlicht"
                ],
                richtig: 0,
                erklaerung: "Aggressives Flussmittel, Schmutzpartikel oder Stagnation in neuen Kupferrohren verhindern die Ausbildung einer gleichmäßigen schützenden Kupferoxidschicht und führen zu punktuellem Lochfraß."
            },
            {
                id: 97,
                abteilung: "Werkstoffe & Normen",
                level: "schwer",
                frage: "Warum ist das Hartlöten von Kupferrohren in der Trinkwasserinstallation für Abmessungen bis einschließlich DN 25 (28 × 1,5 mm) nach DVGW-Arbeitsblatt GW 2 nicht mehr zulässig?",
                optionen: [
                    "Durch die hohen Löttemperaturen (über 450 °C) glüht das Kupferrohr weich (Verlust der Festigkeit) und es entstehen schädliche Verzunderungen im Rohrinneren (Lochfraßgefahr)",
                    "Weil Hartlot Blei enthält",
                    "Weil Kupferrohre unter DN 25 schmelzen",
                    "Weil es keine Hartlot-Fittings in diesen Größen gibt"
                ],
                richtig: 0,
                erklaerung: "Bis 28 × 1,5 mm sind in Trinkwasseranlagen nur Pressen, Weichlöten (bis 28 mm) oder Klemm-/Steckverbindungen erlaubt, um Festigkeitsverlust und Zunderbildung durch Hartlöten zu vermeiden."
            },
            {
                id: 98,
                abteilung: "Werkstoffe & Normen",
                level: "schwer",
                frage: "Wie berechnet sich die thermische Längenausdehnung (ΔL) einer Rohrleitung?",
                optionen: [
                    "ΔL = L0 × α × ΔT (Ursprungslänge × Längenausdehnungskoeffizient × Temperaturdifferenz)",
                    "ΔL = L0 / (α × ΔT)",
                    "ΔL = ΔT × L0²",
                    "ΔL = α + ΔT"
                ],
                richtig: 0,
                erklaerung: "Beispiel Kupfer (α = 0,0165 mm/(m·K)): Bei 10 m Länge und 50 K Erwärmung dehnt sich das Rohr um 10 × 0,0165 × 50 = 8,25 mm aus."
            },
            {
                id: 99,
                abteilung: "Werkstoffe & Normen",
                level: "schwer",
                frage: "Was versteht man in der DIN 4109 (Schallschutz im Hochbau) unter ‚schutzwürdigen Räumen‘?",
                optionen: [
                    "Wohn-, Schlaf-, Kinder- und Arbeitszimmer sowie Unterrichts- und Krankenräume (im Gegensatz zu Bädern, Fluren oder Technikräumen)",
                    "Ausschließlich Heizungskeller und Hausanschlussräume",
                    "Nur Balkone und Terrassen",
                    "Alle Räume mit einem Bodenablauf"
                ],
                richtig: 0,
                erklaerung: "Gegenüber schutzwürdigen Räumen (wie Schlafräumen fremder Wohnungen) gelten strenge maximale Schalldruckpegel für Wasser- und Abwasserinstallationen (z. B. max. 30 dB(A) bzw. 25 dB(A) bei erhöhtem Schallschutz)."
            },
            {
                id: 100,
                abteilung: "Werkstoffe & Normen",
                level: "schwer",
                frage: "Welche Anforderung stellt die Muster-Leitungsanlagen-Richtlinie (MLAR) an brennbare Rohrleitungen (z. B. Kunststoff-Abwasserrohre > DN 32), die durch feuerwiderstandsfähige Decken oder Brandwände geführt werden?",
                optionen: [
                    "Sie müssen mit zugelassenen Brandschutzmanschetten oder geprüften Abschottungssystemen gesichert werden, die im Brandfall aufschäumen und die Öffnung feuerdicht verschließen",
                    "Sie dürfen einfach mit Bauschaum eingeklebt werden",
                    "Es sind keine besonderen Maßnahmen erforderlich",
                    "Sie müssen mit Aluminiumfolie umwickelt werden"
                ],
                richtig: 0,
                erklaerung: "Schmilzt ein Kunststoffrohr im Brandfall weg, entsteht ein Loch in der Brandwand/Decke. Intumeszierende Brandschutzmanschetten blähen sich bei Hitze stark auf und quetschen bzw. verschließen die Durchdringung zuverlässig."
            }
        ];

        let aktuelleAbteilung = 'alle';
        let aktuellesLevel = 'alle';
        let gefilterteFragen = [...fragenKatalog];
        let aktuelleFrageIndex = 0;
        let richtigeAntwortenAnzahl = 0;
        let beantworteteFragenAnzahl = 0;
        let frageBeantwortet = false;
        let deutscheStimmen = [];

        // Schlüsselwörter zur Erkennung männlicher und weiblicher deutscher Stimmen
        const maennlicheKeywords = ['markus', 'martin', 'yannick', 'stefan', 'daniel', 'hans', 'male', 'männlich'];
        const weiblicheKeywords = ['anna', 'helena', 'petra', 'marie', 'marlene', 'vicki', 'female', 'weiblich'];

        /**
         * Lädt alle deutschen Systemstimmen und entfernt doppelte iOS-Einträge.
         */
        function stimmenLaden() {
            try {
                if (!('speechSynthesis' in window)) return;
                const alleStimmen = window.speechSynthesis.getVoices();
                const gefiltert = alleStimmen.filter(v => v.lang && v.lang.toLowerCase().includes('de'));

                const stimmenMap = new Map();
                gefiltert.forEach(stimme => {
                    const basisName = stimme.name
                        .replace(/\(.*?\)/g, '')
                        .replace(/Microsoft|Apple|Google|Deutsch|German/gi, '')
                        .trim()
                        .toLowerCase();

                    const istErweitert = stimme.name.toLowerCase().includes('erweitert') ||
                                         stimme.name.toLowerCase().includes('enhanced') ||
                                         stimme.name.toLowerCase().includes('premium');

                    if (!stimmenMap.has(basisName) || istErweitert) {
                        stimmenMap.set(basisName, stimme);
                    }
                });

                deutscheStimmen = Array.from(stimmenMap.values());
            } catch (e) {
                console.warn("Fehler beim Laden der Stimmen:", e);
            }
        }

        /**
         * Sucht die beste verfügbare Systemstimme für 'male' oder 'female'.
         */
        function findeStimmeFuerProfil(profil) {
            if (deutscheStimmen.length === 0) {
                stimmenLaden();
            }
            if (deutscheStimmen.length === 0) return null;

            const keywords = profil === 'male' ? maennlicheKeywords : weiblicheKeywords;
            for (const kw of keywords) {
                const treffer = deutscheStimmen.find(v => v.name.toLowerCase().includes(kw));
                if (treffer) return treffer;
            }
            return deutscheStimmen[0];
        }

        if ('speechSynthesis' in window) {
            window.speechSynthesis.onvoiceschanged = stimmenLaden;
        }

        /**
         * Wechselt zwischen den Tabs 'Quiz-Trainer' und 'Notizen & Editor'.
         */
        function switchTab(tab) {
            const quizSec = document.getElementById('section-quiz');
            const editorSec = document.getElementById('section-editor');
            const btnQuiz = document.getElementById('btn-quiz');
            const btnEditor = document.getElementById('btn-editor');

            if (tab === 'quiz') {
                quizSec.classList.remove('hidden');
                editorSec.classList.add('hidden');
                btnQuiz.className = "flex-1 py-3 px-4 rounded-2xl text-sm font-bold transition-all bg-blue-600 text-white shadow-sm active:scale-[0.98]";
                btnEditor.className = "flex-1 py-3 px-4 rounded-2xl text-sm font-bold transition-all text-slate-600 hover:bg-slate-200/70 active:scale-[0.98]";
            } else {
                quizSec.classList.add('hidden');
                editorSec.classList.remove('hidden');
                btnEditor.className = "flex-1 py-3 px-4 rounded-2xl text-sm font-bold transition-all bg-blue-600 text-white shadow-sm active:scale-[0.98]";
                btnQuiz.className = "flex-1 py-3 px-4 rounded-2xl text-sm font-bold transition-all text-slate-600 hover:bg-slate-200/70 active:scale-[0.98]";
                ladeNotizen();
            }
        }

        /**
         * Wendet sowohl den Abteilungs- als auch den Schwierigkeitsfilter kombiniert an.
         */
        function applyFilters() {
            if ('speechSynthesis' in window) {
                window.speechSynthesis.cancel();
            }

            gefilterteFragen = fragenKatalog.filter(f => {
                const matchDept = aktuelleAbteilung === 'alle' || f.abteilung === aktuelleAbteilung;
                const matchLevel = aktuellesLevel === 'alle' || f.level === aktuellesLevel;
                return matchDept && matchLevel;
            });

            aktuelleFrageIndex = 0;
            richtigeAntwortenAnzahl = 0;
            beantworteteFragenAnzahl = 0;
            ladeFrage();
        }

        /**
         * Setzt die gewählte Fachabteilung und aktualisiert die Filter-Buttons.
         */
        function setDepartment(dept) {
            aktuelleAbteilung = dept;
            const abteilungen = [
                'alle',
                'Heizung & Wärmepumpen',
                'Sanitär & Trinkwasser',
                'Gas & Abgas',
                'Lüftung & Klima',
                'Elektro & Regelung',
                'Werkstoffe & Normen'
            ];

            abteilungen.forEach(abt => {
                const btn = document.getElementById(`dept-${abt}`);
                if (!btn) return;
                if (abt === dept) {
                    btn.className = "shrink-0 py-2 px-3.5 rounded-xl text-xs font-bold border-2 border-blue-600 bg-blue-50 text-blue-800 transition-all active:scale-95";
                } else {
                    btn.className = "shrink-0 py-2 px-3.5 rounded-xl text-xs font-bold border border-slate-200 bg-white text-slate-700 hover:bg-slate-50 transition-all active:scale-95";
                }
            });

            applyFilters();
        }

        /**
         * Filtert die Fragen nach dem gewählten Schwierigkeitslevel ('alle', 'leicht', 'mittel', 'schwer').
         */
        function setDifficulty(level) {
            aktuellesLevel = level;
            const levels = ['alle', 'leicht', 'mittel', 'schwer'];
            levels.forEach(lvl => {
                const btn = document.getElementById(`diff-${lvl}`);
                if (!btn) return;
                if (lvl === level) {
                    btn.className = "py-2 px-2 rounded-xl text-xs font-bold border-2 border-blue-600 bg-blue-50 text-blue-800 transition-all active:scale-95 text-center";
                } else {
                    btn.className = "py-2 px-2 rounded-xl text-xs font-bold border border-slate-200 bg-white text-slate-700 hover:bg-slate-50 transition-all active:scale-95 text-center";
                }
            });

            applyFilters();
        }

        /**
         * Mischt die aktuell gefilterten Fragen zufällig durch (Fisher-Yates Shuffle).
         */
        function shuffleQuestions() {
            if ('speechSynthesis' in window) {
                window.speechSynthesis.cancel();
            }
            for (let i = gefilterteFragen.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [gefilterteFragen[i], gefilterteFragen[j]] = [gefilterteFragen[j], gefilterteFragen[i]];
            }
            aktuelleFrageIndex = 0;
            richtigeAntwortenAnzahl = 0;
            beantworteteFragenAnzahl = 0;
            ladeFrage();
        }

        /**
         * Lädt die aktuelle Frage sofort in die Benutzeroberfläche.
         */
        function ladeFrage() {
            const questionBox = document.getElementById('question-box');
            const optionsContainer = document.getElementById('options-container');
            const counterEl = document.getElementById('question-counter');
            const scoreEl = document.getElementById('score-display');
            const levelBadge = document.getElementById('level-badge');
            const topicTag = document.getElementById('topic-tag');
            const nextBtn = document.getElementById('next-btn');
            const feedbackEl = document.getElementById('quiz-feedback');

            if (!questionBox || !optionsContainer || gefilterteFragen.length === 0) return;

            frageBeantwortet = false;
            const q = gefilterteFragen[aktuelleFrageIndex];

            counterEl.innerText = `Frage ${aktuelleFrageIndex + 1} von ${gefilterteFragen.length}`;
            scoreEl.innerText = `Richtig: ${richtigeAntwortenAnzahl}`;
            topicTag.innerText = `${q.abteilung} • #${q.id}`;
            questionBox.innerText = q.frage;

            // Level-Badge färben
            if (q.level === 'leicht') {
                levelBadge.className = "px-2.5 py-1 rounded-full text-[11px] font-bold bg-emerald-100 text-emerald-800";
                levelBadge.innerText = "🟢 Leicht";
            } else if (q.level === 'mittel') {
                levelBadge.className = "px-2.5 py-1 rounded-full text-[11px] font-bold bg-amber-100 text-amber-800";
                levelBadge.innerText = "🟡 Mittel";
            } else {
                levelBadge.className = "px-2.5 py-1 rounded-full text-[11px] font-bold bg-rose-100 text-rose-800";
                levelBadge.innerText = "🔴 Schwer";
            }

            optionsContainer.innerHTML = '';
            q.optionen.forEach((option, index) => {
                const btn = document.createElement('button');
                btn.type = 'button';
                btn.className = "w-full text-left p-4 rounded-2xl border border-slate-200 bg-white hover:border-blue-500 hover:bg-blue-50/40 text-sm font-medium transition-all text-slate-800 active:scale-[0.99] shadow-2xs";
                btn.innerText = option;
                btn.onclick = () => antworte(index, btn);
                optionsContainer.appendChild(btn);
            });

            nextBtn.style.display = 'none';
            feedbackEl.classList.add('hidden');
            feedbackEl.innerHTML = '';
        }

        /**
         * Wertet die gewählte Antwort aus und blendet die fachliche Erklärung inklusive Vorlese-Button ein.
         */
        function antworte(auswahlIndex, buttonElement) {
            if (frageBeantwortet) return;
            frageBeantwortet = true;
            beantworteteFragenAnzahl++;

            const q = gefilterteFragen[aktuelleFrageIndex];
            const alleButtons = document.querySelectorAll('#options-container button');
            alleButtons.forEach(b => b.disabled = true);

            const feedbackEl = document.getElementById('quiz-feedback');
            feedbackEl.classList.remove('hidden');

            const vorlesenErklaerungBtn = `
                <button type="button" onclick="textVorlesen('erklaerung')" class="mt-2.5 inline-flex items-center gap-1.5 px-3 py-1.5 rounded-lg bg-white/80 hover:bg-white text-slate-800 font-bold text-[11px] border border-slate-300/70 shadow-2xs transition-all active:scale-95">
                    <span>🔊</span> Erklärung vorlesen
                </button>
            `;

            if (auswahlIndex === q.richtig) {
                buttonElement.className = "w-full text-left p-4 rounded-2xl border-2 border-emerald-500 bg-emerald-50 text-emerald-950 text-sm font-bold shadow-sm";
                feedbackEl.className = "p-4 rounded-2xl bg-emerald-50/90 border border-emerald-200 text-emerald-950 text-xs leading-relaxed mb-4";
                feedbackEl.innerHTML = `
                    <span class="text-emerald-700 font-extrabold text-sm block mb-1">✅ Richtig!</span>
                    <p id="explanation-text">${q.erklaerung}</p>
                    ${vorlesenErklaerungBtn}
                `;
                richtigeAntwortenAnzahl++;
            } else {
                buttonElement.className = "w-full text-left p-4 rounded-2xl border-2 border-rose-500 bg-rose-50 text-rose-950 text-sm font-bold shadow-sm";
                alleButtons[q.richtig].className = "w-full text-left p-4 rounded-2xl border-2 border-emerald-500 bg-emerald-50 text-emerald-950 text-sm font-bold shadow-sm";
                feedbackEl.className = "p-4 rounded-2xl bg-rose-50/90 border border-rose-200 text-rose-950 text-xs leading-relaxed mb-4";
                feedbackEl.innerHTML = `
                    <span class="text-rose-700 font-extrabold text-sm block mb-1">❌ Leider falsch.</span>
                    <p id="explanation-text">${q.erklaerung}</p>
                    ${vorlesenErklaerungBtn}
                `;
            }

            document.getElementById('score-display').innerText = `Richtig: ${richtigeAntwortenAnzahl}`;
            document.getElementById('next-btn').style.display = 'block';
        }

        /**
         * Wechselt zur nächsten Frage im aktuellen Filter.
         */
        function naechsteFrage() {
            if ('speechSynthesis' in window) {
                window.speechSynthesis.cancel();
            }
            aktuelleFrageIndex = (aktuelleFrageIndex + 1) % gefilterteFragen.length;
            ladeFrage();
        }

        /**
         * Liest wahlweise die aktuelle Frage ('frage') oder die Erklärung ('erklaerung') vor.
         */
        function textVorlesen(quelle) {
            let text = "";
            if (quelle === 'erklaerung') {
                const expEl = document.getElementById('explanation-text');
                if (expEl) text = expEl.innerText;
            } else {
                const qEl = document.getElementById('question-box');
                if (qEl) text = qEl.innerText;
            }

            if (!text) return;

            if (!('speechSynthesis' in window)) {
                const feedbackEl = document.getElementById('quiz-feedback');
                feedbackEl.classList.remove('hidden');
                feedbackEl.className = "p-3 rounded-xl bg-rose-50 text-rose-700 text-xs font-semibold mb-4 text-center";
                feedbackEl.innerText = "Dein Browser unterstützt leider keine Sprachausgabe.";
                return;
            }

            try {
                window.speechSynthesis.cancel();

                const profil = document.getElementById('voice-profile').value;
                const speech = new SpeechSynthesisUtterance(text);
                speech.lang = 'de-DE';

                const stimme = findeStimmeFuerProfil(profil);
                if (stimme) {
                    speech.voice = stimme;
                }

                if (profil === 'male') {
                    speech.pitch = 0.78;
                    speech.rate = 0.95;
                } else {
                    speech.pitch = 1.00;
                    speech.rate = 0.98;
                }

                window.speechSynthesis.speak(speech);
            } catch (err) {
                console.error("Sprachausgabe-Fehler:", err);
            }
        }

        /**
         * Speichert persönliche Notizen lokal im Browser (localStorage).
         */
        function notizSpeichern() {
            try {
                const content = document.getElementById('user-notes').value;
                localStorage.setItem('omar_meister_notiz', content);
                
                const statusEl = document.getElementById('save-status');
                statusEl.style.opacity = '1';
                setTimeout(() => {
                    statusEl.style.opacity = '0';
                }, 2000);
            } catch (e) {
                console.warn("Speichern fehlgeschlagen:", e);
            }
        }

        /**
         * Lädt gespeicherte Notizen aus dem localStorage.
         */
        function ladeNotizen() {
            try {
                const savedNotes = localStorage.getItem('omar_meister_notiz');
                if (savedNotes !== null) {
                    document.getElementById('user-notes').value = savedNotes;
                }
            } catch (e) {
                console.warn("Laden der Notizen fehlgeschlagen:", e);
            }
        }

        /**
         * Initialisiert die App sofort ohne Verzögerung.
         */
        function initApp() {
            ladeFrage();
            stimmenLaden();
            ladeNotizen();
        }

        // Direkte Ausführung am Ende des Body + Fallback
        initApp();
        if (document.readyState === 'loading') {
            document.addEventListener('DOMContentLoaded', initApp);
        }
    </script>
</body>
</html>
