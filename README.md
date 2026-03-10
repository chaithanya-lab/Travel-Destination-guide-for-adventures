<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Global Adventure AI | 2026 Planner</title>
    <style>
        :root {
            --primary: #2a9d8f;
            --secondary: #264653;
            --accent: #e76f51;
            --glass: rgba(255, 255, 255, 0.9);
        }

        body {
            font-family: 'Inter', sans-serif;
            margin: 0;
            background: url('https://images.unsplash.com/photo-1488646953014-85cb44e25828?auto=format&fit=crop&w=1600&q=80') no-repeat center center fixed;
            background-size: cover;
            color: #333;
        }

        .overlay {
            background: rgba(0, 0, 0, 0.4);
            min-height: 100vh;
            padding: 40px 20px;
        }

        .container {
            max-width: 900px;
            margin: auto;
            background: var(--glass);
            padding: 30px;
            border-radius: 20px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.3);
            backdrop-filter: blur(10px);
        }

        h1 { text-align: center; color: var(--secondary); margin-bottom: 5px; }
        .subtitle { text-align: center; color: #666; margin-bottom: 30px; }

        .search-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-bottom: 25px;
        }

        input, select {
            padding: 15px;
            border: 1px solid #ddd;
            border-radius: 12px;
            font-size: 1rem;
            width: 100%;
            box-sizing: border-box;
        }

        .btn-search {
            grid-column: 1 / -1;
            background: var(--primary);
            color: white;
            border: none;
            padding: 18px;
            border-radius: 12px;
            font-weight: bold;
            font-size: 1.1rem;
            cursor: pointer;
            transition: 0.3s;
        }

        .btn-search:hover { background: var(--secondary); transform: scale(1.02); }

        /* Results Styles */
        #itineraryResult { display: none; margin-top: 40px; }
        
        .itinerary-card {
            background: white;
            margin-bottom: 15px;
            padding: 20px;
            border-radius: 15px;
            border-left: 6px solid var(--accent);
            animation: slideUp 0.5s ease-out;
        }

        .meta-info {
            display: flex;
            justify-content: space-around;
            background: #eee;
            padding: 15px;
            border-radius: 12px;
            margin-bottom: 25px;
            font-weight: bold;
        }

        @keyframes slideUp {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
    </style>
</head>
<body>

<div class="overlay">
    <div class="container">
        <h1>Global Adventure AI</h1>
        <p class="subtitle">Real-time trip logic for 2026</p>

        <div class="search-grid">
            <input type="text" id="country" placeholder="Enter Country (e.g. Japan, Iceland, Peru)">
            <input type="date" id="travelDate">
            <select id="duration">
                <option value="3">3 Days Adventure</option>
                <option value="5">5 Days Expedition</option>
                <option value="7">1 Week Journey</option>
                <option value="10">10 Days Grand Tour</option>
            </select>
            <button class="btn-search" onclick="fetchTravelPlan()">Generate Real-Time Plan</button>
        </div>

        <div id="itineraryResult">
            <div class="meta-info">
                <span id="resWeather">☁️ Loading Weather...</span>
                <span id="resBudget">💰 Est. Cost: --</span>
                <span id="resSeason">📅 Season: --</span>
            </div>
            <div id="planContent"></div>
        </div>
    </div>
</div>

<script>
    // Simulated Knowledge Base for 2026 Destinations
    const travelDB = {
        "japan": { destinations: ["Tokyo", "Kyoto", "Hokkaido", "Osaka"], adventures: ["Summit Mt. Fuji", "Mario Kart Street Racing", "Onsen Retreat", "Robot Cafe Tour"], cost: 200 },
        "iceland": { destinations: ["Reykjavík", "Vík", "Akureyri"], adventures: ["Northern Lights Chase", "Blue Lagoon Soak", "Glacier Trekking", "Black Sand Beach Photo Ops"], cost: 250 },
        "peru": { destinations: ["Cusco", "Lima", "Sacred Valley"], adventures: ["Machu Picchu Sunrise hike", "Amazon Jungle Safari", "Sandboarding in Huacachina"], cost: 120 },
        "italy": { destinations: ["Rome", "Florence", "Amalfi Coast", "Venice"], adventures: ["Colosseum Underground Tour", "Pasta Making in Tuscany", "Gondola Serenade"], cost: 180 }
    };

    function fetchTravelPlan() {
        const countryInput = document.getElementById('country').value.toLowerCase().trim();
        const duration = parseInt(document.getElementById('duration').value);
        const dateInput = document.getElementById('travelDate').value;

        if (!countryInput || !dateInput) {
            alert("Please provide the country and your travel date!");
            return;
        }

        const data = travelDB[countryInput] || { 
            destinations: ["The Capital City", "Coastal Region", "Mountain Highlands"], 
            adventures: ["Local Food Tour", "Hidden Landmark Hike", "Sunset Viewing"], 
            cost: 150 
        };

        // Display Area
        document.getElementById('itineraryResult').style.display = 'block';
        const planContent = document.getElementById('planContent');
        planContent.innerHTML = "";

        // Update Meta Info
        document.getElementById('resWeather').innerText = `☀️ 22°C (Typical for ${countryInput})`;
        document.getElementById('resBudget').innerText = `💰 Est. Budget: $${data.cost * duration}`;
        document.getElementById('resSeason').innerText = `📅 Best for: Adventure`;

        // Generate Itinerary
        for (let i = 1; i <= duration; i++) {
            const dest = data.destinations[i % data.destinations.length];
            const adv = data.adventures[i % data.adventures.length];
            
            const dayDiv = document.createElement('div');
            dayDiv.className = 'itinerary-card';
            dayDiv.innerHTML = `
                <h3>Day ${i}: Explore ${dest}</h3>
                <p><strong>Primary Adventure:</strong> ${adv}</p>
                <p><strong>Details:</strong> Experience the best of ${countryInput} with a deep-dive into ${dest}'s local culture and scenery on ${dateInput}.</p>
                <small style="color: var(--primary)">#Adventure2026 #${countryInput}Travel</small>
            `;
            planContent.appendChild(dayDiv);
        }
        
        window.scrollTo({ top: 500, behavior: 'smooth' });
    }
</script>

</body>
</html># Travel-Destination-guide-for-adventures
