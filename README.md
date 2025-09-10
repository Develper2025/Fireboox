<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Fireboox</title>
    <meta name="description" content="A lightweight browser experience">
    <style>
        /* CSS Variables for Theming */
        :root {
            /* Light theme (default) */
            --bg-primary: #f8f9fa;
            --bg-secondary: #ffffff;
            --text-primary: #202124;
            --text-secondary: #5f6368;
            --accent-color: #1a73e8;
            --border-color: #dadce0;
            --shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
            --card-shadow: 0 1px 6px rgba(0, 0, 0, 0.1);
            --hover-bg: rgba(32, 33, 36, 0.059);
        }

        /* Dark theme */
        [data-theme="dark"] {
            --bg-primary: #202124;
            --bg-secondary: #303134;
            --text-primary: #e8eaed;
            --text-secondary: #9aa0a6;
            --accent-color: #8ab4f8;
            --border-color: #5f6368;
            --shadow: 0 1px 3px rgba(0, 0, 0, 0.3);
            --card-shadow: 0 1px 6px rgba(0, 0, 0, 0.3);
            --hover-bg: rgba(232, 234, 237, 0.08);
        }

        /* Base styles */
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
            background-color: var(--bg-primary);
            color: var(--text-primary);
            line-height: 1.5;
            transition: background-color 0.3s ease, color 0.3s ease;
        }

        /* Reduced motion for accessibility */
        @media (prefers-reduced-motion: reduce) {
            * {
                animation-duration: 0.01ms !important;
                animation-iteration-count: 1 !important;
                transition-duration: 0.01ms !important;
            }
        }

        /* App container */
        .app-container {
            max-width: 100%;
            min-height: 100vh;
            padding: 0;
            margin: 0 auto;
        }

        /* Top bar styles */
        .top-bar {
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 0.75rem 1rem;
            background-color: var(--bg-secondary);
            border-bottom: 1px solid var(--border-color);
            box-shadow: var(--shadow);
            position: sticky;
            top: 0;
            z-index: 100;
        }

        .logo-container {
            display: flex;
            align-items: center;
            gap: 0.75rem;
        }

        .logo {
            font-weight: bold;
            font-size: 1.25rem;
            color: var(--accent-color);
        }

        .app-name {
            font-size: 1rem;
            color: var(--text-primary);
        }

        .button-group {
            display: flex;
            gap: 0.5rem;
        }

        .icon-button {
            background: none;
            border: none;
            width: 2.5rem;
            height: 2.5rem;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            color: var(--text-secondary);
            transition: background-color 0.2s;
        }

        .icon-button:hover {
            background-color: var(--hover-bg);
        }

        .icon-button svg {
            width: 1.25rem;
            height: 1.25rem;
            fill: currentColor;
        }

        /* Main content */
        .main-content {
            padding: 1.5rem 1rem;
            max-width: 800px;
            margin: 0 auto;
            width: 100%;
        }

        /* Search box */
        .search-container {
            margin-bottom: 2rem;
            animation: subtle-glow 2s ease;
        }

        @keyframes subtle-glow {
            0% { box-shadow: 0 0 10px rgba(26, 115, 232, 0.3); }
            100% { box-shadow: none; }
        }

        .search-form {
            display: flex;
            margin-bottom: 1rem;
        }

        .search-input {
            flex: 1;
            padding: 0.75rem 1rem;
            border: 1px solid var(--border-color);
            border-radius: 24px 0 0 24px;
            font-size: 1rem;
            background-color: var(--bg-secondary);
            color: var(--text-primary);
        }

        .search-button {
            padding: 0 1.5rem;
            background-color: var(--accent-color);
            color: white;
            border: none;
            border-radius: 0 24px 24px 0;
            cursor: pointer;
            font-size: 1rem;
        }

        /* Quick links */
        .quick-links {
            margin-bottom: 2rem;
        }

        .section-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1rem;
        }

        .section-title {
            font-size: 1.125rem;
            font-weight: 500;
        }

        .add-button {
            background: none;
            border: none;
            color: var(--accent-color);
            cursor: pointer;
            font-size: 0.875rem;
            display: flex;
            align-items: center;
            gap: 0.25rem;
        }

        .links-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(80px, 1fr));
            gap: 1rem;
        }

        .link-card {
            background-color: var(--bg-secondary);
            border-radius: 12px;
            padding: 0.75rem;
            display: flex;
            flex-direction: column;
            align-items: center;
            text-decoration: none;
            color: var(--text-primary);
            box-shadow: var(--card-shadow);
            transition: transform 0.2s, box-shadow 0.2s;
            position: relative;
        }

        .link-card:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
        }

        .link-icon {
            width: 2rem;
            height: 2rem;
            margin-bottom: 0.5rem;
            border-radius: 50%;
            background-color: var(--bg-primary);
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            color: var(--accent-color);
        }

        .link-name {
            font-size: 0.75rem;
            text-align: center;
            overflow: hidden;
            text-overflow: ellipsis;
            white-space: nowrap;
            width: 100%;
        }

        .remove-link {
            position: absolute;
            top: -0.25rem;
            right: -0.25rem;
            background-color: var(--bg-secondary);
            border: 1px solid var(--border-color);
            border-radius: 50%;
            width: 1.25rem;
            height: 1.25rem;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            font-size: 0.75rem;
            color: var(--text-secondary);
        }

        /* Bookmarks */
        .bookmarks {
            margin-bottom: 2rem;
        }

        .bookmarks-list {
            list-style: none;
        }

        .bookmark-item {
            display: flex;
            align-items: center;
            padding: 0.75rem;
            background-color: var(--bg-secondary);
            border-radius: 8px;
            margin-bottom: 0.5rem;
            box-shadow: var(--card-shadow);
        }

        .bookmark-icon {
            margin-right: 0.75rem;
            width: 1.5rem;
            height: 1.5rem;
            border-radius: 50%;
            background-color: var(--bg-primary);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 0.75rem;
            color: var(--accent-color);
        }

        .bookmark-details {
            flex: 1;
        }

        .bookmark-title {
            font-size: 0.875rem;
            margin-bottom: 0.25rem;
        }

        .bookmark-url {
            font-size: 0.75rem;
            color: var(--text-secondary);
        }

        .bookmark-actions {
            display: flex;
            gap: 0.5rem;
        }

        /* History */
        .history-list {
            list-style: none;
        }

        .history-item {
            padding: 0.75rem;
            background-color: var(--bg-secondary);
            border-radius: 8px;
            margin-bottom: 0.5rem;
            box-shadow: var(--card-shadow);
        }

        .history-query {
            font-size: 0.875rem;
            margin-bottom: 0.25rem;
        }

        .history-time {
            font-size: 0.75rem;
            color: var(--text-secondary);
        }

        /* Modal */
        .modal-backdrop {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: rgba(0, 0, 0, 0.5);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 1000;
            padding: 1rem;
        }

        .modal {
            background-color: var(--bg-secondary);
            border-radius: 12px;
            padding: 1.5rem;
            width: 100%;
            max-width: 400px;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.15);
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1.5rem;
        }

        .modal-title {
            font-size: 1.25rem;
            font-weight: 500;
        }

        .close-modal {
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            color: var(--text-secondary);
        }

        .form-group {
            margin-bottom: 1rem;
        }

        .form-label {
            display: block;
            margin-bottom: 0.5rem;
            font-size: 0.875rem;
        }

        .form-input {
            width: 100%;
            padding: 0.75rem;
            border: 1px solid var(--border-color);
            border-radius: 8px;
            background-color: var(--bg-primary);
            color: var(--text-primary);
        }

        .modal-actions {
            display: flex;
            justify-content: flex-end;
            gap: 0.75rem;
            margin-top: 1.5rem;
        }

        .button {
            padding: 0.5rem 1rem;
            border-radius: 8px;
            border: none;
            cursor: pointer;
            font-size: 0.875rem;
        }

        .button-secondary {
            background-color: var(--bg-primary);
            color: var(--text-primary);
            border: 1px solid var(--border-color);
        }

        .button-primary {
            background-color: var(--accent-color);
            color: white;
        }

        /* PSE containers */
        .pse-search-container {
            margin-bottom: 1rem;
        }

        .pse-results-container {
            min-height: 400px;
        }

        /* Incognito indicator */
        .incognito-indicator {
            position: fixed;
            bottom: 1rem;
            right: 1rem;
            background-color: rgba(0, 0, 0, 0.7);
            color: white;
            padding: 0.5rem 1rem;
            border-radius: 20px;
            font-size: 0.875rem;
            display: flex;
            align-items: center;
            gap: 0.5rem;
            z-index: 100;
        }

        /* Utility classes */
        .hidden {
            display: none;
        }

        .sr-only {
            position: absolute;
            width: 1px;
            height: 1px;
            padding: 0;
            margin: -1px;
            overflow: hidden;
            clip: rect(0, 0, 0, 0);
            white-space: nowrap;
            border: 0;
        }

        /* Responsive adjustments */
        @media (min-width: 640px) {
            .top-bar {
                padding: 0.75rem 2rem;
            }
            
            .main-content {
                padding: 2rem;
            }
            
            .search-input {
                padding: 1rem 1.5rem;
            }
            
            .links-grid {
                grid-template-columns: repeat(auto-fill, minmax(100px, 1fr));
            }
        }
    </style>
