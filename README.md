# ChordGrid
Designed and written by Victor Paredes

A modular JavaScript library for visualizing guitar and stringed instrument fretboards with customizable themes, tunings, and chord displays.

## Overview

ChordGrid provides a complete fretboard visualization system that can be configured via three settings groups and initialized dynamically. It supports multiple instruments (guitar, mandolin, etc.), custom tunings, fret markers, themes, and interactive chord displays.

## Features

- 🎸 **Multi-instrument support** - Guitar, mandolin, and custom stringed instruments
- 🎨 **Customizable themes** - Multiple visual themes with CSS variable support
- 🎯 **Flexible tuning** - Support for standard and custom tunings
- 📍 **Fret markers** - Configurable single and double dot markers
- 🎵 **Chord visualization** - Display chords with fingering patterns
- 🎛️ **Control panel** - Optional real-time control interface
- 🔧 **Multiple instances** - Support for multiple fretboard instances on the same page

## Quick Start

### Basic HTML Setup

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ChordGrid Example</title>
    <link rel="stylesheet" href="css/fretboard.css">
    <link rel="stylesheet" href="css/fretboard_control_panel.css">
</head>
<body>
    <!-- Fretboard container -->
    <div id="fretboard-container">
        <div id="fretboard_1" data-fretboard="full" data-fretboard-id="my_fretboard"></div>
    </div>

    <!-- Optional control panel -->
    <div id="fretboard-control-panel" fretboard_target="my_fretboard">
        <h2>Fretboard Controls</h2>
    </div>

    <!-- Include ChordGrid scripts -->
    <script src="js/fretboard.js"></script>
    <script src="js/fretboard_control_panel.js"></script>
</body>
</html>
```

### Basic JavaScript Initialization

```javascript
Fretboard.init({
    containerId: 'fretboard_1',
    
    // Settings Group A - Fretboard Variables
    settingsGroupA: {
        dotTextMode: 'note',
        showFretIndicators: 'first-fret-cond',
        numStrings: 6,
        stringType: '1',
        tuning: {
            1: 'E',
            2: 'A',
            3: 'D',
            4: 'G',
            5: 'B',
            6: 'E'
        }
    },
    
    // Settings Group B - Fretboard Skin
    settingsGroupB: {
        fretMarkers: {
            3: 'single',
            5: 'single',
            7: 'single',
            9: 'single',
            12: 'double',
            15: 'single',
            17: 'single',
            19: 'single',
            21: 'single',
            24: 'double'
        },
        fretboardBindingDisplay: true
    }
});
```

## Configuration Examples

### Standard Guitar with Custom Theme

```javascript
Fretboard.init({
    containerId: 'fretboard_1',
    
    settingsGroupA: {
        dotTextMode: 'note',
        numStrings: 6,
        tuning: {
            1: 'E', 2: 'A', 3: 'D', 4: 'G', 5: 'B', 6: 'E'
        }
    },
    
    settingsGroupB: {
        fretMarkers: {
            3: 'single',
            5: 'single',
            7: 'single',
            9: 'single',
            12: 'double',
            15: 'single',
            17: 'single',
            19: 'single',
            21: 'single',
            24: 'double'
        },
        fretboardBindingDisplay: false,
        cssVariables: {
            '--string-1-default-color': 'linear-gradient(90deg, rgba(20, 20, 20, 1) 0%, rgba(60, 60, 60, 1) 50%, rgba(20, 20, 20, 1) 100%)'
        }
    },
    
    themes: {
        guitarEbony: {
            themeLabel: 'Ebony',
            fretMarkers: {
                3: 'single', 5: 'single', 7: 'single', 9: 'single',
                12: 'double', 15: 'single', 17: 'single', 19: 'single',
                21: 'single', 24: 'double'
            },
            fretboardBindingDisplay: false,
            cssVariables: {
                '--string-1-default-color': 'linear-gradient(90deg, rgba(20, 20, 20, 1) 0%, rgba(60, 60, 60, 1) 50%, rgba(20, 20, 20, 1) 100%)'
            }
        }
    }
});
```

### Mandolin Configuration

```javascript
Fretboard.init({
    containerId: 'fretboard_1',
    
    settingsGroupA: {
        numStrings: 4,
        stringType: '2',
        tuning: {
            1: 'G',
            2: 'D',
            3: 'A',
            4: 'E'
        }
    },
    
    instruments: {
        mandolin: {
            instrumentLabel: 'Mandolin',
            tuning: {
                1: 'G', 2: 'D', 3: 'A', 4: 'E'
            },
            numStrings: 4,
            stringType: '2'
        }
    },
    
    themes: {
        mandolinRosewood: {
            themeLabel: 'Rosewood',
            fretMarkers: {
                3: 'single', 5: 'single', 7: 'single', 9: 'single',
                12: 'double', 15: 'single', 17: 'single', 19: 'single',
                21: 'single', 24: 'double'
            },
            fretboardBindingDisplay: true
        }
    }
});
```

### Displaying a Chord

```javascript
Fretboard.init({
    containerId: 'fretboard_1',
    
    settingsGroupA: {
        numStrings: 6,
        tuning: {
            1: 'E', 2: 'A', 3: 'D', 4: 'G', 5: 'B', 6: 'E'
        }
    },
    
    // Settings Group C - Chord Variables
    settingsGroupC: {
        name: 'C Major',
        root: 'C',
        startFret: 1,
        numFrets: 4,
        fingering: [
            { string: 1, fret: 0 },  // Open string
            { string: 2, fret: 3 },  // 3rd fret
            { string: 3, fret: 0 },  // Open string
            { string: 4, fret: 0 },  // Open string
            { string: 5, fret: 1 },  // 1st fret
            { string: 6, fret: 0 }   // Open string
        ]
    }
});
```

## Dynamic Updates

You can update fretboard settings dynamically after initialization using the `updateSettingsGroupA`, `updateSettingsGroupB`, and `updateSettingsGroupC` methods. This is useful for creating interactive interfaces with buttons or other controls.

### Updating Settings Group A (Fretboard Variables)

```html
<button onclick="updateTuning()">Switch to Drop D Tuning</button>

