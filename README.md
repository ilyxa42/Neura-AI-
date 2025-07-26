<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEURA</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        /* Общие переменные и базовые стили */
        :root {
            /* Dark Theme Variables */
            --dark-purple: #0A0015;
            --medium-purple: #1F0040;
            --light-purple: #8A2BE2;
            --accent-blue: #ADD8E6;
            --text-color-light: #f0f0f0;
            --text-color-medium: #bbb;
            --text-color-dark: #888;
            --sidebar-bg: #150025;
            --sidebar-border: #300060;
            --top-bar-bg: #1A0035;
            --chat-bg-ai: #1A0035;
            --chat-bg-user: linear-gradient(135deg, #4d0099, #6a00cd);
            --input-bg: #330066;
            --input-border: #4d0099;
            --input-focus-bg: #38006d;
            --button-primary-bg: linear-gradient(45deg, var(--light-purple), var(--accent-blue));
            --button-primary-hover-bg: linear-gradient(45deg, #a04aff, #c2e0f2);
            --button-secondary-bg: var(--medium-purple);
            --button-secondary-hover-bg: #300060;
            --settings-modal-bg: linear-gradient(to top, #150025 0%, #080010 100%);
            --settings-item-bg: var(--medium-purple);
            --settings-item-hover-bg: #300060;
            --settings-input-bg: #200040;
            --settings-border-line: #200040;
            --bg-gradient-1: rgba(43, 0, 85, 0.4);
            --bg-gradient-2: rgba(26, 0, 51, 0.4);
            --bg-gradient-3: var(--dark-purple);
            --bg-gradient-4: #05000A;
            --main-content-gradient-1: rgba(43, 0, 85, 0.2);
            --main-content-gradient-2: rgba(26, 0, 51, 0.2);
            --main-content-gradient-3: var(--dark-purple);
            --main-content-gradient-4: #05000A;
        }

        /* Light Theme Variables */
        body.light-theme {
            --dark-purple: #F8F8F8;
            --medium-purple: #EAEAEA;
            --light-purple: #8A2BE2; /* Keep accent colors */
            --accent-blue: #ADD8E6; /* Keep accent colors */
            --text-color-light: #333;
            --text-color-medium: #555;
            --text-color-dark: #777;
            --sidebar-bg: #FFFFFF;
            --sidebar-border: #E0E0E0;
            --top-bar-bg: #F5F5F5;
            --chat-bg-ai: #F2F2F2;
            --chat-bg-user: linear-gradient(135deg, #a04aff, #c2e0f2); /* Lighter user chat */
            --input-bg: #FFFFFF;
            --input-border: #DDD;
            --input-focus-bg: #F5F5F5;
            --button-primary-bg: linear-gradient(45deg, var(--light-purple), var(--accent-blue));
            --button-primary-hover-bg: linear-gradient(45deg, #a04aff, #c2e0f2);
            --button-secondary-bg: #E0E0E0;
            --button-secondary-hover-bg: #DCDCDC;
            --settings-modal-bg: linear-gradient(to top, #F0F0F0 0%, #FFFFFF 100%);
            --settings-item-bg: #F8F8F8;
            --settings-item-hover-bg: #F0F0F0;
            --settings-input-bg: #F2F2F2;
            --settings-border-line: #EAEAEA;
            --bg-gradient-1: rgba(200, 200, 255, 0.2);
            --bg-gradient-2: rgba(220, 220, 255, 0.2);
            --bg-gradient-3: #F0F0F0;
            --bg-gradient-4: #FFFFFF;
            --main-content-gradient-1: rgba(200, 200, 255, 0.1);
            --main-content-gradient-2: rgba(220, 220, 255, 0.1);
            --main-content-gradient-3: #F0F0F0;
            --main-content-gradient-4: #FFFFFF;
        }

        :root {
            --sidebar-width: 280px;
            --top-bar-height: 60px; /* Adjust based on actual top-bar height, set by JS */
            --chat-input-area-height: 100px; /* Approximate height of input area, set by JS */
        }

        body {
            font-family: 'Inter', sans-serif;
            margin: 0;
            padding: 0;
            background: radial-gradient(circle at top left, var(--bg-gradient-1) 0%, transparent 40%),
                        radial-gradient(circle at bottom right, var(--bg-gradient-2) 0%, transparent 50%),
                        linear-gradient(to bottom, var(--bg-gradient-3) 0%, var(--bg-gradient-4) 100%);
            color: var(--text-color-light);
            display: flex;
            min-height: 100vh;
            overflow: hidden;
            box-sizing: border-box;
            -webkit-font-smoothing: antialiased;
            text-rendering: optimizeLegibility;
            position: relative;
            transition: background 0.5s ease, color 0.5s ease;
        }

        /* Эффект шума/зерна на фоне */
        body::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-image: url('data:image/svg+xml;utf8,<svg width="100%" height="100%" viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg"><filter id="noiseFilter"><feTurbulence type="fractalNoise" baseFrequency="0.6" numOctaves="3" stitchTiles="stitch"/></filter><rect width="100%" height="100%" filter="url(#noiseFilter)" opacity="0.05"/></svg>');
            pointer-events: none;
            z-index: -1;
        }

        /* Анимированные фоновые линии */
        body::after {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: repeating-linear-gradient(
                45deg,
                rgba(138, 43, 226, 0.03),
                rgba(138, 43, 226, 0.03) 2px,
                transparent 2px,
                transparent 20px
            ),
            repeating-linear-gradient(
                -45deg,
                rgba(173, 216, 230, 0.03),
                rgba(173, 216, 230, 0.03) 2px,
                transparent 2px,
                transparent 20px
            );
            animation: moveLines 60s linear infinite;
            pointer-events: none;
            z-index: -2;
            opacity: 0.8;
        }

        @keyframes moveLines {
            0% { background-position: 0 0; }
            100% { background-position: 100vw 100vh; }
        }

        /* Основной контейнер приложения */
        .app-wrapper {
            display: flex;
            width: 100%;
            height: 100vh;
            overflow: hidden;
        }

        /* Боковая панель (Sidebar) */
        .sidebar {
            width: var(--sidebar-width);
            min-width: var(--sidebar-width);
            background-color: var(--sidebar-bg);
            padding: 20px;
            display: flex;
            flex-direction: column;
            box-shadow: 2px 0 20px rgba(0, 0, 0, 0.6);
            position: fixed; /* Changed to fixed to be fully off-screen */
            top: 0;
            left: 0;
            height: 100vh;
            z-index: 200;
            transform: translateX(calc(-1 * var(--sidebar-width))); /* Fully off-screen by default */
            transition: transform 0.4s cubic-bezier(0.25, 0.1, 0.25, 1), background-color 0.5s ease, border-right-color 0.5s ease;
            flex-shrink: 0;
            overflow-y: auto;
            border-right: 1px solid var(--sidebar-border);
        }

        .sidebar.active {
            transform: translateX(0); /* Slide in */
        }

        .sidebar-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 1px solid var(--sidebar-border);
            transition: all 0.4s ease, border-bottom-color 0.5s ease;
        }

        .sidebar-header .logo {
            font-size: 28px;
            font-weight: 700;
            background: linear-gradient(45deg, var(--light-purple), var(--accent-blue));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            text-shadow: 0 0 12px rgba(138, 43, 226, 0.7);
            white-space: nowrap;
            transition: font-size 0.4s ease, width 0.4s ease;
        }

        .new-chat-button {
            background: linear-gradient(90deg, #4d0099, #6a00cd);
            color: var(--text-color-light);
            padding: 12px 18px;
            border-radius: 25px;
            border: none;
            cursor: pointer;
            font-size: 16px;
            font-weight: 500;
            display: flex;
            align-items: center;
            gap: 8px;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.4);
            white-space: nowrap;
            flex-shrink: 0;
        }

        .new-chat-button:hover {
            background: linear-gradient(90deg, #6a00cd, #8a00ff);
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(0, 0, 0, 0.6), 0 0 10px rgba(138, 43, 226, 0.5);
        }
        .new-chat-button:active {
            transform: translateY(0);
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
        }

        .sidebar-nav {
            margin-top: 20px;
            flex-grow: 1;
            padding-right: 5px;
            overflow-y: auto;
            scrollbar-width: thin;
            scrollbar-color: #4d0099 #180030;
        }
        .sidebar-nav::-webkit-scrollbar {
            width: 8px;
        }
        .sidebar-nav::-webkit-scrollbar-track {
            background: #180030;
        }
        .sidebar-nav::-webkit-scrollbar-thumb {
            background-color: #4d0099;
            border-radius: 10px;
            border: 2px solid #180030;
        }

        .sidebar-nav ul {
            list-style: none;
            padding: 0;
            margin: 0;
        }

        .sidebar-nav ul li {
            margin-bottom: 8px;
        }

        .sidebar-nav a, .sidebar-bottom-button {
            display: flex;
            align-items: center;
            gap: 12px;
            padding: 12px 15px;
            border-radius: 10px;
            color: var(--text-color-medium);
            text-decoration: none;
            transition: all 0.2s ease-out, background-color 0.5s ease, color 0.5s ease;
            font-size: 16px;
            cursor: pointer;
            background-color: transparent;
            border: none;
            width: 100%;
            box-sizing: border-box;
            text-align: left;
            position: relative;
            overflow: hidden;
            z-index: 1;
        }

        .sidebar-nav a::before, .sidebar-bottom-button::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, rgba(138,43,226,0.2) 0%, rgba(173,216,230,0.1) 100%);
            opacity: 0;
            transition: opacity 0.3s ease;
            z-index: -1;
        }

        .sidebar-nav a:hover, .sidebar-bottom-button:hover {
            color: var(--text-color-light);
            background-color: var(--button-secondary-hover-bg);
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
        }
        .sidebar-nav a:hover::before, .sidebar-bottom-button:hover::before {
             opacity: 1;
        }

        .sidebar-nav a.active {
            background-color: var(--medium-purple);
            color: var(--text-color-light);
            font-weight: 600;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.4);
            transition: background-color 0.5s ease, color 0.5s ease;
        }
        .sidebar-nav a.active::before {
            opacity: 0.5;
        }

        .sidebar-nav svg, .sidebar-bottom-button svg, .new-chat-button svg {
            width: 20px;
            height: 20px;
            fill: currentColor;
            transition: fill 0.2s ease;
            flex-shrink: 0;
        }

        .sidebar-nav a.active svg {
            fill: var(--light-purple);
            filter: drop-shadow(0 0 5px rgba(138,43,226,0.6));
        }
        .new-chat-button svg {
            filter: drop-shadow(0 0 5px rgba(255,255,255,0.3));
        }

        .chat-history-title {
            color: var(--text-color-dark);
            font-size: 13px;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            margin-top: 25px;
            margin-bottom: 10px;
            padding-left: 15px;
            font-weight: 500;
            white-space: nowrap;
            transition: color 0.5s ease;
        }

        .chat-history ul {
            max-height: 200px;
            overflow-y: auto;
            list-style: none;
            padding: 0;
            margin: 0;
            box-sizing: border-box;
            width: 100%;
        }

        .chat-history ul li a {
            font-size: 14px;
            padding: 8px 15px;
            margin-bottom: 5px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            width: 100%;
            box-sizing: border-box;
        }
        .chat-history-item-text {
            flex-grow: 1;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
            min-width: 0;
        }

        .chat-history-item-delete {
            background: none;
            border: none;
            color: var(--text-color-dark);
            font-size: 18px;
            cursor: pointer;
            margin-left: 10px;
            opacity: 0;
            transition: opacity 0.2s ease, color 0.2s ease;
            line-height: 1;
            width: 20px;
            height: 20px;
            display: flex;
            align-items: center;
            justify-content: center;
            flex-shrink: 0;
        }
        .chat-history ul li:hover .chat-history-item-delete {
            opacity: 1;
        }
        .chat-history-item-delete:hover {
            color: var(--text-color-light);
        }


        .sidebar-bottom {
            margin-top: auto;
            padding-top: 20px;
            border-top: 1px solid var(--sidebar-border);
            padding-right: 5px;
            transition: border-top-color 0.5s ease;
        }

        /* Основной контент */
        .main-content {
            flex-grow: 1;
            display: flex;
            flex-direction: column;
            background: radial-gradient(circle at top right, var(--main-content-gradient-1) 0%, transparent 40%),
                        radial-gradient(circle at bottom left, var(--main-content-gradient-2) 0%, transparent 50%),
                        linear-gradient(to top, var(--main-content-gradient-3) 0%, var(--main-content-gradient-4) 100%);
            position: relative;
            overflow: hidden;
            box-shadow: inset 0 0 20px rgba(0, 0, 0, 0.3);
            transition: background 0.5s ease;
            width: 100%; /* Ensure main content takes full width */
        }

        .top-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px 25px;
            background-color: var(--top-bar-bg);
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
            flex-shrink: 0;
            z-index: 50;
            border-bottom: 1px solid var(--sidebar-border);
            transition: background-color 0.5s ease, border-bottom-color 0.5s ease;
        }

        .top-bar .title {
            font-size: 22px;
            font-weight: 600;
            color: var(--text-color-light);
            text-shadow: 0 0 8px rgba(173, 216, 230, 0.5);
            flex-grow: 1;
            text-align: center;
            transition: color 0.5s ease;
        }
        .top-bar .menu-toggle {
            margin-right: 15px;
        }
        .top-bar > div:last-child {
            width: 26px; /* Balance the menu toggle on the left */
        }


        .menu-toggle {
            background: none;
            border: none;
            color: var(--text-color-light);
            font-size: 26px;
            cursor: pointer;
            padding: 5px;
            border-radius: 5px;
            transition: background-color 0.2s ease, transform 0.2s ease, color 0.5s ease;
            display: block; /* Always visible to toggle sidebar */
        }
        .menu-toggle:hover {
            background-color: rgba(255, 255, 255, 0.1);
            transform: scale(1.1);
        }
        .menu-toggle svg {
            width: 26px;
            height: 26px;
            fill: currentColor;
            filter: drop-shadow(0 0 5px rgba(255,255,255,0.3));
        }

        /* Переключаемые секции контента */
        .content-section {
            flex-grow: 1;
            padding: 20px 30px;
            overflow-y: auto;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: flex-start;
            position: absolute;
            top: var(--top-bar-height);
            left: 0;
            width: 100%;
            height: calc(100% - var(--top-bar-height));
            opacity: 0;
            visibility: hidden;
            transform: translateY(20px);
            transition: opacity 0.5s ease-out, visibility 0.5s ease-out, transform 0.5s ease-out;
            box-sizing: border-box;
            pointer-events: none;
        }

        .content-section.active {
            opacity: 1;
            visibility: visible;
            transform: translateY(0);
            z-index: 1;
            pointer-events: auto;
        }
        .content-section h2 {
            font-size: 38px;
            margin-bottom: 30px;
            text-align: center;
            background: linear-gradient(45deg, var(--accent-blue), var(--light-purple));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            text-shadow: 0 0 15px rgba(173, 216, 230, 0.8);
            font-weight: 700;
            transition: text-shadow 0.5s ease;
        }
        .content-section p, .content-section ul {
            font-size: 17px;
            line-height: 1.7;
            margin-bottom: 20px;
            color: var(--text-color-medium);
            max-width: 800px;
            text-align: justify;
            width: 100%;
            box-sizing: border-box;
            padding: 0 10px;
            transition: color 0.5s ease;
        }
        .content-section ul {
            list-style: none;
            padding: 0;
            margin: 0;
            width: 100%;
        }
        .content-section ul li {
            background-color: var(--medium-purple);
            padding: 18px 25px;
            border-radius: 15px;
            margin-bottom: 15px;
            display: flex;
            align-items: flex-start;
            gap: 20px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
            color: var(--text-color-light);
            transition: transform 0.2s ease, box-shadow 0.2s ease, background-color 0.5s ease, border-color 0.5s ease, color 0.5s ease;
            border: 1px solid rgba(138,43,226,0.3);
        }
        .content-section ul li:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.4);
            border-color: var(--light-purple);
        }
        .content-section ul li span {
            color: var(--light-purple);
            font-size: 24px;
            line-height: 1;
            filter: drop-shadow(0 0 8px rgba(138,43,226,0.8));
        }

        /* Главный экран (для чата) */
        .main-chat-screen {
            flex-grow: 1;
            display: flex;
            flex-direction: column;
            padding: 0 20px;
            box-sizing: border-box;
            max-width: 900px;
            margin: 0 auto;
            width: 100%;
            position: relative;
            height: calc(100% - var(--top-bar-height) - var(--chat-input-area-height));
            overflow-y: hidden;
        }
        @media (max-width: 768px) {
            .main-chat-screen {
                padding: 0 15px;
            }
        }

        /* Приветствие в чате - Centered */
        .main-chat-screen .greeting {
            text-align: center;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            flex-grow: 1;
            transition: opacity 0.3s ease, transform 0.3s ease, visibility 0.3s ease, height 0.3s ease, margin-bottom 0.3s ease;
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 100%;
            box-sizing: border-box;
            max-width: 800px;
            height: auto;
            z-index: 0;
            padding: 20px;
        }
        @media (max-width: 768px) {
            .main-chat-screen .greeting {
                top: calc(50% - (var(--top-bar-height) / 2));
            }
        }
        /* Neon glow effect for greeting */
        @keyframes glowing {
            0% { text-shadow: 0 0 10px var(--accent-blue), 0 0 20px var(--light-purple), 0 0 30px var(--accent-blue); }
            50% { text-shadow: 0 0 15px var(--light-purple), 0 0 25px var(--accent-blue), 0 0 40px var(--light-purple); }
            100% { text-shadow: 0 0 10px var(--accent-blue), 0 0 20px var(--light-purple), 0 0 30px var(--accent-blue); }
        }

        .main-chat-screen .greeting h1 {
            font-size: 42px;
            margin-bottom: 10px;
            background: linear-gradient(45deg, var(--accent-blue), var(--light-purple));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            text-shadow: 0 0 20px rgba(173, 216, 230, 0.9);
            animation: glowing 3s ease-in-out infinite alternate;
            transition: text-shadow 0.3s ease;
        }
        .main-chat-screen .greeting.hidden h1 {
            animation: none;
            text-shadow: none;
        }

        .main-chat-screen .greeting.hidden {
            opacity: 0;
            transform: translateY(-70px) translateX(-50%);
            pointer-events: none;
            visibility: hidden;
            height: 0;
            margin-bottom: 0;
            overflow: hidden; /* Ensure content is fully hidden */
        }

        .main-chat-screen .greeting p {
            font-size: 20px;
            color: var(--text-color-medium);
            max-width: 600px;
            margin: 0 auto;
            line-height: 1.5;
            transition: color 0.5s ease;
        }


        .chat-messages-container {
            flex-grow: 1;
            overflow-y: auto;
            display: flex;
            flex-direction: column;
            padding-right: 15px;
            scrollbar-width: thin;
            scrollbar-color: #4d0099 #100020;
            position: relative;
            z-index: 2;
            padding-top: 15px;
            padding-bottom: 15px;
        }
        @media (max-width: 768px) {
            .chat-messages-container {
                padding-right: 5px;
            }
        }
        .chat-messages-container::-webkit-scrollbar {
            width: 10px;
        }
        .chat-messages-container::-webkit-scrollbar-track {
            background: #100020;
        }
        .chat-messages-container::-webkit-scrollbar-thumb {
            background-color: #4d0099;
            border-radius: 10px;
            border: 3px solid #100020;
        }

        .chat-message {
            background-color: var(--chat-bg-ai);
            padding: 15px 22px;
            border-radius: 20px;
            margin-bottom: 12px;
            max-width: 75%;
            word-wrap: break-word;
            box-shadow: 0 4px 10px rgba(0,0,0,0.3);
            line-height: 1.6;
            border: 1px solid rgba(60, 0, 120, 0.3);
            transition: background-color 0.5s ease, border-color 0.5s ease;
        }
        .chat-message.user {
            align-self: flex-end;
            background: var(--chat-bg-user);
            color: var(--text-color-light);
            border: 1px solid rgba(138,43,226,0.5);
        }
        .chat-message.ai {
            align-self: flex-start;
            background-color: var(--chat-bg-ai);
            border: 1px solid rgba(40,0,80,0.5);
        }
        .chat-message strong {
            color: var(--accent-blue);
            font-weight: 600;
        }
        .chat-message.user strong {
            color: var(--accent-blue);
        }

        .chat-input-area {
            display: flex;
            flex-direction: column; /* Stack buttons and input */
            gap: 15px;
            padding: 15px;
            border-top: 1px solid var(--top-bar-bg);
            background-color: var(--dark-purple);
            flex-shrink: 0;
            box-shadow: 0 -5px 15px rgba(0, 0, 0, 0.4);
            border-radius: 20px 20px 0 0;
            align-items: center;
            transition: background-color 0.5s ease, border-top-color 0.5s ease;
            position: sticky;
            bottom: 0;
            left: 0;
            width: 100%;
            box-sizing: border-box;
            max-width: 900px;
            margin: 0 auto;
            z-index: 10;
        }
        @media (max-width: 768px) {
            .chat-input-area {
                position: fixed;
                bottom: 0;
                left: 0;
                width: 100%;
                border-radius: 0;
                max-width: 100%;
                padding-bottom: max(15px, env(safe-area-inset-bottom)); /* Adjust for safe areas on mobile */
            }
        }
        .chat-input-area .text-input-group {
            flex-grow: 1;
            display: flex;
            gap: 15px;
            width: 100%;
        }

        .chat-input-area textarea {
            flex-grow: 1;
            padding: 15px 20px;
            border-radius: 25px;
            border: 1px solid var(--input-border);
            background-color: var(--input-bg);
            color: var(--text-color-light);
            font-size: 16px;
            resize: none;
            min-height: 40px;
            max-height: 180px;
            overflow-y: auto;
            box-shadow: inset 0 2px 5px rgba(0, 0, 0, 0.2);
            transition: border-color 0.3s ease, background-color 0.3s ease, color 0.5s ease;
        }
        .chat-input-area textarea:focus {
            border-color: var(--light-purple);
            background-color: var(--input-focus-bg);
            outline: none;
            box-shadow: inset 0 2px 5px rgba(0, 0, 0, 0.3), 0 0 12px rgba(138,43,226,0.6);
        }
        .chat-input-area textarea::placeholder {
            color: var(--text-color-medium);
        }
        .chat-input-area button {
            background: var(--button-primary-bg);
            color: white;
            padding: 10px 22px;
            border-radius: 25px;
            border: none;
            cursor: pointer;
            font-size: 18px;
            font-weight: 600;
            transition: all 0.3s ease, background 0.5s ease;
            box-shadow: 0 5px 15px rgba(0,0,0,0.4);
            flex-shrink: 0;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .chat-input-area button:hover {
            background: var(--button-primary-hover-bg);
            transform: translateY(-2px);
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.6), 0 0 20px rgba(138,43,226,0.8);
        }
        .chat-input-area button:active {
            transform: translateY(0);
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
        }
        .chat-input-area button svg {
            width: 22px;
            height: 22px;
            fill: white;
        }

        .chat-input-area .post-send-buttons { /* New container for buttons after send */
            display: flex;
            gap: 10px;
            width: 100%;
            justify-content: flex-end; /* Align to right */
            position: relative;
            flex-shrink: 0;
        }
        @media (max-width: 768px) {
            .chat-input-area .post-send-buttons {
                justify-content: center; /* Center buttons on mobile */
            }
        }

        /* Compact Media Chat button */
        .chat-input-area #media-chat-toggle {
            background: var(--button-secondary-bg);
            color: var(--text-color-medium);
            width: 50px; /* Slightly larger fixed width for compact button */
            height: 50px; /* Slightly larger fixed height for compact button */
            padding: 0;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 2px 8px rgba(0,0,0,0.2);
            position: relative;
            transition: all 0.3s ease, background-color 0.5s ease, color 0.5s ease;
        }
        .chat-input-area #media-chat-toggle svg {
            width: 26px; /* Adjust icon size */
            height: 26px; /* Adjust icon size */
            fill: currentColor;
            margin-right: 0;
        }
        .chat-input-area #media-chat-toggle span {
            display: none;
        }
        .chat-input-area #media-chat-toggle::after {
            content: '';
        }
        .chat-input-area #media-chat-toggle:hover {
            background: var(--button-secondary-hover-bg);
            color: var(--text-color-light);
            transform: translateY(-1px);
            box-shadow: 0 4px 10px rgba(0,0,0,0.3);
        }

        /* Dropdown styles for combined button */
        .dropdown {
            position: relative;
            display: inline-block;
            height: 50px; /* Match height of compact button */
            display: flex;
            align-items: center;
        }

        .dropdown-content {
            display: none;
            position: absolute;
            bottom: 100%;
            left: 50%;
            transform: translateX(-50%);
            background-color: var(--medium-purple);
            min-width: 180px;
            box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.5);
            border-radius: 10px;
            padding: 10px 0;
            z-index: 10;
            margin-bottom: 10px;
            border: 1px solid rgba(138,43,226,0.3);
            transition: background-color 0.5s ease, border-color 0.5s ease;
        }

        .dropdown-content button {
            color: var(--text-color-light);
            padding: 12px 16px;
            text-decoration: none;
            display: flex;
            align-items: center;
            gap: 8px;
            width: 100%;
            text-align: left;
            border: none;
            background: none;
            cursor: pointer;
            border-radius: 0;
            font-size: 15px;
            transition: background-color 0.5s ease, color 0.5s ease;
            box-shadow: none;
            transform: none;
        }

        .dropdown-content button:hover {
            background-color: var(--button-secondary-hover-bg);
            transform: none;
            box-shadow: none;
        }
        .dropdown-content button svg {
            width: 18px;
            height: 18px;
            fill: currentColor;
        }

        .dropdown:hover .dropdown-content,
        .dropdown.active .dropdown-content {
            display: block;
        }


        /* Галерея изображений */
        .image-gallery {
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
            gap: 30px;
            margin-top: 50px;
            width: 100%;
            max-width: 800px;
            padding-bottom: 30px;
            flex-grow: 1;
        }

        .generate-image-button {
            background: var(--button-primary-bg);
            color: white;
            padding: 20px 40px;
            border-radius: 30px;
            border: none;
            cursor: pointer;
            font-size: 20px;
            font-weight: 700;
            transition: all 0.3s ease, background 0.5s ease;
            box-shadow: 0 8px 25px rgba(0,0,0,0.5);
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .generate-image-button:hover {
            background: var(--button-primary-hover-bg);
            transform: translateY(-5px);
            box-shadow: 0 12px 30px rgba(0, 0, 0, 0.7), 0 0 25px rgba(138,43,226,0.9);
        }
        .generate-image-button:active {
            transform: translateY(0);
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.3);
        }
        .generate-image-button svg {
            width: 30px;
            height: 30px;
            fill: white;
        }

        /* Projects Section */
        .create-project-button {
            background: linear-gradient(90deg, #00994d, #00cd6a);
            color: var(--text-color-light);
            padding: 15px 30px;
            border-radius: 25px;
            border: none;
            cursor: pointer;
            font-size: 18px;
            font-weight: 600;
            display: flex;
            align-items: center;
            gap: 10px;
            transition: all 0.3s ease, color 0.5s ease;
            box-shadow: 0 5px 15px rgba(0,0,0,0.4);
            margin-top: 30px;
        }
        .create-project-button:hover {
            background: linear-gradient(90deg, #00cd6a, #00ff8a);
            transform: translateY(-2px);
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.6), 0 0 10px rgba(0, 205, 106, 0.6);
        }
        .create-project-button:active {
            transform: translateY(0);
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
        }
        .create-project-button svg {
            width: 24px;
            height: 24px;
            fill: currentColor;
        }


        /* Настройки (модальное окно) */
        .settings-modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.8);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 1000;
            opacity: 0;
            visibility: hidden;
            transition: opacity 0.3s ease, visibility 0.3s ease;
            backdrop-filter: blur(5px);
        }

        .settings-modal.active {
            opacity: 1;
            visibility: visible;
        }

        .settings-content {
            background: var(--settings-modal-bg);
            padding: 35px;
            border-radius: 20px;
            box-shadow: 0 0 30px rgba(0, 0, 0, 0.7);
            width: 90%;
            max-width: 700px;
            max-height: 90vh;
            overflow-y: auto;
            position: relative;
            border: 1px solid var(--medium-purple);
            transition: background 0.5s ease, border-color 0.5s ease;
        }
        .settings-content h2 {
            font-size: 36px;
            text-align: center;
            margin-bottom: 35px;
            background: linear-gradient(45deg, var(--accent-blue), var(--light-purple));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            text-shadow: 0 0 15px rgba(173, 216, 230, 0.8);
            transition: text-shadow 0.5s ease;
        }
        .settings-content .close-button {
            position: absolute;
            top: 18px;
            right: 18px;
            background: none;
            border: none;
            color: var(--text-color-medium);
            font-size: 35px;
            cursor: pointer;
            line-height: 1;
            transition: color 0.2s ease, transform 0.2s ease;
        }
        .settings-content .close-button:hover {
            color: var(--text-color-light);
            transform: rotate(90deg);
        }
        .settings-group {
            margin-bottom: 30px;
            padding-bottom: 20px;
            border-bottom: 1px solid var(--settings-border-line);
            transition: border-bottom-color 0.5s ease;
        }
        .settings-group:last-child {
            border-bottom: none;
            margin-bottom: 0;
            padding-bottom: 0;
        }
        .settings-group h3 {
            font-size: 22px;
            color: var(--light-purple);
            margin-bottom: 20px;
            padding-bottom: 5px;
            border-bottom: 1px dashed rgba(138,43,226,0.3);
            filter: drop-shadow(0 0 5px rgba(138,43,226,0.5));
            transition: color 0.5s ease, filter 0.5s ease;
        }
        .setting-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
            background-color: var(--settings-item-bg);
            padding: 15px 20px;
            border-radius: 10px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.2);
            transition: background-color 0.2s ease, border-color 0.5s ease;
            border: 1px solid rgba(60, 0, 120, 0.3);
        }
        .setting-item:hover {
            background-color: var(--settings-item-hover-bg);
        }
        .setting-item label {
            font-size: 17px;
            color: var(--text-color-light);
            flex-grow: 1;
            transition: color 0.5s ease;
        }
        .setting-item select, .setting-item input[type="text"], .setting-item input[type="email"] {
            background-color: var(--settings-input-bg);
            color: var(--text-color-light);
            border: 1px solid var(--input-border);
            border-radius: 8px;
            padding: 10px 12px;
            font-size: 16px;
            min-width: 180px;
            appearance: none;
            background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="%23bbb"><path d="M7 10l5 5 5-5z"/></svg>');
            background-repeat: no-repeat;
            background-position: right 10px center;
            background-size: 20px;
            cursor: pointer;
            transition: background-color 0.5s ease, color 0.5s ease, border-color 0.5s ease;
        }
        .setting-item input[type="checkbox"] {
            width: 24px;
            height: 24px;
            accent-color: var(--light-purple);
            cursor: pointer;
        }
        .setting-item button {
            background: var(--button-primary-bg);
            color: white;
            padding: 10px 18px;
            border-radius: 10px;
            border: none;
            cursor: pointer;
            font-size: 16px;
            font-weight: 500;
            transition: all 0.3s ease, background 0.5s ease;
            box-shadow: 0 3px 10px rgba(0,0,0,0.3);
        }
        .setting-item button:hover {
            background: var(--button-primary-hover-bg);
            transform: translateY(-1px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.4), 0 0 8px rgba(138,43,226,0.5);
        }
        .setting-item button:active {
            transform: translateY(0);
            box-shadow: 0 2px 8px rgba(0,0,0,0.2);
        }
        .setting-item button.danger {
            background: linear-gradient(45deg, #cc0000, #ff4d4d);
        }
        .setting-item button.danger:hover {
            background: linear-gradient(45deg, #ff3333, #ff6666);
            box-shadow: 0 5px 15px rgba(0,0,0,0.4), 0 0 8px rgba(255,77,77,0.5);
        }

        /* Адаптивность */
        @media (max-width: 768px) {
            .main-content {
                padding-top: 0;
            }
            .top-bar {
                background-color: var(--dark-purple);
                position: sticky;
                top: 0;
                width: 100%;
                z-index: 100;
                box-shadow: 0 2px 10px rgba(0, 0, 0, 0.4);
                border-bottom: none;
            }

            .content-section {
                padding: 20px 15px;
                height: calc(100% - var(--top-bar-height) - var(--chat-input-area-height)); /* Adjusted height for sections to account for fixed input area */
                top: var(--top-bar-height);
            }
            /* Specific adjustment for chat section if needed, but general rule above should handle it */
            /* .content-section#main-chat {
                height: calc(100% - var(--top-bar-height) - var(--chat-input-area-height));
            } */

            .content-section h2 {
                font-size: 28px;
            }
            .content-section p, .content-section ul li {
                font-size: 15px;
            }
            .image-gallery {
                margin-top: 30px;
                gap: 20px;
            }
            .generate-image-button {
                padding: 15px 30px;
                font-size: 18px;
            }
            .generate-image-button svg {
                width: 24px;
                height: 24px;
            }

            .settings-content {
                padding: 25px;
            }
            .settings-content h2 {
                font-size: 28px;
            }
            .settings-group h3 {
                font-size: 18px;
            }
            .setting-item label, .setting-item select, .setting-item input, .setting-item button {
                font-size: 15px;
            }
             .setting-item select, .setting-item input[type="text"], .setting-item input[type="email"] {
                 min-width: 120px;
             }
        }
    </style>
</head>
<body>

    <div class="app-wrapper">

        <aside class="sidebar" id="sidebar">
            <div class="sidebar-header">
                <div class="logo">NEURA</div>
                <button class="new-chat-button" id="new-chat-button">
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M19 13h-6v6h-2v-6H5v-2h6V5h2v6h6v2z"/></svg>
                    <span>Новый чат</span>
                </button>
            </div>

            <nav class="sidebar-nav">
                <ul>
                    <li>
                        <a href="#" data-section="main-chat" class="active" data-title="Чат">
                            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M20 2H4c-1.1 0-1.99.9-1.99 2L2 22l4-4h14c1.1 0 2-.9 2-2V4c0-1.1-.9-2-2-2zm-2 12H6v-2h12v2zm0-3H6V9h12v2zm0-3H6V6h12v2z"/></svg>
                            <span>Чат</span>
                        </a>
                    </li>
                    <li>
                        <a href="#" data-section="images-section" data-title="Изображения">
                            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M21 19V5c0-1.1-.9-2-2-2H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2zM8.5 13.5l2.5 3.01L14.5 12l4.5 6H5l3.5-4.5z"/></svg>
                            <span>Изображения</span>
                        </a>
                    </li>
                    <li>
                        <a href="#" data-section="knowledge-section" data-title="База знаний">
                            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2zM9 17H7v-7h2v7zm4 0h-2V7h2v10zm4 0h-2v-4h2v4z"/></svg>
                            <span>Знания</span>
                        </a>
                    </li>
                     <li>
                        <a href="#" data-section="projects-section" data-title="Проекты">
                            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M14 2H6c-1.1 0-1.99.9-1.99 2L4 20c0 1.1.89 2 1.99 2H18c1.1 0 2-.9 2-2V8l-6-6zm2 14H8v-2h8v2zm0-4H8v-2h8v2zm-3-5V3.5L17.5 9H13z"/></svg>
                            <span>Проекты</span>
                        </a>
                    </li>
                </ul>

                <p class="chat-history-title">Сегодня</p>
                <div class="chat-history" id="chat-history-today">
                    <ul>
                        </ul>
                </div>
                <p class="chat-history-title">Вчера</p>
                <div class="chat-history" id="chat-history-yesterday">
                    <ul>
                        </ul>
                </div>

            </nav>

            <div class="sidebar-bottom">
                <button class="sidebar-bottom-button" id="settings-button">
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M12 8c1.1 0 2-.9 2-2s-.9-2-2-2-2 .9-2 2 .9 2 2 2zm0 2c-1.1 0-2 .9-2 2s.9 2 2 2 2-.9 2-2-.9-2-2-2zm0 6c-1.1 0-2 .9-2 2s.9 2 2 2 2-.9 2-2-.9-2-2-2z"/></svg>
                    <span>Настройки</span>
                </button>
                 <button class="sidebar-bottom-button" id="logout-button">
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M17 7l-1.41 1.41L18.17 11H8v2h10.17l-2.58 2.58L17 17l5-5zM4 5h7V3H4c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h7v-2H4V5z"/></svg>
                    <span>Выйти</span>
                </button>
            </div>
        </aside>

        <main class="main-content" id="main-content-area">
            <div class="top-bar">
                <button class="menu-toggle" id="menu-toggle">
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M3 18h18v-2H3v2zm0-5h18v-2H3v2zm0-7v2h18V6H3z"/></svg>
                </button>
                <span class="title" id="current-title">Чат</span>
                <div></div>
            </div>

            <section class="content-section active" id="main-chat" data-title="Чат">
                <div class="main-chat-screen">
                    <div class="greeting" id="chat-greeting">
                        <h1>Привет, я — Нейроника</h1>
                        <p>Я — ваш квантовый помощник. Чем могу помочь сегодня?</p>
                    </div>

                    <div class="chat-messages-container" id="chat-messages-container">
                    </div>

                </div>
                <div class="chat-input-area" id="chat-input-area">
                    <div class="text-input-group">
                        <textarea id="chat-input" placeholder="Введите ваше сообщение..."></textarea>
                        <button id="send-button">
                            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M2.01 21L23 12 2.01 3 2 10l15 2-15 2z" fill="white"/></svg>
                        </button>
                    </div>
                    <div class="post-send-buttons">
                        <div class="dropdown" id="media-chat-dropdown">
                            <button id="media-chat-toggle">
                                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor"><path d="M12 14c1.66 0 2.99-1.34 2.99-3L15 5c0-1.66-1.34-3-3-3S9 3.34 9 5v6c0 1.66 1.34 3 3 3zm5.2-3c0 3.2-2.8 5.4-5.2 5.4s-5.2-2.2-5.2-5.4H5c0 3.41 2.72 6.23 6 6.72V21h2v-2.28c3.28-.49 6-3.31 6-6.72h-1.8z"/></svg>
                            </button>
                            <div class="dropdown-content">
                                <button id="voice-chat-button">
                                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor"><path d="M12 14c1.66 0 2.99-1.34 2.99-3L15 5c0-1.66-1.34-3-3-3S9 3.34 9 5v6c0 1.66 1.34 3 3 3zm5.2-3c0 3.2-2.8 5.4-5.2 5.4s-5.2-2.2-5.2-5.4H5c0 3.41 2.72 6.23 6 6.72V21h2v-2.28c3.28-.49 6-3.31 6-6.72h-1.8z"/></svg>
                                    Голосовой чат
                                </button>
                                <button id="video-chat-button">
                                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor"><path d="M17 10.5V7c0-.55-.45-1-1-1H4c-.55 0-1 .45-1 1v10c0 .55.45 1 1 1h12c.55 0 1-.45 1-1v-3.5l4 4v-11l-4 4z"/></svg>
                                    Видеочат
                                </button>
                            </div>
                        </div>
                    </div>
                </div>
            </section>

            <section class="content-section" id="images-section" data-title="Изображения">
                <h2>Генерация изображений</h2>
                <p>Позвольте Нейронике воплотить ваши идеи в визуальные шедевры. Просто нажмите кнопку, чтобы начать!</p>
                <div class="image-gallery">
                    <button class="generate-image-button">
                        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M21 19V5c0-1.1-.9-2-2-2H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2zM8.5 13.5l2.5 3.01L14.5 12l4.5 6H5l3.5-4.5z"/></svg>
                        Сгенерировать изображение
                    </button>
                    </div>
            </section>

            <section class="content-section" id="knowledge-section" data-title="База знаний">
                <h2>База знаний Нейроники</h2>
                <p>Здесь собраны ключевые концепции и ответы на часто задаваемые вопросы.</p>
                <ul>
                    <li>
                        <span>•</span> Что такое Нейроника?<br>
                        Нейроника — это передовой квантовый искусственный интеллект, разработанный для решения сложных задач и творческого взаимодействия.
                    </li>
                    <li>
                        <span>•</span> Как Neura AI использует квантовые принципы?<br>
                        Наша система использует принципы суперпозиции и запутанности для более эффективной обработки данных и выполнения вычислений, что позволяет достигать беспрецедентной скорости и точности.
                    </li>
                    <li>
                        <span>•</span> Какие задачи может решить Нейроника?<br>
                        От написания текстов и генерации изображений до анализа данных и создания креативных идей, оптимизации процессов и научных исследований.
                    </li>


                     <li>
                        <span>•</span> Поддерживается ли Нейроника на разных платформах?<br>
                        Да, Нейроника оптимизирована для работы на веб-платформах, а также имеет нативные приложения для мобильных устройств.
                    </li>
                </ul>
                <p style="margin-top: 20px; text-align: center;">Если у вас есть конкретный вопрос, спросите его в чате!</p>
            </section>

            <section class="content-section" id="projects-section" data-title="Проекты">
                <h2>Ваши Проекты</h2>
                <p>Управляйте своими текущими проектами и создавайте новые, используя мощь Нейроники.</p>
                <button class="create-project-button">
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M19 13h-6v6h-2v-6H5v-2h6V5h2v6h6v2z"/></svg>
                    Создать новый проект
                </button>
                <p style="margin-top: 20px; text-align: center;">Нейроника поможет вам в реализации любых ваших идей!</p>
            </section>

        </main>
    </div>

    <div class="settings-modal" id="settings-modal">
        <div class="settings-content">
            <button class="close-button" id="close-settings">&times;</button>
            <h2>Настройки</h2>

            <div class="settings-group">
                <h3>Общие</h3>
                <div class="setting-item">
                    <label for="theme-select">Тема интерфейса:</label>
                    <select id="theme-select">
                        <option value="dark">Темная</option>
                        <option value="light">Светлая</option>
                    </select>
                </div>
                <div class="setting-item">
                    <label for="language-select">Язык:</label>
                    <select id="language-select">
                        <option value="ru">Русский (RU)</option>
                        <option value="en">English (EN)</option>
                    </select>
                </div>
                 <div class="setting-item">
                    <label for="notifications-toggle">Уведомления:</label>
                    <input type="checkbox" id="notifications-toggle" checked>
                </div>
            </div>

            <div class="settings-group">
                <h3>Аккаунт</h3>
                <div class="setting-item">
                    <label for="email-input">Email:</label>
                    <input type="email" id="email-input" value="user@example.com" readonly>
                </div>
                <div class="setting-item">
                    <label>Подписка:</label>
                    <span>Premium (до 25.07.2026)</span>
                </div>
                <div class="setting-item">
                    <button>Управление подпиской</button>
                </div>
                 <div class="setting-item">
                    <button class="danger">Удалить аккаунт</button>
                </div>
            </div>

            <div class="settings-group">
                <h3>Конфиденциальность</h3>
                <div class="setting-item">
                    <label for="data-sharing-toggle">Разрешить сбор анонимных данных:</label>
                    <input type="checkbox" id="data-sharing-toggle">
                </div>
                <div class="setting-item">
                    <label>История чатов:</label>
                    <button id="clear-chat-history-button">Очистить историю</button>
                </div>
            </div>

        </div>
    </div>


    <script>
        document.addEventListener('DOMContentLoaded', () => {
            // --- Элементы DOM ---
            const sidebarNavLinks = document.querySelectorAll('.sidebar-nav a');
            const contentSections = document.querySelectorAll('.content-section');
            const mainChatSection = document.getElementById('main-chat');
            const sidebar = document.getElementById('sidebar');
            const menuToggle = document.getElementById('menu-toggle');
            const currentTitle = document.getElementById('current-title');
            const newChatButton = document.getElementById('new-chat-button');
            const mainContentArea = document.getElementById('main-content-area');

            const settingsButton = document.getElementById('settings-button');
            const settingsModal = document.getElementById('settings-modal');
            const closeSettingsButton = document.getElementById('close-settings');
            const clearChatHistoryButton = document.getElementById('clear-chat-history-button');
            const themeSelect = document.getElementById('theme-select');

            const chatInput = document.getElementById('chat-input');
            const sendButton = document.getElementById('send-button');
            const chatMessagesContainer = document.getElementById('chat-messages-container');
            const chatGreeting = document.getElementById('chat-greeting');
            const chatInputArea = document.getElementById('chat-input-area');

            const chatHistoryToday = document.getElementById('chat-history-today').querySelector('ul');
            const chatHistoryYesterday = document.getElementById('chat-history-yesterday').querySelector('ul');

            const mediaChatToggle = document.getElementById('media-chat-toggle');
            const mediaChatDropdown = document.getElementById('media-chat-dropdown');
            const voiceChatButton = document.getElementById('voice-chat-button');
            const videoChatButton = document.getElementById('video-chat-button');

            let touchStartX = 0;
            let touchEndX = 0;

            // --- Управление темами ---
            function applyTheme(theme) {
                document.body.classList.remove('dark-theme', 'light-theme');
                if (theme === 'light') {
                    document.body.classList.add('light-theme');
                } else {
                    document.body.classList.add('dark-theme'); // По умолчанию темная тема
                }
                localStorage.setItem('theme', theme); // Сохраняем выбор темы
                themeSelect.value = theme; // Обновляем выпадающий список
            }

            // Загрузка темы при загрузке страницы
            const savedTheme = localStorage.getItem('theme') || 'dark'; // По умолчанию 'dark'
            applyTheme(savedTheme);

            // Обработчик изменения темы
            themeSelect.addEventListener('change', (event) => {
                applyTheme(event.target.value);
            });

            // --- Управление секциями контента ---
            function showSection(targetSectionId) {
                contentSections.forEach(section => {
                    section.classList.remove('active');
                });
                const targetSection = document.getElementById(targetSectionId);
                if (targetSection) {
                    targetSection.classList.add('active');
                    currentTitle.textContent = targetSection.getAttribute('data-title') || targetSection.querySelector('h2')?.textContent || 'Чат';
                }
                // Боковая панель должна закрываться при выборе секции
                sidebar.classList.remove('active');
                updateGreetingVisibility(); // Обновляем видимость приветствия
            }

            // --- Управление историей чатов ---
            function saveChatHistory() {
                const todayChats = Array.from(chatHistoryToday.children).map(li => ({
                    id: li.dataset.id,
                    name: li.querySelector('.chat-history-item-text').textContent,
                }));
                const yesterdayChats = Array.from(chatHistoryYesterday.children).map(li => ({
                    id: li.dataset.id,
                    name: li.querySelector('.chat-history-item-text').textContent,
                }));
                localStorage.setItem('todayChatHistory', JSON.stringify(todayChats));
                localStorage.setItem('yesterdayChatHistory', JSON.stringify(yesterdayChats));
            }

            function loadChatHistory() {
                const todayChats = JSON.parse(localStorage.getItem('todayChatHistory')) || [];
                const yesterdayChats = JSON.parse(localStorage.getItem('yesterdayChatHistory')) || [];

                chatHistoryToday.innerHTML = '';
                chatHistoryYesterday.innerHTML = '';

                todayChats.forEach(chat => {
                    addNewChatHistoryEntry(chat.name, chat.id, 'today', false); // false = не сохранять повторно
                });
                yesterdayChats.forEach(chat => {
                    addNewChatHistoryEntry(chat.name, chat.id, 'yesterday', false);
                });
            }

            // Функция для добавления новой записи в историю чатов
            function addNewChatHistoryEntry(chatName = "Новый чат", chatId = null, section = 'today', save = true) {
                if (!chatId) {
                    chatId = `chat-${Date.now()}`; // Генерируем уникальный ID
                }

                const listItem = document.createElement('li');
                listItem.setAttribute('data-id', chatId);
                listItem.innerHTML = `
                    <a href="#" data-section="main-chat">
                        <span class="chat-history-item-text">${chatName}</span>
                        <button class="chat-history-item-delete">&times;</button>
                    </a>
                `;

                const targetHistory = section === 'today' ? chatHistoryToday : chatHistoryYesterday;
                targetHistory.prepend(listItem); // Добавляем в начало списка

                // Ограничиваем количество элементов в истории
                const maxChatHistoryItems = 10; // Можно настроить
                if (targetHistory.children.length > maxChatHistoryItems) {
                    const oldestChatLi = targetHistory.lastElementChild;
                    const oldestChatId = oldestChatLi.dataset.id;
                    oldestChatLi.remove();
                    localStorage.removeItem(`chatMessages_${oldestChatId}`); // Удаляем сообщения для старого чата
                }

                attachChatHistoryListeners(listItem);

                if (save) {
                    localStorage.setItem(`chatMessages_${chatId}`, JSON.stringify([])); // Инициализируем пустыми сообщениями
                    saveChatHistory();
                }

                return listItem;
            }

            // Функция для загрузки сообщений для текущего активного чата
            function loadChatMessages(chatId = null) {
                let currentChatId = chatId;

                if (!currentChatId) {
                    currentChatId = localStorage.getItem('activeChatId');
                }

                chatMessagesContainer.innerHTML = ''; // Очищаем текущие сообщения

                if (currentChatId) {
                    const messages = JSON.parse(localStorage.getItem(`chatMessages_${currentChatId}`)) || [];
                    messages.forEach(msg => {
                        const msgDiv = document.createElement('div');
                        msgDiv.classList.add('chat-message', msg.sender);
                        msgDiv.innerHTML = `<strong>${msg.sender === 'user' ? 'Вы' : 'Нейроника'}:</strong> ${msg.text}`;
                        chatMessagesContainer.appendChild(msgDiv);
                    });
                    chatMessagesContainer.scrollTop = chatMessagesContainer.scrollHeight;
                }
                updateGreetingVisibility(); // Обновляем видимость приветствия после загрузки
            }

            // Функция для прикрепления слушателей событий к элементам истории чатов
            function attachChatHistoryListeners(item) {
                const deleteButton = item.querySelector('.chat-history-item-delete');
                if (deleteButton) {
                    deleteButton.addEventListener('click', (event) => {
                        event.preventDefault();
                        event.stopPropagation(); // Предотвращаем клик по ссылке
                        const chatIdToDelete = item.dataset.id;
                        const wasActive = (localStorage.getItem('activeChatId') === chatIdToDelete);

                        item.remove();
                        localStorage.removeItem(`chatMessages_${chatIdToDelete}`); // Удаляем сообщения
                        saveChatHistory(); // Сохраняем обновленную историю

                        if (wasActive) {
                            // Если удален активный чат, переключаемся на последний или создаем новый
                            localStorage.removeItem('activeChatId');
                            chatMessagesContainer.innerHTML = ''; // Очищаем контейнер сообщений
                            const mostRecentChat = chatHistoryToday.querySelector('li') || chatHistoryYesterday.querySelector('li');
                            if (mostRecentChat) {
                                localStorage.setItem('activeChatId', mostRecentChat.dataset.id);
                                loadChatMessages(mostRecentChat.dataset.id);
                            } else {
                                // Если чатов нет, показываем приветствие
                                updateGreetingVisibility();
                            }
                            // Убеждаемся, что "Чат" остается активным в сайдбаре
                            sidebarNavLinks.forEach(l => l.classList.remove('active'));
                            document.querySelector('.sidebar-nav a[data-section="main-chat"]').classList.add('active');
                        }
                        updateGreetingVisibility(); // Переоцениваем видимость приветствия после удаления
                    });
                }

                const chatLink = item.querySelector('a');
                if (chatLink) {
                    chatLink.addEventListener('click', (event) => {
                        event.preventDefault();
                        // Снимаем активность со всех ссылок, затем активируем текущую
                        sidebarNavLinks.forEach(l => l.classList.remove('active'));
                        document.querySelector('.sidebar-nav a[data-section="main-chat"]').classList.add('active'); // Активируем ссылку "Чат"
                        showSection('main-chat'); // Показываем секцию чата

                        const clickedChatId = item.dataset.id;
                        localStorage.setItem('activeChatId', clickedChatId); // Устанавливаем активный чат
                        loadChatMessages(clickedChatId); // Загружаем сообщения
                    });
                }
            }

            // Загружаем историю чатов и сообщения при загрузке страницы
            loadChatHistory();
            const initialActiveChatId = localStorage.getItem('activeChatId');
            if (initialActiveChatId) {
                // Если есть активный чат, загружаем его сообщения и активируем соответствующую ссылку
                const activeLink = document.querySelector(`.sidebar-nav a[data-section="main-chat"]`); // Предполагаем, что ссылка "Чат" всегда одна
                if (activeLink) {
                    sidebarNavLinks.forEach(l => l.classList.remove('active'));
                    activeLink.classList.add('active');
                }
                loadChatMessages(initialActiveChatId);
            } else {
                // Если активного чата нет, убедимся, что контейнер сообщений пуст
                chatMessagesContainer.innerHTML = '';
            }
            updateGreetingVisibility(); // Инициализация видимости приветствия

            // Прикрепляем слушателей к уже существующим элементам истории чатов (после загрузки)
            document.querySelectorAll('.chat-history ul li').forEach(attachChatHistoryListeners);


            // --- Обработчики событий ---

            // Переключение секций через навигацию сайдбара
            sidebarNavLinks.forEach(link => {
                link.addEventListener('click', (event) => {
                    event.preventDefault();
                    sidebarNavLinks.forEach(l => l.classList.remove('active'));
                    link.classList.add('active');
                    const targetSectionId = link.dataset.section;
                    showSection(targetSectionId);

                    if (targetSectionId === 'main-chat') {
                        loadChatMessages(); // Перезагружаем сообщения для активного чата
                    }
                });
            });

            // Кнопка "Новый чат"
            newChatButton.addEventListener('click', () => {
                sidebarNavLinks.forEach(l => l.classList.remove('active'));
                document.querySelector('.sidebar-nav a[data-section="main-chat"]').classList.add('active');
                showSection('main-chat');
                chatMessagesContainer.innerHTML = '';
                chatInput.value = '';
                chatInput.style.height = 'auto'; // Сбрасываем высоту
                chatInput.focus();
                const newChatLi = addNewChatHistoryEntry("Новый чат"); // Создаем новую запись в истории
                localStorage.setItem('activeChatId', newChatLi.dataset.id); // Устанавливаем ее как активную
                updateGreetingVisibility(); // Показываем приветствие
                updateDynamicHeights(); // Обновляем высоту области ввода
            });

            // Кнопка "Настройки"
            settingsButton.addEventListener('click', () => {
                settingsModal.classList.add('active');
                sidebar.classList.remove('active'); // Закрываем сайдбар при открытии настроек
            });

            // Кнопка закрытия настроек
            closeSettingsButton.addEventListener('click', () => {
                settingsModal.classList.remove('active');
            });

            // Закрытие настроек по клику вне модального окна
            settingsModal.addEventListener('click', (event) => {
                if (event.target === settingsModal) {
                    settingsModal.classList.remove('active');
                }
            });

            // Кнопка "Очистить историю чатов"
            clearChatHistoryButton.addEventListener('click', () => {
                if (confirm('Вы уверены, что хотите полностью очистить всю историю чатов? Это действие необратимо.')) {
                    chatHistoryToday.innerHTML = '';
                    chatHistoryYesterday.innerHTML = '';
                    localStorage.removeItem('todayChatHistory');
                    localStorage.removeItem('yesterdayChatHistory');
                    // Удаляем все сообщения чатов
                    for (let i = localStorage.length - 1; i >= 0; i--) { // Итерируем в обратном порядке, чтобы избежать проблем с изменением длины
                        const key = localStorage.key(i);
                        if (key && key.startsWith('chatMessages_')) {
                            localStorage.removeItem(key);
                        }
                    }
                    localStorage.removeItem('activeChatId'); // Сбрасываем активный чат
                    chatMessagesContainer.innerHTML = ''; // Очищаем сообщения в текущем представлении
                    alert('История чатов очищена!');
                    settingsModal.classList.remove('active');
                    updateGreetingVisibility(); // Показываем приветствие
                }
            });

            // Динамическое обновление CSS переменных высоты
            const topBar = document.querySelector('.top-bar');
            function updateDynamicHeights() {
                if (topBar) {
                    const topBarHeight = topBar.offsetHeight;
                    document.documentElement.style.setProperty('--top-bar-height', `${topBarHeight}px`);
                }
                if (chatInputArea) {
                    const chatInputAreaHeight = chatInputArea.offsetHeight;
                    document.documentElement.style.setProperty('--chat-input-area-height', `${chatInputAreaHeight}px`);
                }
                // Также можно обновить высоту main-chat-screen, если она зависит от этих переменных
                if (mainChatSection.classList.contains('active')) {
                    // Force re-calculation for main-chat-screen height if needed
                }
            }

            // Используем ResizeObserver для более надежного обновления высот
            const topBarResizeObserver = new ResizeObserver(updateDynamicHeights);
            if (topBar) topBarResizeObserver.observe(topBar);
            const chatInputAreaResizeObserver = new ResizeObserver(updateDynamicHeights);
            if (chatInputArea) chatInputAreaResizeObserver.observe(chatInputArea);

            updateDynamicHeights(); // Инициализация

            // Автоматическая подстройка высоты textarea
            chatInput.addEventListener('input', () => {
                chatInput.style.height = 'auto';
                chatInput.style.height = (chatInput.scrollHeight) + 'px';
                updateDynamicHeights(); // Обновляем высоту области ввода
                chatMessagesContainer.scrollTop = chatMessagesContainer.scrollHeight; // Прокручиваем вниз
            });

            // Переключение боковой панели
            menuToggle.addEventListener('click', () => {
                sidebar.classList.toggle('active');
            });

            // Обработка свайпов для боковой панели
            mainContentArea.addEventListener('touchstart', (e) => {
                touchStartX = e.changedTouches[0].screenX;
            }, { passive: true });

            mainContentArea.addEventListener('touchend', (e) => {
                touchEndX = e.changedTouches[0].screenX;
                handleGesture();
            }, { passive: true });

            function handleGesture() {
                const swipeThreshold = 75; // Пикселей для срабатывания свайпа
                const currentSidebarActive = sidebar.classList.contains('active');

                if (touchEndX < touchStartX - swipeThreshold) { // Свайп влево
                    if (currentSidebarActive) {
                        sidebar.classList.remove('active');
                    }
                } else if (touchEndX > touchStartX + swipeThreshold) { // Свайп вправо
                    if (!currentSidebarActive) {
                        sidebar.classList.add('active');
                    }
                }
            }


            // --- Логика чата: отправка сообщений, скрытие приветствия ---

            sendButton.addEventListener('click', sendMessage);
            chatInput.addEventListener('keypress', (e) => {
                if (e.key === 'Enter' && !e.shiftKey) {
                    e.preventDefault();
                    sendMessage();
                }
            });

            function sendMessage() {
                const messageText = chatInput.value.trim();
                if (messageText) {
                    let activeChatId = localStorage.getItem('activeChatId');

                    // Если активного чата нет, создаем новый
                    if (!activeChatId) {
                        const newChatLi = addNewChatHistoryEntry(messageText.length > 25 ? messageText.substring(0, 25) + '...' : messageText);
                        activeChatId = newChatLi.dataset.id;
                        localStorage.setItem('activeChatId', activeChatId);
                    } else {
                        // Обновляем название существующего "Нового чата" первым сообщением
                        const currentChatLink = document.querySelector(`#chat-history-today li[data-id="${activeChatId}"] a, #chat-history-yesterday li[data-id="${activeChatId}"] a`);
                        if (currentChatLink) {
                            const chatTextSpan = currentChatLink.querySelector('.chat-history-item-text');
                            if (chatTextSpan && chatTextSpan.textContent === "Новый чат") {
                                const snippet = messageText.length > 25 ? messageText.substring(0, 25) + '...' : messageText;
                                chatTextSpan.textContent = snippet;
                                saveChatHistory(); // Сохраняем обновленное имя
                            }
                        }
                    }

                    // Добавляем сообщение пользователя
                    const userMessageDiv = document.createElement('div');
                    userMessageDiv.classList.add('chat-message', 'user');
                    userMessageDiv.innerHTML = `<strong>Вы:</strong> ${messageText}`;
                    chatMessagesContainer.appendChild(userMessageDiv);

                    // Сохраняем сообщение в localStorage
                    let currentChatMessages = JSON.parse(localStorage.getItem(`chatMessages_${activeChatId}`)) || [];
                    currentChatMessages.push({ sender: 'user', text: messageText });
                    localStorage.setItem(`chatMessages_${activeChatId}`, JSON.stringify(currentChatMessages));

                    chatInput.value = '';
                    chatInput.style.height = 'auto';
                    updateDynamicHeights(); // Обновляем высоту области ввода
                    chatMessagesContainer.scrollTop = chatMessagesContainer.scrollHeight;

                    updateGreetingVisibility(); // Скрываем приветствие

                    // Имитация ответа ИИ
                    setTimeout(() => {
                        const aiMessageText = `Понял ваш запрос: "${messageText}". Думаю над ответом...`;
                        const aiMessageDiv = document.createElement('div');
                        aiMessageDiv.classList.add('chat-message', 'ai');
                        aiMessageDiv.innerHTML = `<strong>Нейроника:</strong> ${aiMessageText}`;
                        chatMessagesContainer.appendChild(aiMessageDiv);

                        currentChatMessages = JSON.parse(localStorage.getItem(`chatMessages_${activeChatId}`)) || [];
                        currentChatMessages.push({ sender: 'ai', text: aiMessageText });
                        localStorage.setItem(`chatMessages_${activeChatId}`, JSON.stringify(currentChatMessages));

                        chatMessagesContainer.scrollTop = chatMessagesContainer.scrollHeight;
                    }, 1000 + Math.random() * 1000); // Случайная задержка
                }
            }

            // Обработчики для выпадающего меню медиа-чата
            mediaChatToggle.addEventListener('click', (event) => {
                event.stopPropagation(); // Предотвращаем закрытие по всплытию
                mediaChatDropdown.classList.toggle('active');
            });

            // Закрытие выпадающего меню при клике в любом месте, кроме него
            document.addEventListener('click', (event) => {
                if (!mediaChatDropdown.contains(event.target)) {
                    mediaChatDropdown.classList.remove('active');
                }
            });

            voiceChatButton.addEventListener('click', () => {
                alert('Голосовой чат пока недоступен. (Beta)');
                mediaChatDropdown.classList.remove('active');
            });

            videoChatButton.addEventListener('click', () => {
                alert('Видеочат пока недоступен. (Beta)');
                mediaChatDropdown.classList.remove('active');
            });

             // Функция для управления видимостью приветствия
             function updateGreetingVisibility() {
                const activeChatId = localStorage.getItem('activeChatId');
                let messagesExist = false;
                if (activeChatId) {
                    const messages = JSON.parse(localStorage.getItem(`chatMessages_${activeChatId}`)) || [];
                    if (messages.length > 0) {
                        messagesExist = true;
                    }
                }

                // Приветствие видно только если активна секция чата и нет сообщений
                if (mainChatSection.classList.contains('active') && !messagesExist) {
                    chatGreeting.classList.remove('hidden');
                } else {
                    chatGreeting.classList.add('hidden');
                }
             }
        });
    </script>

</body>
</html>
