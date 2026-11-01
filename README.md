🪐 ExoMind 3D: The AI Exoplanet Laboratory

An interactive 3D astronomy classroom that runs in the browser. Students change a planet's distance from its star, mass and greenhouse gases, and a decision tree trained on NASA Exoplanet Archive data classifies the world as Icy, Habitable or Lava Wasteland, while the 3D planet changes color, size and glow in real time.

Live demo: add your website link here

Features
Tab	What students do
🧪 Lab	Move 3 sliders (or click the Earth, Mars and Venus presets). See the habitability score, the ML decision path and a Science Academy explanation. Complete guided Missions.
🪐 Planets	Explore 8 planets plus Ceres and Pluto. Click a planet in 3D for facts, or send its real numbers to the Lab.
⭐ Stars	Change a star's mass and life stage to watch it grow into a giant, explode, or collapse into a white dwarf, neutron star or black hole.
🎯 Quiz	10 random questions per round from a pool of 16, with instant feedback and a score.
❓ Help	Searchable glossary of 23 common doubts (AU, greenhouse gas, black hole and more).

The 3D view has a glowing star, a green Goldilocks-zone ring (0.8 to 1.5 AU), an orbiting planet, and mouse controls: drag to rotate, scroll to zoom.

How to run it

Just open it: double-click index.html. You need an internet connection, because Three.js loads from a CDN.

No installation, build step or server is required.

The machine learning part
Model: scikit-learn DecisionTreeClassifier, max_depth=3.
Features: planet mass (Earth masses), effective distance from the star (AU), greenhouse factor (%).
Classes: 0 Icy, 1 Habitable, 2 Lava Wasteland.
Data: planets from the NASA Exoplanet Archive (mass, orbit and star luminosity). If the archive is unreachable, the script falls back to synthetic data.
Deployment: the script exports the learned thresholds as a JavaScript if/else function (mlPredict) that runs in the browser. The Habitability Score is the probability of the Habitable class at the leaf the planet lands in.
Retrain the model
bash
pip install pandas scikit-learn requests
python train_exoplanet_model.py

This prints the accuracy and the tree rules, and writes exoplanet_tree.js. Copy the function inside it over the old mlPredict function in index.html.

Honest limitations
NASA does not publish a "habitability class" and does not measure greenhouse gas. Labels come from simple climate physics (surface temperature with noise), and greenhouse values are simulated. The tree learns that physics. It does not discover facts about real habitability.
Real NASA data is about 97% hot (lava-type) planets, because telescopes find close-in planets most easily. A high accuracy number is therefore misleading, and the Habitable and Icy classes are learned from very few examples. Mixing in balanced synthetic data gives a more trustworthy tree.
Two rules sit outside the model as physics: a planet under 0.3 Earth masses becomes an airless rock, and one over 8 Earth masses becomes a gas giant.
In the Planets tab, sizes and distances are not to scale.
Project structure
index.html                  the whole app (HTML, CSS, JavaScript, Three.js via CDN)
train_exoplanet_model.py    trains the decision tree and exports it to JavaScript
exoplanet_tree.js           the latest trained tree (paste into index.html)
README.md                   this file
Built with

HTML, CSS, vanilla JavaScript, Three.js, Python, pandas, scikit-learn, NASA Exoplanet Archive.
