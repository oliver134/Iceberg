// ==UserScript==
// @name        Iceberg Farm
// @namespace   Violentmonkey Scripts
// @match       *://0xiceberg.com/webapp/*
// @grant       none
// @version     1.0
// @description  
// @author      Emin M
// @icon        https://github.com/oliver134/Iceberg/blob/main/iceberg.png
// @downloadURL
// @updateURL
// @homepage     
// ==/UserScript==

(function() {
    'use strict';

    // Mobile User-Agent for Telegram on iPhone and Android devices
    const telegramUserAgent = {
        iphone: "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Mobile/15E148 Safari/604.1",
        xiaomi: "Mozilla/5.0 (Linux; Android 10; Mi 9T Pro) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/88.0.4324.152 Mobile Safari/537.36 TelegramBot (like TwitterBot)",
        samsung: "Mozilla/5.0 (Linux; Android 11; SAMSUNG SM-N986B) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.77 Mobile Safari/537.36 TelegramBot (like TwitterBot)"
    };

    // Choose the User-Agent based on the desired device
    const userAgent = telegramUserAgent.samsung; // Change to 'iphone' or 'xiaomi' as needed

    // Override the User-Agent
    Object.defineProperty(navigator, 'userAgent', {
        get: function() { return userAgent; }
    });

    // Function to click the first button with the initial SVG
    function clickFirstButton() {
        const buttons = document.querySelectorAll('button.chakra-button.css-g8p8ek');

        for (let button of buttons) {
            const svg = button.querySelector('svg[viewBox="0 0 512 512"]');
            if (svg) {
                button.click();
                return true;
            }
        }
        return false;
    }

    // Function to click the second button within the specified div and containing the text "Start farming"
    function clickSecondButton() {
        const divs = document.querySelectorAll('div.chakra-offset-slide');

        for (let div of divs) {
            const button = div.querySelector('button.chakra-button.css-3gq9if');
            if (button && button.textContent.includes('Start farming')) {
                button.click();
                return true;
            }
        }
        return false;
    }

    function searchAndClickButtons() {
        const foundFirstButton = clickFirstButton();

        if (!foundFirstButton) {
            const foundSecondButton = clickSecondButton();

            if (!foundSecondButton) {
                setTimeout(searchAndClickButtons, 500); // Retry every 500ms if neither button is found
            }
        }
    }

    // Function to start the process and repeat every 10 seconds
    function startProcess() {
        searchAndClickButtons();
        setTimeout(startProcess, 10000); // Repeat every 10 seconds
    }

    // Run the initial function once the page is fully loaded
    window.addEventListener('load', () => {
        startProcess();
    });
})();

