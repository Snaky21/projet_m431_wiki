# 📅 Mon Emploi du Temps

<div style="
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); 
    color: white; 
    padding: 25px; 
    border-radius: 12px; 
    margin-bottom: 30px; 
    text-align: center;
    box-shadow: 0 4px 15px rgba(0,0,0,0.2);
    font-family: sans-serif;
">
    <div style="font-size: 0.9em; text-transform: uppercase; letter-spacing: 2px; opacity: 0.8; margin-bottom: 10px;">
        En Direct
    </div>
    <div id="main-status" style="font-size: 2.5em; font-weight: bold; margin-bottom: 5px;">
        Chargement...
    </div>
    <div id="sub-status" style="font-size: 1.1em; opacity: 0.9; margin-bottom: 20px;">
        --
    </div>
    <div style="background: rgba(255,255,255,0.2); height: 6px; border-radius: 10px; overflow: hidden; max-width: 400px; margin: 0 auto;">
        <div id="progress-bar" style="width: 0%; height: 100%; background: #4fd1c5; transition: width 1s linear;"></div>
    </div>
</div>

<script>
    const scheduleData = [
        { name: "H1",       start: [7, 15],  end: [8, 0] },
        { name: "H2",       start: [8, 5],   end: [8, 50] },
        { name: "H3",       start: [8, 55],  end: [9, 40] },
        { name: "☕ Grande Pause", start: [9, 40], end: [10, 5] },
        { name: "H4",       start: [10, 5],  end: [10, 50] },
        { name: "H5",       start: [10, 55], end: [11, 40] },
        { name: "H6",       start: [11, 45], end: [12, 30] },
        { name: "🥪 Pause Midi",   start: [12, 30], end: [12, 40] },
        { name: "H7",       start: [12, 40], end: [13, 25] },
        { name: "H8",       start: [13, 30], end: [14, 15] },
        { name: "☕ Pause",  start: [14, 15], end: [14, 35] },
        { name: "H9",       start: [14, 35], end: [15, 20] },
        { name: "H10",      start: [15, 25], end: [16, 10] },
        { name: "H11",      start: [16, 15], end: [17, 0] },
        { name: "H12",      start: [17, 5],  end: [17, 50] }
    ];

    function updateTimer() {
        const now = new Date();
        const currentTotalMin = now.getHours() * 60 + now.getMinutes();
        const currentSeconds = now.getSeconds();
        const absoluteNow = currentTotalMin * 60 + currentSeconds;

        let activePeriod = null;
        let nextPeriod = null;
        
        for (let i = 0; i < scheduleData.length; i++) {
            const p = scheduleData[i];
            const pStart = p.start[0] * 60 + p.start[1];
            const pEnd = p.end[0] * 60 + p.end[1];

            if (currentTotalMin >= (pStart) && currentTotalMin < pEnd) {
                activePeriod = p;
                if (i + 1 < scheduleData.length) nextPeriod = scheduleData[i+1];
                break;
            }
            if (currentTotalMin < pStart) {
                nextPeriod = p;
                break;
            }
        }

        const mainStatus = document.getElementById('main-status');
        const subStatus = document.getElementById('sub-status');
        const progressBar = document.getElementById('progress-bar');

        if (activePeriod) {
            const pEndSeconds = (activePeriod.end[0] * 60 + activePeriod.end[1]) * 60;
            const remainingSeconds = pEndSeconds - absoluteNow;
            const m = Math.floor(remainingSeconds / 60);
            const s = remainingSeconds % 60;
            mainStatus.innerHTML = `${activePeriod.name} en cours`;
            subStatus.innerHTML = `Fin dans <strong>${m} min ${s} s</strong>`;
            
            const pStartSeconds = (activePeriod.start[0] * 60 + activePeriod.start[1]) * 60;
            const totalDuration = pEndSeconds - pStartSeconds;
            const pct = ((absoluteNow - pStartSeconds) / totalDuration) * 100;
            progressBar.style.width = pct + "%";
            progressBar.style.backgroundColor = "#4fd1c5";

        } else if (nextPeriod) {
            const pStartSeconds = (nextPeriod.start[0] * 60 + nextPeriod.start[1]) * 60;
            const remainingSeconds = pStartSeconds - absoluteNow;
            const m = Math.floor(remainingSeconds / 60);
            const s = remainingSeconds % 60;
            mainStatus.innerHTML = `⏳ Pause / Transition`;
            subStatus.innerHTML = `Le cours <strong>${nextPeriod.name}</strong> commence dans <strong>${m} min ${s} s</strong>`;
            progressBar.style.width = "100%";
            progressBar.style.backgroundColor = "#fbbf24";
        } else {
            mainStatus.innerHTML = "🎉 Journée Terminée";
            subStatus.innerHTML = "À demain !";
            progressBar.style.width = "0%";
        }
    }
    setInterval(updateTimer, 1000);
    updateTimer();