</head>
<body>
    <div class="app-container">
        <!-- Top bar with logo and controls -->
        <header class="top-bar">
            <div class="logo-container">
                <div class="logo">F</div>
                <div class="app-name">Fireboox</div>
            </div>
            <div class="button-group">
                <button class="icon-button theme-toggle" aria-label="Toggle theme">
                    <svg viewBox="0 0 24 24">
                        <path d="M12 22c5.523 0 10-4.477 10-10S17.523 2 12 2 2 6.477 2 12s4.477 10 10 10zm0-18a8 8 0 1 1 0 16 8 8 0 0 1 0-16z"/>
                    </svg>
                </button>
                <button class="icon-button incognito-toggle" aria-label="Toggle incognito mode">
                    <svg viewBox="0 0 24 24">
                        <path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm0 18c-4.42 0-8-3.58-8-8s3.58-8 8-8 8 3.58 8 8-3.58 8-8 8zm4.5-8c0 1.93-1.57 3.5-3.5 3.5s-3.5-1.57-3.5-3.5 1.57-3.5 3.5-3.5 3.5 1.57 3.5 3.5z"/>
                    </svg>
                </button>
                <button class="icon-button clear-data" aria-label="Clear browsing data">
                    <svg viewBox="0 0 24 24">
                        <path d="M19 4h-3.5l-1-1h-5l-1 1H5v2h14V4zm0 16c0 1.1-.9 2-2 2H7c-1.1 0-2-.9-2-2V8c0-1.1.9-2 2-2h10c1.1 0 2 .9 2 2v12zM9 10h2v8H9v-8zm4 0h2v8h-2v-8z"/>
                    </svg>
                </button>
            </div>
        </header>

        <!-- Main content area -->
        <main class="main-content">
            <!-- Search container -->
            <div class="search-container">
                <form class="search-form" id="search-form">
                    <input type="text" class="search-input" id="search-input" placeholder="Search the web..." aria-label="Search the web">
                    <button type="submit" class="search-button">Search</button>
                </form>
                
                <!-- PSE search container -->
                <div class="pse-search-container hidden">
                    <!-- PASTE_PSE_SCRIPT_HERE -->
                    <div class="gcse-search"></div>
                </div>
            </div>

            <!-- Quick links section -->
            <section class="quick-links">
                <div class="section-header">
                    <h2 class="section-title">Quick Links</h2>
                    <button class="add-button" id="add-link-btn">
                        <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor">
                            <path d="M19 13h-6v6h-2v-6H5v-2h6V5h2v6h6v2z"/>
                        </svg>
                        Add
                    </button>
                </div>
                <div class="links-grid" id="links-grid"></div>
            </section>

            <!-- Bookmarks section -->
            <section class="bookmarks">
                <div class="section-header">
                    <h2 class="section-title">Bookmarks</h2>
                    <button class="add-button" id="add-bookmark-btn">
                        <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor">
                            <path d="M19 13h-6v6h-2v-6H5v-2h6V5h2v6h6v2z"/>
                        </svg>
                        Add
                    </button>
                </div>
                <ul class="bookmarks-list" id="bookmarks-list"></ul>
            </section>

            <!-- Recent searches/history section -->
            <section class="history">
                <div class="section-header">
                    <h2 class="section-title">Recent Searches</h2>
                    <button class="add-button hidden"> <!-- Hidden as it's not needed for history -->
                        Add
                    </button>
                </div>
                <ul class="history-list" id="history-list"></ul>
            </section>

            <!-- PSE results container -->
            <div class="pse-results-container hidden">
                <div class="gcse-searchresults"></div>
            </div>
        </main>

        <!-- Incognito mode indicator -->
        <div class="incognito-indicator hidden" id="incognito-indicator">
            <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor">
                <path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm0 18c-4.42 0-8-3.58-8-8s3.58-8 8-8 8 3.58 8 8-3.58 8-8 8zm4.5-8c0 1.93-1.57 3.5-3.5 3.5s-3.5-1.57-3.5-3.5 1.57-3.5 3.5-3.5 3.5 1.57 3.5 3.5z"/>
            </svg>
            Incognito Mode
        </div>

        <!-- Modal for adding links/bookmarks -->
        <div class="modal-backdrop hidden" id="modal-backdrop">
            <div class="modal">
                <div class="modal-header">
                    <h3 class="modal-title" id="modal-title">Add Link</h3>
                    <button class="close-modal" id="close-modal">&times;</button>
                </div>
                <form id="modal-form">
                    <div class="form-group">
                        <label for="item-name" class="form-label">Name</label>
                        <input type="text" class="form-input" id="item-name" required>
                    </div>
                    <div class="form-group">
                        <label for="item-url" class="form-label">URL</label>
                        <input type="url" class="form-input" id="item-url" required>
                    </div>
                    <div class="modal-actions">
                        <button type="button" class="button button-secondary" id="cancel-modal">Cancel</button>
                        <button type="submit" class="button button-primary">Save</button>
                    </div>
                </form>
            </div>
        </div>
    </div>

    <script>
        /* STORAGE */
        // Storage keys
        const STORAGE_KEYS = {
            THEME: 'fireboox-theme',
            LINKS: 'fireboox-links',
            BOOKMARKS: 'fireboox-bookmarks',
            HISTORY: 'fireboox-history',
            INCOGNITO: 'fireboox-incognito'
        };

        // Default quick links
        const DEFAULT_LINKS = [
            { name: 'YouTube', url: 'https://youtube.com' },
            { name: 'Facebook', url: 'https://facebook.com' },
            { name: 'Google', url: 'https://google.com' },
            { name: 'Twitter', url: 'https://twitter.com' },
            { name: 'Instagram', url: 'https://instagram.com' },
            { name: 'Wikipedia', url: 'https://wikipedia.org' }
        ];

        // Get data from localStorage
        function getStorageData(key, fallback = []) {
            try {
                const data = localStorage.getItem(key);
                return data ? JSON.parse(data) : fallback;
            } catch (error) {
                console.error(`Error reading from localStorage for key "${key}":`, error);
                return fallback;
            }
        }

        // Save data to localStorage
        function setStorageData(key, data) {
            try {
                localStorage.setItem(key, JSON.stringify(data));
            } catch (error) {
                console.error(`Error saving to localStorage for key "${key}":`, error);
            }
        }

        /* THEME */
        // Initialize theme
        function initTheme() {
            const savedTheme = localStorage.getItem(STORAGE_KEYS.THEME);
            const systemPrefersDark = window.matchMedia('(prefers-color-scheme: dark)').matches;
            
            if (savedTheme) {
                document.documentElement.setAttribute('data-theme', savedTheme);
            } else if (systemPrefersDark) {
                document.documentElement.setAttribute('data-theme', 'dark');
            }
        }

        // Toggle theme
        function toggleTheme() {
            const currentTheme = document.documentElement.getAttribute('data-theme') || 'light';
            const newTheme = currentTheme === 'light' ? 'dark' : 'light';
            
            document.documentElement.setAttribute('data-theme', newTheme);
            localStorage.setItem(STORAGE_KEYS.THEME, newTheme);
        }

        /* APP STATE */
        let isIncognitoMode = false;
        let currentModalType = null;

        // Toggle incognito mode
        function toggleIncognitoMode() {
            isIncognitoMode = !isIncognitoMode;
            
            // Update UI
            const indicator = document.getElementById('incognito-indicator');
            if (isIncognitoMode) {
                indicator.classList.remove('hidden');
                localStorage.setItem(STORAGE_KEYS.INCOGNITO, 'true');
            } else {
                indicator.classList.add('hidden');
                localStorage.removeItem(STORAGE_KEYS.INCOGNITO);
            }
        }

        // Clear all data
        function clearAllData() {
            if (confirm('Are you sure you want to clear all browsing data? This cannot be undone.')) {
                localStorage.removeItem(STORAGE_KEYS.LINKS);
                localStorage.removeItem(STORAGE_KEYS.BOOKMARKS);
                localStorage.removeItem(STORAGE_KEYS.HISTORY);
                
                // Reload the page to reflect changes
                location.reload();
            }
        }

        /* UI MANAGEMENT */
        // Render quick links
        function renderQuickLinks() {
            const linksGrid = document.getElementById('links-grid');
            const links = getStorageData(STORAGE_KEYS.LINKS, DEFAULT_LINKS);
            
            linksGrid.innerHTML = '';
            
            links.forEach((link, index) => {
                const linkElement = document.createElement('a');
                linkElement.href = link.url;
                linkElement.className = 'link-card';
                linkElement.target = '_blank';
                linkElement.rel = 'noopener';
                
                linkElement.innerHTML = `
                    <div class="link-icon">${link.name.charAt(0)}</div>
                    <div class="link-name">${link.name}</div>
                    <button class="remove-link" data-index="${index}" aria-label="Remove ${link.name}">×</button>
                `;
                
                linksGrid.appendChild(linkElement);
            });
            
            // Add event listeners to remove buttons
            document.querySelectorAll('.remove-link').forEach(button => {
                button.addEventListener('click', (e) => {
                    e.preventDefault();
                    e.stopPropagation();
                    
                    const index = parseInt(button.getAttribute('data-index'));
                    removeLink(index);
                });
            });
        }

        // Remove a quick link
        function removeLink(index) {
            const links = getStorageData(STORAGE_KEYS.LINKS, DEFAULT_LINKS);
            links.splice(index, 1);
            setStorageData(STORAGE_KEYS.LINKS, links);
            renderQuickLinks();
        }

        // Add a new quick link
        function addNewLink(name, url) {
            const links = getStorageData(STORAGE_KEYS.LINKS, DEFAULT_LINKS);
            links.push({ name, url });
            setStorageData(STORAGE_KEYS.LINKS, links);
            renderQuickLinks();
        }

        // Render bookmarks
        function renderBookmarks() {
            const bookmarksList = document.getElementById('bookmarks-list');
            const bookmarks = getStorageData(STORAGE_KEYS.BOOKMARKS, []);
            
            bookmarksList.innerHTML = '';
            
            if (bookmarks.length === 0) {
                bookmarksList.innerHTML = '<p style="padding: 1rem; text-align: center; color: var(--text-secondary);">No bookmarks yet</p>';
                return;
            }
            
            bookmarks.forEach((bookmark, index) => {
                const listItem = document.createElement('li');
                listItem.className = 'bookmark-item';
                
                listItem.innerHTML = `
                    <div class="bookmark-icon">${bookmark.name.charAt(0)}</div>
                    <div class="bookmark-details">
                        <div class="bookmark-title">${bookmark.name}</div>
                        <div class="bookmark-url">${bookmark.url}</div>
                    </div>
                    <div class="bookmark-actions">
                        <button class="icon-button" aria-label="Visit ${bookmark.name}" onclick="window.open('${bookmark.url}', '_blank')">
                            <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor">
                                <path d="M19 19H5V5h7V3H5c-1.11 0-2 .9-2 2v14c0 1.1.89 2 2 2h14c1.1 0 2-.9 2-2v-7h-2v7zM14 3v2h3.59l-9.83 9.83 1.41 1.41L19 6.41V10h2V3h-7z"/>
                            </svg>
                        </button>
                        <button class="icon-button" aria-label="Remove bookmark" data-index="${index}">
                            <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor">
                                <path d="M19 4h-3.5l-1-1h-5l-1 1H5v2h14V4zm0 16c0 1.1-.9 2-2 2H7c-1.1 0-2-.9-2-2V8c0-1.1.9-2 2-2h10c1.1 0 2 .9 2 2v12zM9 10h2v8H9v-8zm4 0h2v8h-2v-8z"/>
                            </svg>
                        </button>
                    </div>
                `;
                
                bookmarksList.appendChild(listItem);
            });
            
            // Add event listeners to remove buttons
            document.querySelectorAll('.bookmark-actions .icon-button:last-child').forEach(button => {
                button.addEventListener('click', () => {
                    const index = parseInt(button.getAttribute('data-index'));
                    removeBookmark(index);
                });
            });
        }

        // Remove a bookmark
        function removeBookmark(index) {
            const bookmarks = getStorageData(STORAGE_KEYS.BOOKMARKS, []);
            bookmarks.splice(index, 1);
            setStorageData(STORAGE_KEYS.BOOKMARKS, bookmarks);
            renderBookmarks();
        }

        // Add a new bookmark
        function addNewBookmark(name, url) {
            const bookmarks = getStorageData(STORAGE_KEYS.BOOKMARKS, []);
            bookmarks.push({ name, url });
            setStorageData(STORAGE_KEYS.BOOKMARKS, bookmarks);
            renderBookmarks();
        }

        // Render search history
        function renderHistory() {
            const historyList = document.getElementById('history-list');
            const history = getStorageData(STORAGE_KEYS.HISTORY, []);
            
            historyList.innerHTML = '';
            
            if (history.length === 0) {
                historyList.innerHTML = '<p style="padding: 1rem; text-align: center; color: var(--text-secondary);">No search history yet</p>';
                return;
            }
            
            // Show only the 10 most recent searches
            const recentHistory = history.slice(-10).reverse();
            
            recentHistory.forEach(item => {
                const listItem = document.createElement('li');
                listItem.className = 'history-item';
                
                listItem.innerHTML = `
                    <div class="history-query">${item.query}</div>
                    <div class="history-time">${new Date(item.timestamp).toLocaleString()}</div>
                `;
                
                // Add click event to search again
                listItem.addEventListener('click', () => {
                    document.getElementById('search-input').value = item.query;
                    performSearch(item.query);
                });
                
                historyList.appendChild(listItem);
            });
        }

        // Add to search history
        function addToHistory(query) {
            if (isIncognitoMode) return;
            
            const history = getStorageData(STORAGE_KEYS.HISTORY, []);
            history.push({
                query,
                timestamp: Date.now()
            });
            
            setStorageData(STORAGE_KEYS.HISTORY, history);
            renderHistory();
        }

        /* MODAL MANAGEMENT */
        // Open modal for adding items
        function openModal(type) {
            currentModalType = type;
            const modal = document.getElementById('modal-backdrop');
            const title = document.getElementById('modal-title');
            const form = document.getElementById('modal-form');
            
            // Set modal title based on type
            if (type === 'link') {
                title.textContent = 'Add Quick Link';
            } else if (type === 'bookmark') {
                title.textContent = 'Add Bookmark';
            }
            
            // Reset form
            form.reset();
            
            // Show modal
            modal.classList.remove('hidden');
        }

        // Close modal
        function closeModal() {
            const modal = document.getElementById('modal-backdrop');
            modal.classList.add('hidden');
            currentModalType = null;
        }

        // Handle modal form submission
        function handleModalSubmit(e) {
            e.preventDefault();
            
            const name = document.getElementById('item-name').value.trim();
            const url = document.getElementById('item-url').value.trim();
            
            // Validate URL format
            let formattedUrl = url;
            if (!formattedUrl.startsWith('http://') && !formattedUrl.startsWith('https://')) {
                formattedUrl = 'https://' + formattedUrl;
            }
            
            try {
                new URL(formattedUrl); // Validate URL
            } catch {
                alert('Please enter a valid URL');
                return;
            }
            
            // Add item based on modal type
            if (currentModalType === 'link') {
                addNewLink(name, formattedUrl);
            } else if (currentModalType === 'bookmark') {
                addNewBookmark(name, formattedUrl);
            }
            
            closeModal();
        }

        /* SEARCH FUNCTIONALITY */
        // PSE WIRING: Check if Google PSE is loaded
        function isPSEAvailable() {
            return typeof google !== 'undefined' && google.search && google.search.cse;
        }

        // Perform search
        function performSearch(query) {
            if (!query.trim()) return;
            
            // Add to history if not in incognito mode
            addToHistory(query);
            
            // Check if PSE is available
            if (isPSEAvailable()) {
                // Use PSE for search
                const element = google.search.cse.element.getElement('searchresults-only0');
                if (element) {
                    element.execute(query);
                    
                    // Show PSE containers
                    document.querySelector('.pse-search-container').classList.remove('hidden');
                    document.querySelector('.pse-results-container').classList.remove('hidden');
                    
                    // Scroll to results
                    document.querySelector('.pse-results-container').scrollIntoView({ behavior: 'smooth' });
                }
            } else {
                // Fallback: open Google search in new tab
                window.open(`https://www.google.com/search?q=${encodeURIComponent(query)}`, '_blank');
            }
        }

        // Handle search form submission
        function handleSearch(e) {
            e.preventDefault();
            const query = document.getElementById('search-input').value.trim();
            performSearch(query);
        }

        /* INITIALIZATION */
        function initApp() {
            // Initialize theme
            initTheme();
            
            // Check incognito mode
            isIncognitoMode = localStorage.getItem(STORAGE_KEYS.INCOGNITO) === 'true';
            if (isIncognitoMode) {
                document.getElementById('incognito-indicator').classList.remove('hidden');
            }
            
            // Render data
            renderQuickLinks();
            renderBookmarks();
            renderHistory();
            
            // Set up event listeners
            document.querySelector('.theme-toggle').addEventListener('click', toggleTheme);
            document.querySelector('.incognito-toggle').addEventListener('click', toggleIncognitoMode);
            document.querySelector('.clear-data').addEventListener('click', clearAllData);
            
            document.getElementById('search-form').addEventListener('submit', handleSearch);
            
            document.getElementById('add-link-btn').addEventListener('click', () => openModal('link'));
            document.getElementById('add-bookmark-btn').addEventListener('click', () => openModal('bookmark'));
            
            document.getElementById('close-modal').addEventListener('click', closeModal);
            document.getElementById('cancel-modal').addEventListener('click', closeModal);
            document.getElementById('modal-form').addEventListener('submit', handleModalSubmit);
            
            // Close modal when clicking outside
            document.getElementById('modal-backdrop').addEventListener('click', (e) => {
                if (e.target === e.currentTarget) {
                    closeModal();
                }
            });
            
            // Check for PSE script periodically
            let pseCheckCount = 0;
            const pseCheckInterval = setInterval(() => {
                if (isPSEAvailable()) {
                    clearInterval(pseCheckInterval);
                    document.querySelector('.pse-search-container').classList.remove('hidden');
                }
                
                // Stop checking after 5 seconds
                if (pseCheckCount++ > 10) {
                    clearInterval(pseCheckInterval);
                }
            }, 500);
        }

        // Initialize the app when DOM is loaded
        document.addEventListener('DOMContentLoaded', initApp);
    </script>
</body>
</html>
