<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lovy-tech | Smart Glasses OS</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Inter', sans-serif;
        }

        body {
            min-height: 100vh;
            overflow: hidden;
            color: white;
        }

        .background-image {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            object-fit: cover;
            z-index: -1;
        }

        /* Header styles */
        header {
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            z-index: 10;
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 1.5rem 2rem;
            opacity: 0;
            animation: fadeIn 0.5s ease-out forwards;
            animation-delay: 0.2s;
        }

        .header-left {
            display: flex;
            align-items: center;
            gap: 1rem;
        }

        .header-title {
            font-size: 1.5rem;
            font-weight: 600;
            text-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
        }

        .header-right {
            display: flex;
            align-items: center;
            gap: 1rem;
        }

        .search-container {
            position: relative;
        }

        .search-icon {
            position: absolute;
            left: 0.75rem;
            top: 50%;
            transform: translateY(-50%);
            color: rgba(255, 255, 255, 0.7);
        }

        .search-input {
            border-radius: 9999px;
            background-color: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(8px);
            padding: 0.5rem 1rem 0.5rem 2.5rem;
            color: white;
            border: 1px solid rgba(255, 255, 255, 0.2);
            outline: none;
        }

        .search-input::placeholder {
            color: rgba(255, 255, 255, 0.7);
        }

        .search-input:focus {
            outline: none;
            box-shadow: 0 0 0 2px rgba(255, 255, 255, 0.3);
        }

        .avatar {
            height: 2.5rem;
            width: 2.5rem;
            border-radius: 9999px;
            background-color: #3b82f6;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }

        /* Main content styles */
        main {
            position: relative;
            height: 100vh;
            width: 100%;
            padding-top: 5rem;
            display: flex;
        }

        /* Sidebar styles */
        .sidebar {
            width: 16rem;
            height: 100%;
            background-color: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(16px);
            padding: 1rem;
            box-shadow: 0 10px 15px rgba(0, 0, 0, 0.1);
            border-right: 1px solid rgba(255, 255, 255, 0.2);
            border-top-right-radius: 1.5rem;
            opacity: 0;
            animation: fadeIn 0.5s ease-out forwards;
            animation-delay: 0.4s;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
        }

        .create-button {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 0.5rem;
            border-radius: 9999px;
            background-color: #3b82f6;
            padding: 0.75rem 1rem;
            color: white;
            width: 100%;
            border: none;
            cursor: pointer;
            margin-bottom: 1.5rem;
        }

        .mini-calendar {
            margin-bottom: 1.5rem;
        }

        .mini-calendar-header {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-bottom: 1rem;
        }

        .mini-calendar-title {
            font-weight: 500;
        }

        .mini-calendar-nav {
            display: flex;
            gap: 0.25rem;
        }

        .mini-calendar-nav-button {
            padding: 0.25rem;
            border-radius: 9999px;
            background: transparent;
            border: none;
            cursor: pointer;
            color: white;
        }

        .mini-calendar-nav-button:hover {
            background-color: rgba(255, 255, 255, 0.2);
        }

        .mini-calendar-grid {
            display: grid;
            grid-template-columns: repeat(7, 1fr);
            gap: 0.25rem;
            text-align: center;
        }

        .mini-calendar-day-name {
            font-size: 0.75rem;
            color: rgba(255, 255, 255, 0.7);
            font-weight: 500;
            padding: 0.25rem;
        }

        .mini-calendar-date {
            font-size: 0.75rem;
            border-radius: 9999px;
            width: 1.75rem;
            height: 1.75rem;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
        }

        .mini-calendar-date:hover {
            background-color: rgba(255, 255, 255, 0.2);
        }

        .mini-calendar-date.current {
            background-color: #3b82f6;
            color: white;
        }

        .mini-calendar-date.empty {
            visibility: hidden;
        }

        .my-calendars-title {
            font-weight: 500;
            margin-bottom: 0.75rem;
        }

        .calendar-list {
            display: flex;
            flex-direction: column;
            gap: 0.5rem;
        }

        .calendar-item {
            display: flex;
            align-items: center;
            gap: 0.75rem;
        }

        .calendar-color {
            width: 0.75rem;
            height: 0.75rem;
            border-radius: 0.125rem;
        }

        .calendar-name {
            font-size: 0.875rem;
        }

        .big-plus-button {
            margin-top: 1.5rem;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 0.5rem;
            border-radius: 9999px;
            background-color: #3b82f6;
            padding: 1rem;
            color: white;
            width: 3.5rem;
            height: 3.5rem;
            border: none;
            cursor: pointer;
            align-self: flex-start;
        }

        /* Calendar view styles */
        .calendar-view {
            flex: 1;
            display: flex;
            flex-direction: column;
            opacity: 0;
            animation: fadeIn 0.5s ease-out forwards;
            animation-delay: 0.6s;
        }

        .calendar-controls {
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 1rem;
            border-bottom: 1px solid rgba(255, 255, 255, 0.2);
        }

        .controls-left {
            display: flex;
            align-items: center;
            gap: 1rem;
        }

        .today-button {
            padding: 0.5rem 1rem;
            color: white;
            background-color: #3b82f6;
            border: none;
            border-radius: 0.375rem;
            cursor: pointer;
        }

        .nav-buttons {
            display: flex;
        }

        .nav-button {
            padding: 0.5rem;
            color: white;
            background: transparent;
            border: none;
            cursor: pointer;
        }

        .nav-button:hover {
            background-color: rgba(255, 255, 255, 0.1);
        }

        .nav-button:first-child {
            border-top-left-radius: 0.375rem;
            border-bottom-left-radius: 0.375rem;
        }

        .nav-button:last-child {
            border-top-right-radius: 0.375rem;
            border-bottom-right-radius: 0.375rem;
        }

        .current-date {
            font-size: 1.25rem;
            font-weight: 600;
        }

        .view-options {
            display: flex;
            align-items: center;
            gap: 0.5rem;
            border-radius: 0.375rem;
            padding: 0.25rem;
        }

        .view-option {
            padding: 0.25rem 0.75rem;
            border-radius: 0.25rem;
            color: white;
            background: transparent;
            border: none;
            font-size: 0.875rem;
            cursor: pointer;
        }

        .view-option.active {
            background-color: rgba(255, 255, 255, 0.2);
        }

        .calendar-content {
            flex: 1;
            overflow: auto;
            padding: 1rem;
        }

        .week-view {
            background-color: rgba(255, 255, 255, 0.2);
            backdrop-filter: blur(16px);
            border-radius: 0.75rem;
            border: 1px solid rgba(255, 255, 255, 0.2);
            box-shadow: 0 20px 25px rgba(0, 0, 0, 0.1);
            height: 100%;
        }

        .week-header {
            display: grid;
            grid-template-columns: repeat(8, 1fr);
            border-bottom: 1px solid rgba(255, 255, 255, 0.2);
        }

        .week-header-cell {
            padding: 0.5rem;
            text-align: center;
        }

        .week-header-cell:not(:first-child) {
            border-left: 1px solid rgba(255, 255, 255, 0.2);
        }

        .week-day {
            font-size: 0.75rem;
            color: rgba(255, 255, 255, 0.7);
            font-weight: 500;
        }

        .week-date {
            font-size: 1.125rem;
            font-weight: 500;
            margin-top: 0.25rem;
        }

        .week-date.current {
            background-color: #3b82f6;
            border-radius: 9999px;
            width: 2rem;
            height: 2rem;
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0.25rem auto 0;
        }

        .time-grid {
            display: grid;
            grid-template-columns: repeat(8, 1fr);
        }

        .time-labels {
            color: rgba(255, 255, 255, 0.7);
        }

        .time-slot {
            height: 5rem;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
            padding-right: 0.5rem;
            text-align: right;
            font-size: 0.75rem;
        }

        .day-column {
            border-left: 1px solid rgba(255, 255, 255, 0.2);
            position: relative;
        }

        .event {
            position: absolute;
            border-radius: 0.375rem;
            padding: 0.5rem;
            color: white;
            font-size: 0.75rem;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            cursor: pointer;
            transition: all 0.2s ease-in-out;
            left: 0.25rem;
            right: 0.25rem;
        }

        .event:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 8px rgba(0, 0, 0, 0.15);
        }

        .event-title {
            font-weight: 500;
        }

        .event-time {
            opacity: 0.8;
            font-size: 0.625rem;
            margin-top: 0.25rem;
        }

        /* AI Popup styles */
        .ai-popup {
            position: fixed;
            bottom: 2rem;
            right: 2rem;
            z-index: 20;
            width: 450px;
            background: linear-gradient(to bottom right, rgba(96, 165, 250, 0.3), rgba(59, 130, 246, 0.3), rgba(37, 99, 235, 0.3));
            backdrop-filter: blur(16px);
            padding: 1.5rem;
            border-radius: 1rem;
            box-shadow: 0 10px 15px rgba(0, 0, 0, 0.1);
            border: 1px solid rgba(147, 197, 253, 0.3);
            color: white;
            display: none;
        }

        .ai-popup.show {
            display: block;
        }

        .close-button {
            position: absolute;
            top: 0.5rem;
            right: 0.5rem;
            color: rgba(255, 255, 255, 0.7);
            background: transparent;
            border: none;
            cursor: pointer;
            transition: color 0.2s;
        }

        .close-button:hover {
            color: white;
        }

        .ai-content {
            display: flex;
            gap: 0.75rem;
        }

        .ai-message {
            min-height: 80px;
            font-weight: 300;
        }

        .ai-actions {
            margin-top: 1.5rem;
            display: flex;
            gap: 0.75rem;
        }

        .ai-button {
            flex: 1;
            padding: 0.625rem;
            background-color: rgba(255, 255, 255, 0.1);
            border: none;
            border-radius: 0.75rem;
            color: white;
            font-size: 0.875rem;
            font-weight: 500;
            cursor: pointer;
            transition: background-color 0.2s;
        }

        .ai-button:hover {
            background-color: rgba(255, 255, 255, 0.2);
        }

        .player-controls {
            margin-top: 1rem;
            display: flex;
            align-items: center;
            justify-content: space-between;
            display: none;
        }

        .player-controls.show {
            display: flex;
        }

        .pause-button {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 0.5rem;
            border-radius: 0.75rem;
            background-color: rgba(255, 255, 255, 0.1);
            padding: 0.625rem 1rem;
            color: white;
            font-size: 0.875rem;
            border: none;
            cursor: pointer;
            transition: background-color 0.2s;
        }

        .pause-button:hover {
            background-color: rgba(255, 255, 255, 0.2);
        }

        /* Event modal styles */
        .modal-overlay {
            position: fixed;
            inset: 0;
            background-color: rgba(0, 0, 0, 0.5);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 50;
            display: none;
        }

        .modal-overlay.show {
            display: flex;
        }

        .event-modal {
            padding: 1.5rem;
            border-radius: 0.5rem;
            box-shadow: 0 20px 25px rgba(0, 0, 0, 0.15);
            max-width: 28rem;
            width: 100%;
            margin: 0 1rem;
        }

        .modal-title {
            font-size: 1.5rem;
            font-weight: 700;
            margin-bottom: 1rem;
        }

        .modal-content {
            display: flex;
            flex-direction: column;
            gap: 0.75rem;
        }

        .modal-item {
            display: flex;
            align-items: center;
        }

        .modal-item-icon {
            margin-right: 0.5rem;
        }

        .modal-item-attendees {
            display: flex;
            align-items: flex-start;
        }

        .modal-actions {
            margin-top: 1.5rem;
            display: flex;
            justify-content: flex-end;
        }

        .close-modal-button {
            background-color: white;
            color: #1f2937;
            padding: 0.5rem 1rem;
            border-radius: 0.25rem;
            border: none;
            cursor: pointer;
            transition: background-color 0.2s;
        }

        .close-modal-button:hover {
            background-color: #f3f4f6;
        }

        /* Animations */
        @keyframes fadeIn {
            from {
                opacity: 0;
            }
            to {
                opacity: 1;
            }
        }

        /* Color classes */
        .bg-blue-500 {
            background-color: #3b82f6;
        }

        .bg-green-500 {
            background-color: #10b981;
        }

        .bg-purple-500 {
            background-color: #8b5cf6;
        }

        .bg-yellow-500 {
            background-color: #f59e0b;
        }

        .bg-indigo-500 {
            background-color: #6366f1;
        }

        .bg-pink-500 {
            background-color: #ec4899;
        }

        .bg-teal-500 {
            background-color: #14b8a6;
        }

        .bg-cyan-500 {
            background-color: #06b6d4;
        }

        .bg-blue-400 {
            background-color: #60a5fa;
        }

        .bg-purple-400 {
            background-color: #a78bfa;
        }

        .bg-red-400 {
            background-color: #f87171;
        }

        .bg-green-400 {
            background-color: #34d399;
        }

        .bg-yellow-400 {
            background-color: #fbbf24;
        }

        .bg-orange-400 {
            background-color: #fb923c;
        }

        .bg-pink-400 {
            background-color: #f472b6;
        }

        /* Responsive styles */
        @media (max-width: 1024px) {
            .sidebar {
                width: 14rem;
            }
        }

        @media (max-width: 768px) {
            header {
                padding: 1rem;
            }

            .header-title {
                font-size: 1.25rem;
            }

            .search-input {
                display: none;
            }

            .sidebar {
                width: 12rem;
            }

            .calendar-controls {
                flex-direction: column;
                gap: 1rem;
                align-items: flex-start;
            }

            .ai-popup {
                width: calc(100% - 2rem);
                right: 1rem;
                left: 1rem;
            }
        }

        @media (max-width: 640px) {
            .sidebar {
                display: none;
            }

            .week-view {
                overflow-x: auto;
            }
        }
    </style>
