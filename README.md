<!DOCTYPE html>
<html lang="pt-br">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>DARK WEB PLAYER</title>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
<style>
  :root {
    --primary: #e50914;
    --primary-dark: #b20710;
    --primary-light: #f40612;
    --bg-dark: #141414;
    --bg-darker: #0a0a0a;
    --bg-light: #1f1f1f;
    --bg-sidebar: #0a0a0a;
    --text-primary: #ffffff;
    --text-secondary: #b3b3b3;
    --accent: #e50914;
    --success: #46d369;
    --error: #e87c03;
    --border: rgba(255, 255, 255, 0.1);
  }
  
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
  }
  
  body {
    background-color: var(--bg-dark);
    color: var(--text-primary);
    overflow-x: hidden;
    line-height: 1.5;
    min-height: 100vh;
    display: flex;
  }
  
  .login-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    padding: 20px;
    background: linear-gradient(135deg, var(--bg-darker) 0%, var(--bg-dark) 100%);
    text-align: center;
    width: 100%;
  }
  
  .login-box {
    background: var(--bg-light);
    border-radius: 10px;
    padding: 30px;
    width: 100%;
    max-width: 500px;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
    border: 1px solid var(--border);
  }
  
  .login-title {
    font-size: 2.2rem;
    margin-bottom: 10px;
    color: var(--text-primary);
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 2px;
  }
  
  .login-subtitle {
    font-size: 1rem;
    color: var(--text-secondary);
    margin-bottom: 30px;
  }
  
  .login-form {
    display: flex;
    flex-direction: column;
    gap: 20px;
  }
  
  .form-group {
    display: flex;
    flex-direction: column;
    gap: 8px;
    text-align: left;
  }
  
  .form-control {
    padding: 12px 15px;
    border-radius: 6px;
    border: 1px solid var(--border);
    background: rgba(255, 255, 255, 0.05);
    color: var(--text-primary);
    font-size: 1rem;
    transition: all 0.2s ease;
  }
  
  .form-control:focus {
    outline: none;
    border-color: var(--primary);
    background: rgba(255, 255, 255, 0.1);
  }
  
  .login-btn {
    padding: 12px;
    background: var(--primary);
    color: white;
    border: none;
    border-radius: 6px;
    font-size: 1rem;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.2s ease;
    margin-top: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 10px;
    min-height: 48px;
  }
  
  .login-btn:hover {
    background: var(--primary-dark);
    transform: translateY(-2px);
  }
  
  .login-btn:disabled {
    opacity: 0.7;
    cursor: not-allowed;
    transform: none;
  }
  
  .login-footer {
    margin-top: 20px;
    font-size: 0.9rem;
    color: var(--text-secondary);
  }
  
  .login-error {
    color: var(--error);
    margin-top: 10px;
    font-size: 0.9rem;
    display: none;
  }
  
  .divider {
    display: flex;
    align-items: center;
    text-align: center;
    color: var(--text-secondary);
    margin: 15px 0;
  }
  .divider::before, .divider::after {
    content: '';
    flex: 1;
    border-bottom: 1px solid var(--border);
  }
  .divider::before { margin-right: 10px; }
  .divider::after { margin-left: 10px; }
  
  .sidebar {
    width: 220px;
    background-color: var(--bg-sidebar);
    height: 100vh;
    position: fixed;
    left: 0;
    top: 0;
    padding: 20px 0;
    display: flex;
    flex-direction: column;
    border-right: 1px solid var(--border);
    z-index: 100;
    overflow-y: auto;
  }
  
  .logo {
    padding: 25px 20px 30px;
    border-bottom: 1px solid var(--border);
    margin-bottom: 20px;
  }
  
  .logo-text {
    font-size: 1.5rem;
    font-weight: bold;
    color: var(--primary);
    text-transform: uppercase;
    letter-spacing: 1px;
  }
  
  .user-info {
    padding: 0 20px;
    margin-bottom: 30px;
    display: flex;
    flex-direction: column;
    gap: 5px;
  }
  
  .user-name {
    font-size: 1.1rem;
    font-weight: 600;
  }
  
  .user-status {
    font-size: 0.8rem;
    color: var(--success);
    display: flex;
    align-items: center;
    gap: 5px;
  }
  
  .status-indicator {
    width: 8px;
    height: 8px;
    background-color: var(--success);
    border-radius: 50%;
    display: inline-block;
  }
  
  .user-expiry {
    font-size: 0.8rem;
    color: var(--text-secondary);
  }
  
  .sidebar-menu {
    flex: 1;
    display: flex;
    flex-direction: column;
    gap: 5px;
    overflow-y: auto;
  }
  
  .menu-item {
    padding: 12px 20px;
    display: flex;
    align-items: center;
    gap: 15px;
    cursor: pointer;
    transition: all 0.2s ease;
    color: var(--text-secondary);
    white-space: nowrap;
  }
  
  .menu-item:hover, .menu-item.active {
    background-color: rgba(229, 9, 20, 0.2);
    color: var(--text-primary);
  }
  
  .menu-item.active {
    border-left: 3px solid var(--primary);
  }
  
  .menu-icon {
    width: 20px;
    height: 20px;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
  }
  
  .main-content {
    margin-left: 220px;
    flex: 1;
    padding: 30px;
    min-height: 100vh;
    overflow-x: hidden;
  }
  
  .featured-container {
    position: relative;
    height: 500px;
    border-radius: 10px;
    overflow: hidden;
    margin-bottom: 40px;
  }
  
  .featured-backdrop {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    object-fit: cover;
    filter: brightness(0.4);
    z-index: 1;
  }
  
  .featured-content {
    position: relative;
    z-index: 2;
    padding: 50px;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    background: linear-gradient(to top, rgba(0,0,0,0.9) 0%, rgba(0,0,0,0) 100%);
  }
  
  .featured-title {
    font-size: 3.5rem;
    font-weight: bold;
    margin-bottom: 15px;
    max-width: 70%;
  }
  
  .featured-info {
    display: flex;
    gap: 20px;
    margin-bottom: 20px;
    align-items: center;
    flex-wrap: wrap;
  }
  
  .featured-genre {
    display: flex;
    gap: 10px;
    flex-wrap: wrap;
  }
  
  .genre-tag {
    background-color: rgba(255, 255, 255, 0.1);
    padding: 3px 10px;
    border-radius: 4px;
    font-size: 0.9rem;
  }
  
  .featured-actions {
    display: flex;
    gap: 15px;
    flex-wrap: wrap;
  }
  
  .play-btn {
    background-color: var(--primary);
    color: white;
    border: none;
    padding: 10px 25px;
    border-radius: 5px;
    font-weight: 600;
    cursor: pointer;
    display: flex;
    align-items: center;
    gap: 8px;
    transition: all 0.2s ease;
  }
  
  .play-btn:hover {
    background-color: var(--primary-dark);
  }
  
  .more-info-btn {
    background-color: rgba(255, 255, 255, 0.2);
    color: white;
    border: 1px solid rgba(255, 255, 255, 0.5);
    padding: 10px 25px;
    border-radius: 5px;
    font-weight: 600;
    cursor: pointer;
    display: flex;
    align-items: center;
    gap: 8px;
    transition: all 0.2s ease;
  }
  
  .more-info-btn:hover {
    background-color: rgba(255, 255, 255, 0.3);
  }
  
  .section {
    margin-bottom: 40px;
  }
  
  .section-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
    flex-wrap: wrap;
    gap: 10px;
  }
  
  .section-title {
    font-size: 1.8rem;
    font-weight: bold;
  }
  
  .section-link {
    color: var(--text-secondary);
    text-decoration: none;
    font-size: 0.9rem;
    display: flex;
    align-items: center;
    gap: 5px;
    transition: color 0.2s ease;
    cursor: pointer;
  }
  
  .section-link:hover {
    color: var(--text-primary);
  }
  
  .content-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
    gap: 20px;
  }
  
  .content-card {
    background-color: var(--bg-light);
    border-radius: 5px;
    overflow: hidden;
    transition: all 0.2s ease;
    cursor: pointer;
    border: 1px solid var(--border);
  }
  
  .content-card:hover {
    transform: scale(1.03);
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
    border-color: var(--primary);
  }
  
  .content-poster-container {
    position: relative;
  }
  
  .content-poster {
    width: 100%;
    height: 300px;
    object-fit: cover;
    display: block;
  }
  
  .content-info {
    padding: 15px;
  }
  
  .content-title {
    font-weight: 600;
    margin-bottom: 5px;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }
  
  .content-meta {
    display: flex;
    justify-content: space-between;
    font-size: 0.8rem;
    color: var(--text-secondary);
  }
  
  .favorite-btn {
    position: absolute;
    top: 10px;
    right: 10px;
    background: rgba(0, 0, 0, 0.7);
    border: none;
    border-radius: 50%;
    width: 36px;
    height: 36px;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    transition: all 0.2s ease;
    z-index: 2;
  }
  
  .favorite-btn:hover {
    background: rgba(0, 0, 0, 0.9);
    transform: scale(1.1);
  }
  
  .player-container {
    display: none;
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: var(--bg-darker);
    z-index: 1000;
    flex-direction: column;
    padding: 20px;
    overflow-y: auto;
  }
  
  .player-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
  }
  
  .player-title {
    font-size: 1.5rem;
    font-weight: bold;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    max-width: 70%;
  }
  
  .player-close {
    background: none;
    border: none;
    color: var(--text-secondary);
    font-size: 1.5rem;
    cursor: pointer;
    flex-shrink: 0;
  }
  
  .player-close:hover {
    color: var(--text-primary);
  }
  
  video {
    width: 100%;
    max-height: 70vh;
    background: black;
    border-radius: 8px;
  }
  
  .player-info {
    display: flex;
    align-items: center;
    gap: 15px;
    margin-top: 15px;
    padding: 15px;
    background: var(--bg-light);
    border-radius: 8px;
    flex-wrap: wrap;
  }
  
  .player-poster {
    width: 100px;
    height: 150px;
    object-fit: cover;
    border-radius: 5px;
  }
  
  .player-details {
    flex: 1;
    min-width: 200px;
  }
  
  .player-content-title {
    font-size: 1.5rem;
    font-weight: bold;
    margin-bottom: 5px;
  }
  
  .player-meta {
    display: flex;
    gap: 15px;
    color: var(--text-secondary);
    font-size: 0.9rem;
    margin-bottom: 10px;
    flex-wrap: wrap;
  }
  
  .player-description {
    color: var(--text-secondary);
    font-size: 0.9rem;
    line-height: 1.4;
  }
  
  .player-controls {
    display: flex;
    gap: 10px;
    margin-top: 20px;
    flex-wrap: wrap;
  }
  
  .player-controls button {
    padding: 10px 20px;
    background: var(--primary);
    color: white;
    border: none;
    border-radius: 5px;
    font-weight: 600;
    cursor: pointer;
    display: flex;
    align-items: center;
    gap: 8px;
    transition: all 0.2s ease;
  }
  
  .player-controls button:hover {
    background: var(--primary-dark);
  }
  
  .player-episodes {
    margin-top: 20px;
    padding: 15px;
    background: var(--bg-light);
    border-radius: 8px;
  }
  
  .player-episodes-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 15px;
    flex-wrap: wrap;
    gap: 10px;
  }
  
  .player-episodes-header h3 {
    margin: 0;
    font-size: 1.2rem;
  }
  
  .player-episodes-list {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
    gap: 10px;
    max-height: 250px;
    overflow-y: auto;
  }
  
  .player-episode-item {
    background: rgba(255, 255, 255, 0.05);
    border-radius: 5px;
    padding: 10px;
    cursor: pointer;
    transition: all 0.2s ease;
  }
  
  .player-episode-item:hover {
    background: rgba(229, 9, 20, 0.2);
  }
  
  .player-episode-item.current {
    background: rgba(229, 9, 20, 0.4);
  }
  
  .player-episode-number {
    font-weight: 600;
    margin-bottom: 5px;
  }
  
  .player-episode-title {
    font-size: 0.9rem;
    color: var(--text-secondary);
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }
  
  .content-details-modal {
    display: none;
    position: fixed;
    z-index: 1001;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    overflow: auto;
    background-color: rgba(0, 0, 0, 0.9);
  }
  
  .modal-content {
    background-color: var(--bg-light);
    margin: 5% auto;
    padding: 20px;
    border: 1px solid var(--border);
    width: 90%;
    max-width: 800px;
    border-radius: 10px;
    position: relative;
  }
  
  .close-modal {
    position: absolute;
    right: 20px;
    top: 15px;
    color: var(--text-secondary);
    font-size: 28px;
    font-weight: bold;
    cursor: pointer;
    z-index: 10;
  }
  
  .close-modal:hover {
    color: var(--text-primary);
  }
  
  .modal-body {
    display: flex;
    gap: 20px;
  }
  
  .modal-poster {
    flex-shrink: 0;
  }
  
  .modal-poster img {
    width: 200px;
    height: 300px;
    object-fit: cover;
    border-radius: 5px;
  }
  
  .modal-info {
    flex: 1;
  }
  
  .modal-title {
    font-size: 1.8rem;
    font-weight: bold;
    margin-bottom: 10px;
  }
  
  .modal-meta {
    display: flex;
    gap: 15px;
    margin: 10px 0;
    flex-wrap: wrap;
  }
  
  .modal-genres {
    display: flex;
    gap: 10px;
    flex-wrap: wrap;
  }
  
  .modal-description {
    color: var(--text-secondary);
    font-size: 0.9rem;
    line-height: 1.4;
    margin: 15px 0;
  }
  
  .modal-actions {
    margin-top: 20px;
    display: flex;
    gap: 15px;
    flex-wrap: wrap;
  }
  
  .series-episodes-modal {
    display: none;
    position: fixed;
    z-index: 1002;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    overflow: auto;
    background-color: rgba(0, 0, 0, 0.9);
  }
  
  .series-modal-content {
    background-color: var(--bg-light);
    margin: 3% auto;
    padding: 20px;
    border: 1px solid var(--border);
    width: 90%;
    max-width: 1000px;
    border-radius: 10px;
    position: relative;
  }
  
  .seasons-container {
    margin-top: 20px;
  }
  
  .season-header {
    background: rgba(255, 255, 255, 0.05);
    border-radius: 5px;
    padding: 12px 15px;
    margin: 10px 0;
    cursor: pointer;
    display: flex;
    justify-content: space-between;
    align-items: center;
    transition: background 0.2s ease;
  }
  
  .season-header:hover {
    background: rgba(255, 255, 255, 0.1);
  }
  
  .season-header h3 {
    margin: 0;
    font-size: 1.1rem;
  }
  
  .season-header i {
    transition: transform 0.3s ease;
  }
  
  .season-header.expanded i {
    transform: rotate(180deg);
  }
  
  .episodes-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
    gap: 15px;
    margin-top: 15px;
    padding-left: 10px;
  }
  
  .episode-card {
    background: rgba(255, 255, 255, 0.05);
    border-radius: 8px;
    padding: 12px;
    cursor: pointer;
    transition: all 0.2s ease;
    text-align: center;
    border: 1px solid transparent;
  }
  
  .episode-card:hover {
    background: rgba(229, 9, 20, 0.2);
    transform: translateY(-3px);
    border-color: var(--primary);
  }
  
  .episode-number {
    font-weight: 600;
    margin-bottom: 5px;
    color: var(--primary);
  }
  
  .episode-title {
    font-size: 0.9rem;
    color: var(--text-secondary);
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }
  
  .modal {
    display: none;
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 0, 0, 0.8);
    z-index: 2000;
    align-items: center;
    justify-content: center;
  }
  
  .modal .modal-inner {
    background: var(--bg-light);
    border-radius: 8px;
    width: 90%;
    max-width: 400px;
    padding: 20px;
  }
  
  .modal-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 15px;
  }
  
  .modal-header h3 {
    font-size: 1.2rem;
    font-weight: bold;
    color: var(--text-primary);
    margin: 0;
  }
  
  .modal-close {
    background: none;
    border: none;
    color: var(--text-secondary);
    font-size: 1.5rem;
    cursor: pointer;
  }
  
  .quality-options {
    display: flex;
    flex-direction: column;
    gap: 8px;
  }
  
  .quality-option {
    padding: 12px;
    background: rgba(255, 255, 255, 0.1);
    border-radius: 6px;
    cursor: pointer;
    transition: background 0.2s;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  
  .quality-option:hover {
    background: rgba(255, 255, 255, 0.2);
  }
  
  .quality-name {
    font-weight: 600;
  }
  
  .quality-resolution {
    color: var(--text-secondary);
    font-size: 0.8rem;
  }
  
  .category-selector {
    margin-bottom: 20px;
    display: flex;
    gap: 10px;
    flex-wrap: wrap;
  }
  
  .category-btn {
    padding: 8px 15px;
    background: rgba(255, 255, 255, 0.1);
    border: 1px solid var(--border);
    border-radius: 5px;
    color: var(--text-primary);
    cursor: pointer;
    transition: all 0.2s ease;
    font-size: 0.9rem;
  }
  
  .category-btn:hover {
    background: rgba(229, 9, 20, 0.2);
    border-color: var(--primary);
  }
  
  .category-btn.active {
    background: var(--primary);
    border-color: var(--primary);
  }
  
  #live-cat-select {
    background-color: #f0f0f0;
    color: #000000;
    border: 1px solid var(--border);
    padding: 8px 12px;
    border-radius: 6px;
    font-weight: 500;
  }
  
  #live-cat-select option {
    background-color: #ffffff;
    color: #000000;
  }
  
  .loading {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 200px;
    width: 100%;
    color: var(--text-secondary);
    font-size: 1rem;
  }
  
  .spinner {
    width: 50px;
    height: 50px;
    border: 4px solid rgba(229, 9, 20, 0.2);
    border-top-color: var(--primary);
    border-radius: 50%;
    animation: spin 1s linear infinite;
  }
  
  .spinner-small {
    width: 20px;
    height: 20px;
    border: 3px solid rgba(255, 255, 255, 0.3);
    border-top-color: white;
    border-radius: 50%;
    animation: spin 0.8s linear infinite;
  }
  
  @keyframes spin {
    to { transform: rotate(360deg); }
  }
  
  .footer {
    margin-top: 50px;
    padding-top: 20px;
    border-top: 1px solid var(--border);
    text-align: center;
    color: var(--text-secondary);
    font-size: 0.9rem;
  }
  
  .menu-toggle {
    display: none;
    position: fixed;
    top: 15px;
    left: 15px;
    z-index: 101;
    background: var(--primary);
    border: none;
    border-radius: 5px;
    width: 40px;
    height: 40px;
    justify-content: center;
    align-items: center;
    cursor: pointer;
    margin-top: 10px;
  }
  
  .menu-toggle svg {
    width: 24px;
    height: 24px;
    color: white;
  }
  
  .search-container {
    margin-bottom: 25px;
  }
  
  .search-input-wrap {
    position: relative;
  }
  
  .search-input-wrap i {
    position: absolute;
    left: 15px;
    top: 50%;
    transform: translateY(-50%);
    color: var(--text-secondary);
  }
  
  .search-input-wrap .form-control {
    padding-left: 45px;
  }
  
  @media (max-width: 1200px) {
    .featured-title { font-size: 2.5rem; }
    .content-grid { grid-template-columns: repeat(auto-fill, minmax(170px, 1fr)); }
  }
  @media (max-width: 992px) {
    .sidebar { width: 180px; }
    .main-content { margin-left: 180px; }
    .featured-title { font-size: 2rem; max-width: 90%; }
    .content-grid { grid-template-columns: repeat(auto-fill, minmax(150px, 1fr)); }
  }
  @media (max-width: 768px) {
    .sidebar { width: 220px; transform: translateX(-100%); transition: tr
<html>
  
</html>
