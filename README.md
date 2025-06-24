<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Interactive Interface</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        /* Custom styles for the Inter font and a smooth appearance */
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f0f4f8; /* Light gray background */
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh; /* Full viewport height */
            margin: 0;
            padding: 20px; /* Add some padding around the content */
            box-sizing: border-box; /* Include padding in element's total width and height */
        }
        .container {
            background-color: #ffffff; /* White background for the main container */
            border-radius: 1.5rem; /* More rounded corners */
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04); /* Deeper shadow */
            max-width: 600px;
            width: 100%;
            padding: 2.5rem; /* More padding inside */
            display: flex;
            flex-direction: column;
            gap: 1.5rem; /* Space between sections */
        }
        .section-title {
            font-size: 1.75rem; /* Larger title */
            font-weight: 700; /* Bold */
            color: #1a202c; /* Dark text color */
            margin-bottom: 1rem;
            text-align: center;
        }
        .button {
            transition: all 0.2s ease-in-out; /* Smooth transition for hover effects */
        }
        .button:hover {
            transform: translateY(-2px); /* Slight lift on hover */
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05); /* Larger shadow on hover */
        }
        /* Custom focus styles for better accessibility */
        .button:focus, .slider:focus {
            outline: 2px solid #6366f1; /* Indigo focus ring */
            outline-offset: 2px;
        }
        .slider-container {
            display: flex;
            flex-direction: column;
            gap: 0.5rem;
        }
        .slider-label {
            font-weight: 500;
            color: #4a5568;
        }
        .slider {
            width: 100%;
            -webkit-appearance: none; /* Remove default styling for webkit browsers */
            appearance: none;
            height: 8px; /* Thinner slider track */
            background: #e2e8f0; /* Light background for track */
            outline: none;
            border-radius: 4px;
            transition: opacity .2s;
        }
        .slider::-webkit-slider-thumb {
            -webkit-appearance: none;
            appearance: none;
            width: 20px; /* Larger thumb */
            height: 20px;
            border-radius: 50%; /* Circular thumb */
            background: #6366f1; /* Indigo thumb */
            cursor: pointer;
            box-shadow: 0 2px 5px rgba(0,0,0,0.2); /* Thumb shadow */
        }
        .slider::-moz-range-thumb {
            width: 20px;
            height: 20px;
            border-radius: 50%;
            background: #6366f1;
            cursor: pointer;
            box-shadow: 0 2px 5px rgba(0,0,0,0.2);
        }
        .message-box {
            background-color: #e0f2f7; /* Light blue */
            color: #0c4a6e; /* Darker blue text */
            padding: 1rem;
            border-radius: 0.75rem;
            text-align: center;
            font-weight: 600;
            margin-top: 1.5rem;
            display: none; /* Hidden by default */
            transition: opacity 0.3s ease-in-out;
            opacity: 0;
        }
        .message-box.show {
            display: block;
            opacity: 1;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1 class="section-title">Interactive Control Panel</h1>

        <!-- Buttons Section -->
        <div class="space-y-4">
            <h2 class="text-xl font-semibold text-gray-800 text-center">Actions</h2>
            <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                <button id="button1" class="button bg-indigo-500 hover:bg-indigo-600 text-white font-bold py-3 px-6 rounded-xl shadow-lg">
                    Primary Action
                </button>
                <button id="button2" class="button bg-green-500 hover:bg-green-600 text-white font-bold py-3 px-6 rounded-xl shadow-lg">
                    Confirm Choice
                </button>
                <button id="button3" class="button bg-yellow-500 hover:bg-yellow-600 text-white font-bold py-3 px-6 rounded-xl shadow-lg">
                    Warning Alert
                </button>
                <button id="button4" class="button bg-red-500 hover:bg-red-600 text-white font-bold py-3 px-6 rounded-xl shadow-lg">
                    Delete Item
                </button>
            </div>
        </div>

        <!-- Sliders Section -->
        <div class="space-y-4">
            <h2 class="text-xl font-semibold text-gray-800 text-center">Settings</h2>
            <div class="slider-container">
                <label for="volumeSlider" class="slider-label">Volume: <span id="volumeValue">50</span></label>
                <input type="range" id="volumeSlider" min="0" max="100" value="50" class="slider">
            </div>
            <div class="slider-container">
                <label for="brightnessSlider" class="slider-label">Brightness: <span id="brightnessValue">75</span></label>
                <input type="range" id="brightnessSlider" min="0" max="100" value="75" class="slider">
            </div>
            <div class="slider-container">
                <label for="contrastSlider" class="slider-label">Contrast: <span id="contrastValue">0</span></label>
                <input type="range" id="contrastSlider" min="-50" max="50" value="0" class="slider">
            </div>
        </div>

        <!-- Message Box -->
        <div id="messageBox" class="message-box">
            <!-- Messages will appear here -->
        </div>
    </div>

    <script>
        // Function to show a message in the message box
        function showMessage(message, duration = 3000) {
            const messageBox = document.getElementById('messageBox');
            messageBox.textContent = message;
            messageBox.classList.add('show');

            // Hide the message after 'duration' milliseconds
            setTimeout(() => {
                messageBox.classList.remove('show');
            }, duration);
        }

        // Button Event Listeners
        document.getElementById('button1').addEventListener('click', () => {
            showMessage('Primary Action button clicked!');
        });

        document.getElementById('button2').addEventListener('click', () => {
            showMessage('Confirm Choice button clicked!');
        });

        document.getElementById('button3').addEventListener('click', () => {
            showMessage('Warning Alert button clicked!');
        });

        document.getElementById('button4').addEventListener('click', () => {
            showMessage('Delete Item button clicked! (Not really deleted)');
        });

        // Slider Event Listeners
        const volumeSlider = document.getElementById('volumeSlider');
        const volumeValue = document.getElementById('volumeValue');
        volumeSlider.addEventListener('input', () => {
            volumeValue.textContent = volumeSlider.value;
            showMessage(`Volume set to: ${volumeSlider.value}`, 1000);
        });

        const brightnessSlider = document.getElementById('brightnessSlider');
        const brightnessValue = document.getElementById('brightnessValue');
        brightnessSlider.addEventListener('input', () => {
            brightnessValue.textContent = brightnessSlider.value;
            showMessage(`Brightness set to: ${brightnessSlider.value}`, 1000);
        });

        const contrastSlider = document.getElementById('contrastSlider');
        const contrastValue = document.getElementById('contrastValue');
        contrastSlider.addEventListener('input', () => {
            contrastValue.textContent = contrastSlider.value;
            showMessage(`Contrast set to: ${contrastSlider.value}`, 1000);
        });

        // Initial update for slider values
        window.onload = () => {
            volumeValue.textContent = volumeSlider.value;
            brightnessValue.textContent = brightnessSlider.value;
            contrastValue.textContent = contrastSlider.value;
        };
    </script>
</body>
</html>
