# source.py
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Campus Energy Dashboard</title>
    <style>
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; margin: 30px; background-color: #f4f6f9; color: #333; }
        h1 { color: #2c3e50; border-bottom: 2px solid #ecf0f1; padding-bottom: 10px; }
        .grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 20px; margin-top: 20px; }
        .card { background: white; padding: 20px; border-radius: 8px; box-shadow: 0 4px 6px rgba(0,0,0,0.05); border-top: 5px solid #3498db; }
        .warning { background-color: #fdf2f2; border-top: 5px solid #e74c3c; }
        .alert-text { color: #c0392b; font-weight: bold; margin-top: 15px; font-size: 0.95em; padding: 8px; background: #f9d5d5; border-radius: 4px; }
        .metric { font-size: 1.1em; margin: 10px 0; }
        strong { color: #2c3e50; }
    </style>
</head>
<body>

    <h1>Campus Energy Monitoring Dashboard</h1>
    
    <div class="grid" id="dashboard-grid">
        <!-- Dashboard cards are generated dynamically -->
    </div>

    <script>
        // Sample data for the three campus buildings
        const campusData = [
            { name: "Science Block", consumption: 125, target: 90 },
            { name: "Arts Pavilion", consumption: 75, target: 80 },
            { name: "Engineering Lab", consumption: 140, target: 100 }
        ];

        const grid = document.getElementById('dashboard-grid');

        campusData.forEach(building => {
            const card = document.createElement('div');
            card.className = 'card';
            
            let alertHTML = '';
            // Trigger warning configuration if consumption > 100 kWh
            if (building.consumption > 100) {
                card.classList.add('warning');
                const excess = building.consumption - 100;
                alertHTML = `<div class="alert-text">⚠️ Alert: Exceeded 100 kWh limit by ${excess} kWh!</div>`;
            }

            card.innerHTML = `
                <h3>${building.name}</h3>
                <p class="metric"><strong>Daily Consumption:</strong> ${building.consumption} kWh</p>
                <p class="metric"><strong>Saving Target:</strong> ${building.target} kWh</p>
                ${alertHTML}
            `;
            grid.appendChild(card);
        });
    </script>
</body>
</html>
