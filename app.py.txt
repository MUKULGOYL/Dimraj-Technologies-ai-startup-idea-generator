# AI Startup Idea Generator Web App using Flask

from flask import Flask, render_template_string, jsonify
import random

app = Flask(__name__)

ideas = [
    "AI-powered personal finance advisor",
    "Voice-controlled smart home system",
    "Healthcare diagnostics with computer vision",
    "AI tutor for school students",
    "Automated content creation for social media",
    "ML-driven stock market trend predictor",
    "AI-based resume analyzer for recruiters",
    "AI chatbot for e-commerce support",
    "Intelligent travel planner using user preferences",
    "Fitness tracking assistant with personalized AI coach"
]

html_template = """
<!DOCTYPE html>
<html lang='en'>
<head>
    <meta charset='UTF-8'>
    <meta name='viewport' content='width=device-width, initial-scale=1.0'>
    <title>Startup Idea Generator - Dimraj Tech</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background: #f0f2f5;
            padding-top: 100px;
        }
        h1 {
            color: #222;
        }
        #idea-box {
            background: white;
            padding: 2rem;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            display: inline-block;
            margin-top: 20px;
        }
        button {
            padding: 10px 20px;
            background-color: #111;
            color: white;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 1rem;
        }
    </style>
</head>
<body>
    <h1>🚀 AI Startup Idea Generator</h1>
    <div id="idea-box">
        <p id="idea">Click the button to get a startup idea!</p>
    </div>
    <br><br>
    <button onclick="getIdea()">Generate Idea</button>

    <script>
        async function getIdea() {
            const res = await fetch('/idea');
            const data = await res.json();
            document.getElementById('idea').innerText = data.idea;
        }
    </script>
</body>
</html>
"""

@app.route('/')
def home():
    return render_template_string(html_template)

@app.route('/idea')
def idea():
    return jsonify({"idea": random.choice(ideas)})

if __name__ == '__main__':
    app.run(debug=True)