<script>
function updateTuning() {
    window.Fretboard.updateSettingsGroupA({
        tuning: { 1: 'D', 2: 'A', 3: 'D', 4: 'G', 5: 'B', 6: 'E' },
        numStrings: 6,
        stringType: '1'
    }, 'fretboard-1');
}
</script>
```

### Updating Settings Group B (Fretboard Skin)

```html
<button onclick="updateTheme()">Apply Ebony Theme</button>

<script>
function updateTheme() {
    window.Fretboard.updateSettingsGroupB({
        fretMarkers: { 3: 'single', 12: 'double' },
        fretboardBindingDisplay: true,
        cssVariables: {
            '--string-1-default-color': 'linear-gradient(90deg, rgba(20, 20, 20, 1) 0%, rgba(60, 60, 60, 1) 50%, rgba(20, 20, 20, 1) 100%)'
        }
    }, 'fretboard-1');
}
</script>
```

### Updating Settings Group C (Chord Variables)

```html
<button onclick="displayChord()">Show C Major Chord</button>

<script>
function displayChord() {
    window.Fretboard.updateSettingsGroupC({
        name: 'C Major',
        root: 'C',
        fingering: [
            { string: 1, fret: 0, finger: 0 },
            { string: 2, fret: 1, finger: 1 },
            { string: 3, fret: 0, finger: 0 },
            { string: 4, fret: 2, finger: 2 },
            { string: 5, fret: 3, finger: 3 },
            { string: 6, fret: 0, finger: 0 }
        ],
        startFret: 1,
        numFrets: 12
    }, false, 'fretboard-1');
}
</script>
```

### Complete Example with Multiple Buttons

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Dynamic Fretboard Updates</title>
    <link rel="stylesheet" href="css/fretboard.css">
</head>
<body>
    <div id="fretboard-container">
        <div id="fretboard_1" data-fretboard="full" data-fretboard-id="fretboard-1"></div>
    </div>

    <div style="margin: 20px;">
        <h3>Fretboard Controls</h3>

        <button onclick="switchToStandardTuning()">Standard Tuning</button>
        <button onclick="switchToDropD()">Drop D Tuning</button>
        <button onclick="showCMajor()">C Major Chord</button>
        <button onclick="showGMajor()">G Major Chord</button>
    </div>

    <script src="js/fretboard.js"></script>
    <script>
        // Initialize fretboard
        Fretboard.init({
            containerId: 'fretboard_1',
            settingsGroupA: {
                numStrings: 6,
                tuning: { 1: 'E', 2: 'A', 3: 'D', 4: 'G', 5: 'B', 6: 'E' }
            }
        });

        // Update functions
        function switchToStandardTuning() {
            window.Fretboard.updateSettingsGroupA({
                tuning: { 1: 'E', 2: 'A', 3: 'D', 4: 'G', 5: 'B', 6: 'E' },
                numStrings: 6,
                stringType: '1'
            }, 'fretboard-1');
        }

        function switchToDropD() {
            window.Fretboard.updateSettingsGroupA({
                tuning: { 1: 'D', 2: 'A', 3: 'D', 4: 'G', 5: 'B', 6: 'E' },
                numStrings: 6,
                stringType: '1'
            }, 'fretboard-1');
        }

        function showCMajor() {
            window.Fretboard.updateSettingsGroupC({
                name: 'C Major',
                root: 'C',
                fingering: [
                    { string: 1, fret: 0, finger: 0 },
                    { string: 2, fret: 1, finger: 1 },
                    { string: 3, fret: 0, finger: 0 },
                    { string: 4, fret: 2, finger: 2 },
                    { string: 5, fret: 3, finger: 3 },
                    { string: 6, fret: 0, finger: 0 }
                ],
                startFret: 1,
                numFrets: 12
            }, false, 'fretboard-1');
        }

        function showGMajor() {
            window.Fretboard.updateSettingsGroupC({
                name: 'G Major',
                root: 'G',
                fingering: [
                    { string: 1, fret: 3, finger: 3 },
                    { string: 2, fret: 0, finger: 0 },
                    { string: 3, fret: 0, finger: 0 },
                    { string: 4, fret: 0, finger: 0 },
                    { string: 5, fret: 2, finger: 2 },
                    { string: 6, fret: 3, finger: 3 }
                ],
                startFret: 1,
                numFrets: 12
            }, false, 'fretboard-1');
        }
    </script>
</body>
</html>
```