</head>
<body>
    <!-- Background Image -->
    <img class="background-image" src="https://images.unsplash.com/photo-1506905925346-21bda4d32df4?q=80&w=2070&auto=format&fit=crop" alt="Beautiful mountain landscape">

    <!-- Navigation -->
    <header>
        <div class="header-left">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="menu-icon">
                <line x1="4" x2="20" y1="12" y2="12"></line>
                <line x1="4" x2="20" y1="6" y2="6"></line>
                <line x1="4" x2="20" y1="18" y2="18"></line>
            </svg>
            <span class="header-title">Calendar</span>
        </div>

        <div class="header-right">
            <div class="search-container">
                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="search-icon">
                    <circle cx="11" cy="11" r="8"></circle>
                    <path d="m21 21-4.3-4.3"></path>
                </svg>
                <input type="text" placeholder="Search" class="search-input">
            </div>
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="settings-icon">
                <path d="M12.22 2h-.44a2 2 0 0 0-2 2v.18a2 2 0 0 1-1 1.73l-.43.25a2 2 0 0 1-2 0l-.15-.08a2 2 0 0 0-2.73.73l-.22.38a2 2 0 0 0 .73 2.73l.15.1a2 2 0 0 1 1 1.72v.51a2 2 0 0 1-1 1.74l-.15.09a2 2 0 0 0-.73 2.73l.22.38a2 2 0 0 0 2.73.73l.15-.08a2 2 0 0 1 2 0l.43.25a2 2 0 0 1 1 1.73V20a2 2 0 0 0 2 2h.44a2 2 0 0 0 2-2v-.18a2 2 0 0 1 1-1.73l.43-.25a2 2 0 0 1 2 0l.15.08a2 2 0 0 0 2.73-.73l.22-.39a2 2 0 0 0-.73-2.73l-.15-.08a2 2 0 0 1-1-1.74v-.5a2 2 0 0 1 1-1.74l.15-.09a2 2 0 0 0 .73-2.73l-.22-.38a2 2 0 0 0-2.73-.73l-.15.08a2 2 0 0 1-2 0l-.43-.25a2 2 0 0 1-1-1.73V4a2 2 0 0 0-2-2z"></path>
                <circle cx="12" cy="12" r="3"></circle>
            </svg>
            <div class="avatar">U</div>
        </div>
    </header>

    <!-- Main Content -->
    <main>
        <!-- Sidebar -->
        <div class="sidebar">
            <div>
                <button class="create-button">
                    <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                        <path d="M5 12h14"></path>
                        <path d="M12 5v14"></path>
                    </svg>
                    <span>Create</span>
                </button>

                <!-- Mini Calendar -->
                <div class="mini-calendar">
                    <div class="mini-calendar-header">
                        <h3 class="mini-calendar-title">March 2025</h3>
                        <div class="mini-calendar-nav">
                            <button class="mini-calendar-nav-button">
                                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                                    <path d="m15 18-6-6 6-6"></path>
                                </svg>
                            </button>
                            <button class="mini-calendar-nav-button">
                                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                                    <path d="m9 18 6-6-6-6"></path>
                                </svg>
                            </button>
                        </div>
                    </div>

                    <div class="mini-calendar-grid">
                        <div class="mini-calendar-day-name">S</div>
                        <div class="mini-calendar-day-name">M</div>
                        <div class="mini-calendar-day-name">T</div>
                        <div class="mini-calendar-day-name">W</div>
                        <div class="mini-calendar-day-name">T</div>
                        <div class="mini-calendar-day-name">F</div>
                        <div class="mini-calendar-day-name">S</div>
                    </div>
                </div>

                <!-- My Calendars -->
                <div>
                    <h3 class="my-calendars-title">My calendars</h3>
                    <div class="calendar-list">
                        <div class="calendar-item">
                            <div class="calendar-color bg-blue-500"></div>
                            <span class="calendar-name">My Calendar</span>
                        </div>
                        <div class="calendar-item">
                            <div class="calendar-color bg-green-500"></div>
                            <span class="calendar-name">Work</span>
                        </div>
                        <div class="calendar-item">
                            <div class="calendar-color bg-purple-500"></div>
                            <span class="calendar-name">Personal</span>
                        </div>
                        <div class="calendar-item">
                            <div class="calendar-color bg-yellow-500"></div>
                            <span class="calendar-name">Family</span>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Big plus button -->
            <button class="big-plus-button">
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                    <path d="M5 12h14"></path>
                    <path d="M12 5v14"></path>
                </svg>
            </button>
        </div>

        <!-- Calendar View -->
        <div class="calendar-view">
            <!-- Calendar Controls -->
            <div class="calendar-controls">
                <div class="controls-left">
                    <button class="today-button">Today</button>
                    <div class="nav-buttons">
                        <button class="nav-button">
                            <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                                <path d="m15 18-6-6 6-6"></path>
                            </svg>
                        </button>
                        <button class="nav-button">
                            <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                                <path d="m9 18 6-6-6-6"></path>
                            </svg>
                        </button>
                    </div>
                    <h2 class="current-date">March 5</h2>
                </div>

                <div class="view-options">
                    <button class="view-option" data-view="day">Day</button>
                    <button class="view-option active" data-view="week">Week</button>
                    <button class="view-option" data-view="month">Month</button>
                </div>
            </div>

            <!-- Calendar Content -->
            <div class="calendar-content">
                <div class="week-view">
                    <!-- Week Header -->
                    <div class="week-header">
                        <div class="week-header-cell"></div>
                        <div class="week-header-cell">
                            <div class="week-day">SUN</div>
                            <div class="week-date">3</div>
                        </div>
                        <div class="week-header-cell">
                            <div class="week-day">MON</div>
                            <div class="week-date">4</div>
                        </div>
                        <div class="week-header-cell">
                            <div class="week-day">TUE</div>
                            <div class="week-date current">5</div>
                        </div>
                        <div class="week-header-cell">
                            <div class="week-day">WED</div>
                            <div class="week-date">6</div>
                        </div>
                        <div class="week-header-cell">
                            <div class="week-day">THU</div>
                            <div class="week-date">7</div>
                        </div>
                        <div class="week-header-cell">
                            <div class="week-day">FRI</div>
                            <div class="week-date">8</div>
                        </div>
                        <div class="week-header-cell">
                            <div class="week-day">SAT</div>
                            <div class="week-date">9</div>
                        </div>
                    </div>

                    <!-- Time Grid -->
                    <div class="time-grid">
                        <!-- Time Labels -->
                        <div class="time-labels">
                            <div class="time-slot">8 AM</div>
                            <div class="time-slot">9 AM</div>
                            <div class="time-slot">10 AM</div>
                            <div class="time-slot">11 AM</div>
                            <div class="time-slot">12 PM</div>
                            <div class="time-slot">1 PM</div>
                            <div class="time-slot">2 PM</div>
                            <div class="time-slot">3 PM</div>
                            <div class="time-slot">4 PM</div>
                        </div>

                        <!-- Day Columns -->
                        <div class="day-column" id="day-1">
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                        </div>
                        <div class="day-column" id="day-2">
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                        </div>
                        <div class="day-column" id="day-3">
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                        </div>
                        <div class="day-column" id="day-4">
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                        </div>
                        <div class="day-column" id="day-5">
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                        </div>
                        <div class="day-column" id="day-6">
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                        </div>
                        <div class="day-column" id="day-7">
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                            <div class="time-slot"></div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </main>

    <!-- AI Popup -->
    <div class="ai-popup" id="ai-popup">
        <button class="close-button" id="close-ai-popup">
            <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                <path d="M18 6 6 18"></path>
                <path d="m6 6 12 12"></path>
            </svg>
        </button>
        <div class="ai-content">
            <div>
                <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="#93c5fd" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                    <path d="m12 3-1.912 5.813a2 2 0 0 1-1.275 1.275L3 12l5.813 1.912a2 2 0 0 1 1.275 1.275L12 21l1.912-5.813a2 2 0 0 1 1.275-1.275L21 12l-5.813-1.912a2 2 0 0 1-1.275-1.275L12 3Z"></path>
                    <path d="M5 3v4"></path>
                    <path d="M19 17v4"></path>
                    <path d="M3 5h4"></path>
                    <path d="M17 19h4"></path>
                </svg>
            </div>
            <div class="ai-message" id="ai-message"></div>
        </div>
        <div class="ai-actions">
            <button class="ai-button" id="yes-button">Yes</button>
            <button class="ai-button" id="no-button">No</button>
        </div>
        <div class="player-controls" id="player-controls">
            <button class="pause-button" id="pause-button">
                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                    <rect width="4" height="16" x="6" y="4"></rect>
                    <rect width="4" height="16" x="14" y="4"></rect>
                </svg>
                <span>Pause Hans Zimmer</span>
            </button>
        </div>
    </div>

    <!-- Event Modal -->
    <div class="modal-overlay" id="event-modal-overlay">
        <div class="event-modal" id="event-modal">
            <h3 class="modal-title" id="modal-title"></h3>
            <div class="modal-content">
                <p class="modal-item">
                    <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="modal-item-icon">
                        <circle cx="12" cy="12" r="10"></circle>
                        <polyline points="12 6 12 12 16 14"></polyline>
                    </svg>
                    <span id="modal-time"></span>
                </p>
                <p class="modal-item">
                    <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="modal-item-icon">
                        <path d="M20 10c0 6-8 12-8 12s-8-6-8-12a8 8 0 0 1 16 0Z"></path>
                        <circle cx="12" cy="10" r="3"></circle>
                    </svg>
                    <span id="modal-location"></span>
                </p>
                <p class="modal-item">
                    <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="modal-item-icon">
                        <rect width="18" height="18" x="3" y="4" rx="2" ry="2"></rect>
                        <line x1="16" x2="16" y1="2" y2="6"></line>
                        <line x1="8" x2="8" y1="2" y2="6"></line>
                        <line x1="3" x2="21" y1="10" y2="10"></line>
                    </svg>
                    <span id="modal-date"></span>
                </p>
                <div class="modal-item-attendees">
                    <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="modal-item-icon">
                        <path d="M16 21v-2a4 4 0 0 0-4-4H6a4 4 0 0 0-4 4v2"></path>
                        <circle cx="9" cy="7" r="4"></circle>
                        <path d="M22 21v-2a4 4 0 0 0-3-3.87"></path>
                        <path d="M16 3.13a4 4 0 0 1 0 7.75"></path>
                    </svg>
                    <span>
                        <strong>Attendees:</strong><br>
                        <span id="modal-attendees"></span>
                    </span>
                </div>
                <p>
                    <strong>Organizer:</strong> <span id="modal-organizer"></span>
                </p>
                <p>
                    <strong>Description:</strong> <span id="modal-description"></span>
                </p>
            </div>
            <div class="modal-actions">
                <button class="close-modal-button" id="close-modal-button">Close</button>
            </div>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // Sample calendar events
            const events = [
                {
                    id: 1,
                    title: "Team Meeting",
                    startTime: "09:00",
                    endTime: "10:00",
                    color: "bg-blue-500",
                    day: 1,
                    description: "Weekly team sync-up",
                    location: "Conference Room A",
                    attendees: ["John Doe", "Jane Smith", "Bob Johnson"],
                    organizer: "Alice Brown",
                },
                {
                    id: 2,
                    title: "Lunch with Sarah",
                    startTime: "12:30",
                    endTime: "13:30",
                    color: "bg-green-500",
                    day: 1,
                    description: "Discuss project timeline",
                    location: "Cafe Nero",
                    attendees: ["Sarah Lee"],
                    organizer: "You",
                },
                {
                    id: 3,
                    title: "Project Review",
                    startTime: "14:00",
                    endTime: "15:30",
                    color: "bg-purple-500",
                    day: 3,
                    description: "Q2 project progress review",
                    location: "Meeting Room 3",
                    attendees: ["Team Alpha", "Stakeholders"],
                    organizer: "Project Manager",
                },
                {
                    id: 4,
                    title: "Client Call",
                    startTime: "10:00",
                    endTime: "11:00",
                    color: "bg-yellow-500",
                    day: 2,
                    description: "Quarterly review with major client",
                    location: "Zoom Meeting",
                    attendees: ["Client Team", "Sales Team"],
                    organizer: "Account Manager",
                },
                {
                    id: 5,
                    title: "Team Brainstorm",
                    startTime: "13:00",
                    endTime: "14:30",
                    color: "bg-indigo-500",
                    day: 4,
                    description: "Ideation session for new product features",
                    location: "Creative Space",
                    attendees: ["Product Team", "Design Team"],
                    organizer: "Product Owner",
                },
                {
                    id: 6,
                    title: "Product Demo",
                    startTime: "11:00",
                    endTime: "12:00",
                    color: "bg-pink-500",
                    day: 5,
                    description: "Showcase new features to stakeholders",
                    location: "Demo Room",
                    attendees: ["Stakeholders", "Dev Team"],
                    organizer: "Tech Lead",
                },
                {
                    id: 7,
                    title: "Marketing Meeting",
                    startTime: "13:00",
                    endTime: "14:00",
                    color: "bg-teal-500",
                    day: 6,
                    description: "Discuss Q3 marketing strategy",
                    location: "Marketing Office",
                    attendees: ["Marketing Team"],
                    organizer: "Marketing Director",
                },
                {
                    id: 8,
                    title: "Code Review",
                    startTime: "15:00",
                    endTime: "16:00",
                    color: "bg-cyan-500",
                    day: 7,
                    description: "Review pull requests for new feature",
                    location: "Dev Area",
                    attendees: ["Dev Team"],
                    organizer: "Senior Developer",
                },
                {
                    id: 9,
                    title: "Morning Standup",
                    startTime: "08:30",
                    endTime: "09:30",
                    color: "bg-blue-400",
                    day: 2,
                    description: "Daily team standup",
                    location: "Slack Huddle",
                    attendees: ["Development Team"],
                    organizer: "Scrum Master",
                },
                {
                    id: 10,
                    title: "Design Review",
                    startTime: "14:30",
                    endTime: "15:45",
                    color: "bg-purple-400",
                    day: 5,
                    description: "Review new UI designs",
                    location: "Design Lab",
                    attendees: ["UX Team", "Product Manager"],
                    organizer: "Lead Designer",
                },
                {
                    id: 11,
                    title: "Investor Meeting",
                    startTime: "10:30",
                    endTime: "12:00",
                    color: "bg-red-400",
                    day: 7,
                    description: "Quarterly investor update",
                    location: "Board Room",
                    attendees: ["Executive Team", "Investors"],
                    organizer: "CEO",
                },
                {
                    id: 12,
                    title: "Team Training",
                    startTime: "09:30",
                    endTime: "11:30",
                    color: "bg-green-400",
                    day: 4,
                    description: "New tool onboarding session",
                    location: "Training Room",
                    attendees: ["All Departments"],
                    organizer: "HR",
                },
                {
                    id: 13,
                    title: "Budget Review",
                    startTime: "13:30",
                    endTime: "15:00",
                    color: "bg-yellow-400",
                    day: 3,
                    description: "Quarterly budget analysis",
                    location: "Finance Office",
                    attendees: ["Finance Team", "Department Heads"],
                    organizer: "CFO",
                },
                {
                    id: 14,
                    title: "Client Presentation",
                    startTime: "11:00",
                    endTime: "12:30",
                    color: "bg-orange-400",
                    day: 6,
                    description: "Present new project proposal",
                    location: "Client Office",
                    attendees: ["Sales Team", "Client Representatives"],
                    organizer: "Account Executive",
                },
                {
                    id: 15,
                    title: "Product Planning",
                    startTime: "14:00",
                    endTime: "15:30",
                    color: "bg-pink-400",
                    day: 1,
                    description: "Roadmap discussion for Q3",
                    location: "Strategy Room",
                    attendees: ["Product Team", "Engineering Leads"],
                    organizer: "Product Manager",
                },
            ];

            // Generate mini calendar dates
            const daysInMonth = 31;
            const firstDayOffset = 5; // Friday is the first day of the month in this example
            const miniCalendarGrid = document.querySelector('.mini-calendar-grid');
            
            // Add day names (already in HTML)
            
            // Add dates
            for (let i = 0; i < daysInMonth + firstDayOffset; i++) {
                const dateDiv = document.createElement('div');
                dateDiv.className = 'mini-calendar-date';
                
                if (i < firstDayOffset) {
                    dateDiv.classList.add('empty');
                } else {
                    const date = i - firstDayOffset + 1;
                    dateDiv.textContent = date;
                    
                    if (date === 5) {
                        dateDiv.classList.add('current');
                    }
                }
                
                miniCalendarGrid.appendChild(dateDiv);
            }

            // Helper function to calculate event position and height
            function calculateEventStyle(startTime, endTime) {
                const start = parseInt(startTime.split(':')[0]) + parseInt(startTime.split(':')[1]) / 60;
                const end = parseInt(endTime.split(':')[0]) + parseInt(endTime.split(':')[1]) / 60;
                const top = (start - 8) * 80; // 80px per hour
                const height = (end - start) * 80;
                return { top: `${top}px`, height: `${height}px` };
            }

            // Render events
            events.forEach(event => {
                const dayColumn = document.getElementById(`day-${event.day}`);
                const eventStyle = calculateEventStyle(event.startTime, event.endTime);
                
                const eventDiv = document.createElement('div');
                eventDiv.className = `event ${event.color}`;
                eventDiv.style.top = eventStyle.top;
                eventDiv.style.height = eventStyle.height;
                eventDiv.dataset.event = JSON.stringify(event);
                
                const titleDiv = document.createElement('div');
                titleDiv.className = 'event-title';
                titleDiv.textContent = event.title;
                
                const timeDiv = document.createElement('div');
                timeDiv.className = 'event-time';
                timeDiv.textContent = `${event.startTime} - ${event.endTime}`;
                
                eventDiv.appendChild(titleDiv);
                eventDiv.appendChild(timeDiv);
                
                dayColumn.appendChild(eventDiv);
                
                // Add event listener
                eventDiv.addEventListener('click', function() {
                    const eventData = JSON.parse(this.dataset.event);
                    showEventModal(eventData);
                });
            });

            // View options
            const viewOptions = document.querySelectorAll('.view-option');
            viewOptions.forEach(option => {
                option.addEventListener('click', function() {
                    viewOptions.forEach(opt => opt.classList.remove('active'));
                    this.classList.add('active');
                    // Here you would typically switch the view based on the selected option
                });
            });

            // AI Popup
            const aiPopup = document.getElementById('ai-popup');
            const aiMessage = document.getElementById('ai-message');
            const closeAiPopup = document.getElementById('close-ai-popup');
            const yesButton = document.getElementById('yes-button');
            const noButton = document.getElementById('no-button');
            const playerControls = document.getElementById('player-controls');
            const pauseButton = document.getElementById('pause-button');
            
            // Show AI popup after 3 seconds
            setTimeout(() => {
                aiPopup.classList.add('show');
                typeMessage("Looks like you don't have that many meetings today. Shall I play some Hans Zimmer essentials to help you get into your Flow State?");
            }, 3000);
            
            // Type message character by character
            function typeMessage(text) {
                let i = 0;
                aiMessage.textContent = '';
                const typingInterval = setInterval(() => {
                    if (i < text.length) {
                        aiMessage.textContent += text.charAt(i);
                        i++;
                    } else {
                        clearInterval(typingInterval);
                    }
                }, 50);
            }
            
            // Close AI popup
            closeAiPopup.addEventListener('click', () => {
                aiPopup.classList.remove('show');
            });
            
            // Yes button - Start playing music
            yesButton.addEventListener('click', () => {
                playerControls.classList.add('show');
                // Here you would typically start playing music
            });
            
            // No button - Close popup
            noButton.addEventListener('click', () => {
                aiPopup.classList.remove('show');
            });
            
            // Pause button - Toggle play/pause
            let isPlaying = true;
            pauseButton.addEventListener('click', () => {
                isPlaying = !isPlaying;
                if (isPlaying) {
                    pauseButton.innerHTML = `
                        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                            <rect width="4" height="16" x="6" y="4"></rect>
                            <rect width="4" height="16" x="14" y="4"></rect>
                        </svg>
                        <span>Pause Hans Zimmer</span>
                    `;
                    // Here you would typically resume playing music
                } else {
                    pauseButton.innerHTML = `
                        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                            <polygon points="5 3 19 12 5 21 5 3"></polygon>
                        </svg>
                        <span>Play Hans Zimmer</span>
                    `;
                    // Here you would typically pause the music
                }
            });

            // Event Modal
            const eventModalOverlay = document.getElementById('event-modal-overlay');
            const eventModal = document.getElementById('event-modal');
            const modalTitle = document.getElementById('modal-title');
            const modalTime = document.getElementById('modal-time');
            const modalLocation = document.getElementById('modal-location');
            const modalDate = document.getElementById('modal-date');
            const modalAttendees = document.getElementById('modal-attendees');
            const modalOrganizer = document.getElementById('modal-organizer');
            const modalDescription = document.getElementById('modal-description');
            const closeModalButton = document.getElementById('close-modal-button');
            
            // Show event modal
            function showEventModal(event) {
                modalTitle.textContent = event.title;
                modalTime.textContent = `${event.startTime} - ${event.endTime}`;
                modalLocation.textContent = event.location;
                
                const weekDays = ["SUN", "MON", "TUE", "WED", "THU", "FRI", "SAT"];
                const weekDates = [3, 4, 5, 6, 7, 8, 9];
                modalDate.textContent = `${weekDays[event.day - 1]}, ${weekDates[event.day - 1]} March 2025`;
                
                modalAttendees.textContent = event.attendees.join(', ') || 'No attendees';
                modalOrganizer.textContent = event.organizer;
                modalDescription.textContent = event.description;
                
                // Set modal color based on event color
                eventModal.className = `event-modal ${event.color}`;
                
                eventModalOverlay.classList.add('show');
            }
            
            // Close event modal
            closeModalButton.addEventListener('click', () => {
                eventModalOverlay.classList.remove('show');
            });
            
            // Close modal when clicking outside
            eventModalOverlay.addEventListener('click', (e) => {
                if (e.target === eventModalOverlay) {
                    eventModalOverlay.classList.remove('show');
                }
            });
        });
    </script>
</body>
</html>