</script>

<div style="box-shadow: 0 4px 8px rgba(0,0,0,0.1); border-radius: 10px; overflow: hidden; margin-top: 20px;">
    <table style="width: 100%; border-collapse: collapse; font-family: sans-serif; background-color: white;">
        <thead>
            <tr style="background: linear-gradient(90deg, #667eea 0%, #764ba2 100%); color: white; text-align: center;">
                <th style="padding: 15px;">Période</th>
                <th style="padding: 15px;">Horaires</th>
                <th style="padding: 15px;">Activité</th>
            </tr>
        </thead>
        <tbody style="text-align: center; color: #333;">
            <tr style="border-bottom: 1px solid #eee;">
                <td style="padding: 12px; font-weight: bold;">H1</td>
                <td style="padding: 12px;">07h15 – 08h00</td>
                <td style="padding: 12px;">👨‍💻 Cours</td>
            </tr>
            <tr style="border-bottom: 1px solid #eee;">
                <td style="padding: 12px; font-weight: bold;">H2</td>
                <td style="padding: 12px;">08h05 – 08h50</td>
                <td style="padding: 12px;">👨‍💻 Cours</td>
            </tr>
            <tr style="border-bottom: 1px solid #eee;">
                <td style="padding: 12px; font-weight: bold;">H3</td>
                <td style="padding: 12px;">08h55 – 09h40</td>
                <td style="padding: 12px;">👨‍💻 Cours</td>
            </tr>
            <tr style="background-color: #fff9c4; border-bottom: 1px solid #eee; font-weight: bold; color: #d84315;">
                <td style="padding: 12px;">Pause</td>
                <td style="padding: 12px;">09h40 – 10h05</td>
                <td style="padding: 12px;">☕ Grande Pause</td>
            </tr>
            <tr style="border-bottom: 1px solid #eee;">
                <td style="padding: 12px; font-weight: bold;">H4</td>
                <td style="padding: 12px;">10h05 – 10h50</td>
                <td style="padding: 12px;">👨‍💻 Cours</td>
            </tr>
            <tr style="border-bottom: 1px solid #eee;">
                <td style="padding: 12px; font-weight: bold;">H5</td>
                <td style="padding: 12px;">10h55 – 11h40</td>
                <td style="padding: 12px;">👨‍💻 Cours</td>
            </tr>
            <tr style="border-bottom: 1px solid #eee;">
                <td style="padding: 12px; font-weight: bold;">H6</td>
                <td style="padding: 12px;">11h45 – 12h30</td>
                <td style="padding: 12px;">👨‍💻 Cours</td>
            </tr>
            <tr style="background-color: #e1f5fe; border-bottom: 1px solid #eee; font-weight: bold; color: #0277bd;">
                <td style="padding: 12px;">Midi</td>
                <td style="padding: 12px;">12h30 – 12h40</td>
                <td style="padding: 12px;">🥪 Pause Déjeuner</td>
            </tr>
            <tr style="border-bottom: 1px solid #eee;">
                <td style="padding: 12px; font-weight: bold;">H7</td>
                <td style="padding: 12px;">12h40 – 13h25</td>
                <td style="padding: 12px;">👨‍💻 Cours</td>
            </tr>
            <tr style="border-bottom: 1px solid #eee;">
                <td style="padding: 12px; font-weight: bold;">H8</td>
                <td style="padding: 12px;">13h30 – 14h15</td>
                <td style="padding: 12px;">👨‍💻 Cours</td>
            </tr>
            <tr style="background-color: #fff9c4; border-bottom: 1px solid #eee; font-weight: bold; color: #d84315;">
                <td style="padding: 12px;">Pause</td>
                <td style="padding: 12px;">14h15 – 14h35</td>
                <td style="padding: 12px;">🥤 Pause</td>
            </tr>
            <tr style="border-bottom: 1px solid #eee;">
                <td style="padding: 12px; font-weight: bold;">H9</td>
                <td style="padding: 12px;">14h35 – 15h20</td>
                <td style="padding: 12px;">👨‍💻 Cours</td>
            </tr>
            <tr style="border-bottom: 1px solid #eee;">
                <td style="padding: 12px; font-weight: bold;">H10</td>
                <td style="padding: 12px;">15h25 – 16h10</td>
                <td style="padding: 12px;">👨‍💻 Cours</td>
            </tr>
            <tr style="border-bottom: 1px solid #eee;">
                <td style="padding: 12px; font-weight: bold;">H11</td>
                <td style="padding: 12px;">16h15 – 17h00</td>
                <td style="padding: 12px;">👨‍💻 Cours</td>
            </tr>
            <tr>
                <td style="padding: 12px; font-weight: bold;">H12</td>
                <td style="padding: 12px;">17h05 – 17h50</td>
                <td style="padding: 12px;">🏁 Fin des cours</td>
            </tr>
        </tbody>
    </table>
</div>