**Note:** The second parameter in `updateSettingsGroupC` (set to `false` in the examples) controls whether to clear existing fingering before applying the new one. Set to `true` to clear, `false` to merge.

## Settings Groups

### Settings Group A - Fretboard Variables
- `dotTextMode`: Display mode for dots (`'note'`, `'fret'`, etc.)
- `showFretIndicators`: Fret indicator display (`'all'`, `'none'`, `'first-fret'`, `'first-fret-cond'`)
- `numStrings`: Number of strings (4-10)
- `stringType`: String type identifier
- `tuning`: Object mapping string numbers to note names
- `cssVariables`: CSS variable overrides

### Settings Group B - Fretboard Skin
- `fretMarkers`: Object mapping fret numbers to marker types (`'single'`, `'double'`)
- `fretboardBindingDisplay`: Boolean to show/hide fretboard bindings
- `cssVariables`: CSS variable overrides for visual styling

### Settings Group C - Chord Variables
- `name`: Chord name
- `root`: Root note
- `startFret`: Starting fret position
- `numFrets`: Number of frets to display
- `fingering`: Array of `{string, fret}` objects

## File Structure

```
ChordGrid/
├── css/
│   ├── fretboard.css
│   └── fretboard_control_panel.css
├── js/
│   ├── fretboard.js
│   └── fretboard_control_panel.js
├── examples/
│   ├── index.html
│   ├── notes.js
│   └── sample_api_input.js
└── img/
    ├── ebony.jpg
    ├── maple_sm.jpg
    ├── motherofpearl.jpg
    └── rosewood.jpg
```

## Browser Support

ChordGrid works in modern browsers that support ES6+ JavaScript and CSS Grid/Flexbox.

## License

TBD

