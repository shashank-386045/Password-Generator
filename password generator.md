### creating a password generator using HTML and java Script 
### aim:
password generator using coding languages HTML and java script
### algorithm:
Show UI controls: password length input, checkboxes for lowercase, uppercase, digits, symbols, a “Generate” button, and a “Copy” button.

Read the user-selected password length and which character types are enabled.

If no character type is selected, show an error and stop.

Build character pools for each type (lowercase, uppercase, digits, symbols).

Ensure password will contain at least one character from every enabled type by selecting one from each chosen pool.

Combine all enabled pools into a single availableChars pool for filling the remaining positions.

Fill remaining password length by randomly drawing characters from availableChars.

Shuffle the password characters so guaranteed-type characters are randomly placed.

Display the final password in the UI and enable the “Copy” button.

When the user clicks “Copy”, copy the password to the clipboard and show a success feedback.

program:

## HTML

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Password Generator</title>
    <style>
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            font-family: Arial, sans-serif;
            background-color: #f0f2f5;
        }
        .container {
            background-color: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }
        #result {
            background-color: #f8f9fa;
            padding: 10px;
            margin-bottom: 20px;
            border-radius: 5px;
            min-height: 20px;
            word-break: break-all;
        }
        .setting {
            margin: 10px 0;
        }
        button {
            background-color: #007bff;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
            margin: 5px;
        }
        button:hover {
            background-color: #0056b3;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>Password Generator</h2>
        <div id="result"></div>
        <div class="settings">
            <div class="setting">
                <label>Password Length</label>
                <input type="number" id="length" min="4" max="20" value="8">
            </div>
            <div class="setting">
                <label>Include Uppercase</label>
                <input type="checkbox" id="uppercase" checked>
            </div>
            <div class="setting">
                <label>Include Lowercase</label>
                <input type="checkbox" id="lowercase" checked>
            </div>
            <div class="setting">
                <label>Include Numbers</label>
                <input type="checkbox" id="numbers" checked>
            </div>
            <div class="setting">
                <label>Include Symbols</label>
                <input type="checkbox" id="symbols" checked>
            </div>
        </div>
        <button id="generate">Generate Password</button>
        <button id="clipboard">Copy to Clipboard</button>
    </div>
    <script src="password generator.js"></script>
</body>
</html>
```
## javascript
```
const resultEl = document.getElementById('result');
const lengthEl = document.getElementById('length');
const uppercaseEl = document.getElementById('uppercase');
const lowercaseEl = document.getElementById('lowercase');
const numbersEl = document.getElementById('numbers');
const symbolsEl = document.getElementById('symbols');
const generateEl = document.getElementById('generate');
const clipboardEl = document.getElementById('clipboard');

const randomFunc = {
    lower: getRandomLower,
    upper: getRandomUpper,
    number: getRandomNumber,
    symbol: getRandomSymbol
};

generateEl.addEventListener('click', () => {
    const length = +lengthEl.value;
    const hasLower = lowercaseEl.checked;
    const hasUpper = uppercaseEl.checked;
    const hasNumber = numbersEl.checked;
    const hasSymbol = symbolsEl.checked;
    
    resultEl.innerText = generatePassword(length, hasLower, hasUpper, hasNumber, hasSymbol);
});

clipboardEl.addEventListener('click', () => {
    if(!resultEl.innerText) { 
        return;
    }
    navigator.clipboard.writeText(resultEl.innerText)
        .then(() => {
            alert('Password copied to clipboard!');
        })
        .catch(err => {
            console.error('Failed to copy password:', err);
        });
});

function generatePassword(length, lower, upper, number, symbol) {
    let generatedPassword = '';
    const typesCount = lower + upper + number + symbol;
    const typesArr = [{lower}, {upper}, {number}, {symbol}].filter(item => Object.values(item)[0]);
    
    if(typesCount === 0) {
        return '';
    }
    
    for(let i = 0; i < length; i += typesCount) {
        typesArr.forEach(type => {
            const funcName = Object.keys(type)[0];
            generatedPassword += randomFunc[funcName]();
        });
    }
    
    return generatedPassword.slice(0, length);
}

function getRandomLower() {
    return String.fromCharCode(Math.floor(Math.random() * 26) + 97);
}

function getRandomUpper() {
    return String.fromCharCode(Math.floor(Math.random() * 26) + 65);
}

function getRandomNumber() {
    return String.fromCharCode(Math.floor(Math.random() * 10) + 48);
}

function getRandomSymbol() {
    const symbols = '!@#$%^&*(){}[]=<>/,.';
    return symbols[Math.floor(Math.random() * symbols.length)];
}
```
output:
<img width="935" height="891" alt="Screenshot 2025-10-22 193700" src="https://github.com/user-attachments/assets/31c11f33-ce97-431b-80fc-29cbbaec531a" />

```
## result:
The password generator project creates a secure, random password based on user-defined criteria (such as length and character types), using a simple web form and client-side scripting.




