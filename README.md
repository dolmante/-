<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>しがないライター</title>
    <style>
        :root {
            --yahoo-red: #ff0033;
            --yahoo-blue: #185ad8;
            --bg-gray: #f2f2f2;
            --border-color: #e0e0e0;
            --text-main: #333333;
            --text-sub: #777777;
        }

        body {
            font-family: "Hiragino Kaku Gothic ProN", "Helvetica Neue", Arial, sans-serif;
            background-color: var(--bg-gray);
            color: var(--text-main);
            margin: 0;
            padding: 0;
        }

        /* 赤いヘッダー */
        header {
            background-color: #ffffff;
            border-bottom: 2px solid var(--yahoo-red);
            padding: 15px 20px;
            display: flex;
            align-items: center;
            justify-content: space-between;
        }

        .header-logo {
            font-size: 1.4rem;
            font-weight: bold;
            color: var(--yahoo-red);
            text-decoration: none;
            display: flex;
            align-items: center;
            gap: 5px;
        }

        /* メインレイアウト */
        .main-container {
            max-width: 950px;
            margin: 20px auto;
            padding: 0 15px;
            display: grid;
            grid-template-columns: 1fr 300px;
            gap: 20px;
        }

        /* スマホ対応 */
        @media (max-width: 768px) {
            .main-container {
                grid-template-columns: 1fr;
            }
            .sidebar {
                display: none;
            }
        }

        /* メインニュースセクション */
        .news-section {
            background-color: #ffffff;
            border: 1px solid var(--border-color);
            border-radius: 4px;
            padding: 20px;
            min-height: 400px;
        }

        /* ヤフー風マルチタブメニュー */
        .tab-menu {
            display: flex;
            border-bottom: 2px solid #333;
            margin-bottom: 15px;
            padding: 0;
            list-style: none;
            gap: 4px;
            overflow-x: auto;
        }

        .tab-item {
            padding: 8px 16px;
            font-weight: bold;
            font-size: 0.9rem;
            cursor: pointer;
            background-color: #e0e0e0;
            color: #333;
            border-radius: 4px 4px 0 0;
            transition: all 0.2s;
            white-space: nowrap;
        }

        .tab-item:hover {
            background-color: #d0d0d0;
        }

        /* アクティブ（選択中）のタブ */
        .tab-item.active {
            background-color: #333;
            color: #fff;
        }

        /* --- 一覧表示 --- */
        .topics-list {
            list-style: none;
            padding: 0;
            margin: 0;
        }

        .topic-item {
            border-bottom: 1px dotted var(--border-color);
            padding: 12px 5px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-size: 0.95rem;
        }

        .topic-item:hover {
            background-color: #f9f9f9;
        }

        .topic-left {
            display: flex;
            align-items: center;
            gap: 10px;
            flex-grow: 1;
        }

        .topic-dot {
            color: var(--yahoo-blue);
            font-size: 1.2rem;
            line-height: 1;
        }

        /* ジャンルバッジ（見出しの前に「[スポーツ]」などを表示） */
        .topic-genre {
            font-size: 0.75rem;
            font-weight: bold;
            color: #fff;
            padding: 2px 6px;
            border-radius: 3px;
            white-space: nowrap;
            display: inline-block;
        }

        /* ジャンルごとのバッジ色分け */
        .genre-entertainment { background-color: #e84393; } /* 芸能: ピンク */
        .genre-sports { background-color: #0984e3; }        /* スポーツ: 青 */
        .genre-movie { background-color: #6c5ce7; }         /* 映画: 紫 */

        .topic-title {
            color: var(--yahoo-blue);
            text-decoration: none;
            font-weight: bold;
            cursor: pointer;
            word-break: break-all;
        }

        .topic-title:hover {
            text-decoration: underline;
        }

        .topic-time {
            font-size: 0.8rem;
            color: var(--text-sub);
            white-space: nowrap;
            margin-left: 10px;
        }

        /* リストが空の時のメッセージ */
        .empty-message {
            color: var(--text-sub);
            text-align: center;
            padding: 40px 0;
            font-size: 0.95rem;
        }

        /* --- 記事詳細表示 --- */
        .article-view {
            display: none;
        }

        .article-title {
            font-size: 1.5rem;
            font-weight: bold;
            line-height: 1.4;
            margin-top: 5px;
            margin-bottom: 10px;
            color: #000;
        }

        .article-meta {
            font-size: 0.85rem;
            color: var(--text-sub);
            margin-bottom: 20px;
            border-bottom: 1px solid var(--border-color);
            padding-bottom: 10px;
        }

        .article-image-container {
            width: 100%;
            max-height: 400px;
            overflow: hidden;
            border-radius: 4px;
            margin-bottom: 20px;
            text-align: center;
            background-color: #f5f5f5;
        }

        .article-image {
            max-width: 100%;
            max-height: 400px;
            object-fit: contain;
        }

        .article-body {
            font-size: 1.05rem;
            line-height: 1.8;
            color: #222;
            white-space: pre-wrap;
            margin-bottom: 30px;
            word-break: break-all;
        }

        .article-actions {
            border-top: 1px solid var(--border-color);
            padding-top: 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .back-btn {
            background-color: #e0e0e0;
            color: #333;
            border: none;
            padding: 8px 16px;
            border-radius: 4px;
            font-size: 0.9rem;
            font-weight: bold;
            cursor: pointer;
        }

        .back-btn:hover {
            background-color: #d0d0d0;
        }

        .delete-single-btn {
            background-color: #e74c3c;
            color: white;
            border: none;
            padding: 8px 16px;
            border-radius: 4px;
            cursor: pointer;
            font-size: 0.85rem;
            font-weight: bold;
        }

        .delete-single-btn:hover {
            background-color: #c0392b;
        }

        /* --- 投稿フォーム --- */
        .sidebar {
            display: flex;
            flex-direction: column;
            gap: 20px;
        }

        .form-card {
            background-color: #ffffff;
            border: 1px solid var(--border-color);
            border-radius: 4px;
            padding: 20px;
        }

        .form-title {
            font-size: 1rem;
            font-weight: bold;
            border-bottom: 2px solid var(--yahoo-red);
            padding-bottom: 8px;
            margin-bottom: 15px;
        }

        .form-group {
            margin-bottom: 12px;
        }

        label {
            display: block;
            font-size: 0.8rem;
            font-weight: bold;
            margin-bottom: 4px;
        }

        input[type="text"], input[type="file"], select, textarea {
            width: 100%;
            padding: 8px;
            border: 1px solid #ccc;
            border-radius: 4px;
            box-sizing: border-box;
            font-size: 0.9rem;
        }

        input[type="file"] {
            background-color: #fafafa;
            cursor: pointer;
        }

        select {
            background-color: #fff;
            cursor: pointer;
        }

        textarea {
            height: 100px;
            resize: none;
        }

        button.submit-btn {
            width: 100%;
            background-color: var(--yahoo-red);
            color: white;
            border: none;
            padding: 10px;
            border-radius: 4px;
            font-size: 0.9rem;
            font-weight: bold;
            cursor: pointer;
        }

        button.submit-btn:hover {
            background-color: #cc002c;
        }

        .clear-btn {
            background: none;
            border: none;
            color: var(--text-sub);
            font-size: 0.8rem;
            cursor: pointer;
            text-decoration: underline;
            padding: 0;
            text-align: right;
            display: block;
            margin-top: 10px;
        }
    </style>
</head>
<body>

<!-- ヘッダー -->
<header>
    <a href="#" class="header-logo" onclick="switchGenre('all'); return false;">しがないライター</a>
</header>

<div class="main-container">
    <!-- 左側：ニュースセクション -->
    <main class="news-section">
        <!-- ヤフー風ジャンル切り替えタブ -->
        <ul class="tab-menu" id="tabMenu">
            <li class="tab-item active" onclick="switchGenre('all')" id="tab-all">すべて</li>
            <li class="tab-item" onclick="switchGenre('entertainment')" id="tab-entertainment">芸能</li>
            <li class="tab-item" onclick="switchGenre('sports')" id="tab-sports">スポーツ</li>
            <li class="tab-item" onclick="switchGenre('movie')" id="tab-movie">映画</li>
        </ul>

        <!-- 状態1: ニュース一覧表示 -->
        <div id="listView">
            <ul class="topics-list" id="topicsList">
                <!-- 投稿がここに並びます -->
            </ul>
        </div>

        <!-- 状態2: 記事詳細表示 -->
        <div id="articleView" class="article-view">
            <h1 class="article-title" id="artTitle">見出し</h1>
            <div class="article-meta" id="artMeta">配信日時</div>
            
            <div class="article-image-container" id="artImageContainer">
                <img class="article-image" id="artImage" src="" alt="ニュース画像">
            </div>

            <div class="article-body" id="artBody">
                本文
            </div>

            <div class="article-actions">
                <button class="back-btn" onclick="showListView()">← トピックス一覧へ戻る</button>
                <button class="delete-single-btn" id="deleteSingleBtn">この記事をボツにする (管理者)</button>
            </div>
        </div>
    </main>

    <!-- 右側：投稿フォーム -->
    <aside class="sidebar">
        <div class="form-card">
            <div class="form-title">トピックスを投稿する</div>
            <form id="bbsForm">
                <div class="form-group">
                    <label for="nameInput">執筆者 (ニックネーム)</label>
                    <input type="text" id="nameInput" placeholder="しがないライター" maxlength="15">
                </div>
                <div class="form-group">
                    <!-- ジャンル選択：デフォルトを「指定なし」に変更 -->
                    <label for="genreSelect">掲載ジャンル</label>
                    <select id="genreSelect">
                        <option value="none">指定なし</option>
                        <option value="entertainment">芸能</option>
                        <option value="sports">スポーツ</option>
                        <option value="movie">映画</option>
                    </select>
                </div>
                <div class="form-group">
                    <label for="titleInput">見出し (最大30文字)</label>
                    <input type="text" id="titleInput" placeholder="記事の短い見出し" maxlength="30" required>
                </div>
                <div class="form-group">
                    <label for="imageFileInput">画像をアップロード (任意)</label>
                    <input type="file" id="imageFileInput" accept="image/*">
                </div>
                <div class="form-group">
                    <label for="contentInput">記事の本文</label>
                    <textarea id="contentInput" placeholder="詳しい内容をここに書き込んでください" required></textarea>
                </div>
                <button type="submit" class="submit-btn">トピックスを掲載</button>
            </form>
            <button class="clear-btn" id="clearBtn">【管理者専用】すべての記事をボツにする</button>
        </div>
    </aside>
</div>

<script>
    const ADMIN_PASSWORD = "shiganai2026"; // 管理者用パスワード

    const STORAGE_KEY = 'yahoo_bbs_posts';
    let posts = [];
    let currentOpenPostId = null;
    let currentGenre = 'all'; // 現在選択されている表示ジャンル ('all', 'entertainment', 'sports', 'movie')

    // 初期化
    window.addEventListener('DOMContentLoaded', () => {
        const savedPosts = localStorage.getItem(STORAGE_KEY);
        if (savedPosts) {
            posts = JSON.parse(savedPosts);
        } else {
            // ジャンルごとの初期サンプルデータ
            posts = [
                {
                    id: 1,
                    name: "編集部",
                    genre: "none", // 指定なし
                    title: "【重要】新機能「ジャンル指定なし」が追加されました",
                    image: "",
                    content: "掲載時にジャンルを「指定なし」にすると、一覧にバッジを表示せずシンプルな見た目で投稿ができます。\n\nもちろん「すべて（ぜんぶ）」のトピックス一覧にはきれいに格納されるので、気軽な雑記やニュースはこちらでどんどん投稿してみてください！",
                    time: "たった今"
                },
                {
                    id: 2,
                    name: "芸能記者",
                    genre: "entertainment",
                    title: "【芸能】しがないライター、ついにマルチカテゴリ対応へ！",
                    image: "",
                    content: "芸能界でも噂されていた『しがないライター』のカテゴリ仕分けがついに実現しました。\n\nこれにより、お目当ての業界スクープをさらに素早くチェックすることが可能に。関係者は「これで朝の巡回が楽になる」と大喜びの様子です。",
                    time: "5分前"
                }
            ];
        }
        renderPosts();
        showListView();
    });

    // フォーム送信
    document.getElementById('bbsForm').addEventListener('submit', function(e) {
        e.preventDefault();

        const nameInput = document.getElementById('nameInput');
        const genreSelect = document.getElementById('genreSelect');
        const titleInput = document.getElementById('titleInput');
        const fileInput = document.getElementById('imageFileInput');
        const contentInput = document.getElementById('contentInput');

        const name = nameInput.value.trim() || 'しがないライター';
        const genre = genreSelect.value;
        const title = titleInput.value.trim();
        const content = contentInput.value.trim();

        if (!title || !content) return;

        const now = new Date();
        const timeString = `${(now.getMonth()+1)}/${now.getDate()} ${(now.getHours())}:${now.getMinutes().toString().padStart(2, '0')}`;

        const file = fileInput.files[0];
        if (file) {
            const reader = new FileReader();
            reader.onload = function(event) {
                const imageDataUrl = event.target.result;
                addNewPost(name, genre, title, imageDataUrl, content, timeString);
            };
            reader.readAsDataURL(file);
        } else {
            addNewPost(name, genre, title, '', content, timeString);
        }

        // フォームクリア
        titleInput.value = '';
        fileInput.value = '';
        contentInput.value = '';
    });

    function addNewPost(name, genre, title, imageSrc, content, timeString) {
        const newPost = {
            id: Date.now(),
            name: name,
            genre: genre, // 'none', 'entertainment', 'sports', 'movie'
            title: title,
            image: imageSrc,
            content: content,
            time: timeString
        };

        posts.unshift(newPost);
        savePosts();
        renderPosts();
        
        // 投稿が「指定なし(none)」なら「すべて(all)」タブへ。それ以外なら選ばれたジャンルへ自動切り替え
        if (genre === 'none') {
            switchGenre('all');
        } else {
            switchGenre(genre);
        }
    }

    function savePosts() {
        try {
            localStorage.setItem(STORAGE_KEY, JSON.stringify(posts));
        } catch (e) {
            alert("画像データのサイズが大きすぎるため保存できませんでした。少し小さめの画像をお試しください。");
        }
    }

    // ジャンルの日本語名とバッジクラスを取得
    function getGenreInfo(genreCode) {
        switch(genreCode) {
            case 'entertainment':
                return { name: '芸能', class: 'genre-entertainment', showBadge: true };
            case 'sports':
                return { name: 'スポーツ', class: 'genre-sports', showBadge: true };
            case 'movie':
                return { name: '映画', class: 'genre-movie', showBadge: true };
            default:
                return { name: '指定なし', class: '', showBadge: false };
        }
    }

    // トピックス一覧の描画
    function renderPosts() {
        const list = document.getElementById('topicsList');
        list.innerHTML = '';

        // 現在選択されているジャンルにフィルタリング
        const filteredPosts = currentGenre === 'all' 
            ? posts 
            : posts.filter(post => post.genre === currentGenre);

        if (filteredPosts.length === 0) {
            list.innerHTML = `<div class="empty-message">このジャンルにはまだトピックスがありません。</div>`;
            return;
        }

        filteredPosts.forEach(post => {
            const genreInfo = getGenreInfo(post.genre);
            const li = document.createElement('li');
            li.className = 'topic-item';

            // バッジの表示有無を判定してHTMLを組み立て
            const badgeHTML = genreInfo.showBadge 
                ? `<span class="topic-genre ${genreInfo.class}">${genreInfo.name}</span>` 
                : '';

            li.innerHTML = `
                <div class="topic-left">
                    <span class="topic-dot">•</span>
                    ${badgeHTML}
                    <span class="topic-title" onclick="openNews(${post.id})">${escapeHTML(post.title)}</span>
                </div>
                <span class="topic-time">${post.time}</span>
            `;
            list.appendChild(li);
        });
    }

    // ジャンルタブ切り替え
    window.switchGenre = function(genre) {
        currentGenre = genre;

        const tabs = document.querySelectorAll('.tab-menu .tab-item');
        tabs.forEach(tab => tab.classList.remove('active'));
        document.getElementById(`tab-${genre}`).classList.add('active');

        showListView();
        renderPosts();
    };

    // 一覧画面を表示
    function showListView() {
        document.getElementById('listView').style.display = 'block';
        document.getElementById('articleView').style.display = 'none';
        document.getElementById('tabMenu').style.display = 'flex';
        currentOpenPostId = null;
    }

    // 記事詳細を表示
    window.openNews = function(id) {
        const post = posts.find(p => p.id === id);
        if (!post) return;

        currentOpenPostId = id;

        document.getElementById('tabMenu').style.display = 'none';

        const genreInfo = getGenreInfo(post.genre);
        const genreLabel = genreInfo.showBadge ? ` - ジャンル: ${genreInfo.name}` : '';

        document.getElementById('artTitle').innerText = post.title;
        document.getElementById('artMeta').innerText = `${post.time}配信${genreLabel} - 著者: ${post.name}`;
        document.getElementById('artBody').innerText = post.content;

        const imgContainer = document.getElementById('artImageContainer');
        const img = document.getElementById('artImage');
        if (post.image) {
            img.src = post.image;
            imgContainer.style.display = 'block';
        } else {
            img.src = '';
            imgContainer.style.display = 'none';
        }

        document.getElementById('listView').style.display = 'none';
        document.getElementById('articleView').style.display = 'block';

        window.scrollTo({ top: 0, behavior: 'smooth' });
    };

    // パスワード照合
    function checkAdmin() {
        const password = prompt('管理者のパスワードを入力してください:');
        if (password === ADMIN_PASSWORD) {
            return true;
        } else {
            alert('パスワードが違います。');
            return false;
        }
    }

    // この記事だけボツにする
    document.getElementById('deleteSingleBtn').addEventListener('click', () => {
        if (currentOpenPostId) {
            if (checkAdmin()) {
                posts = posts.filter(post => post.id !== currentOpenPostId);
                savePosts();
                renderPosts();
                showListView();
                alert('記事をボツにしました。');
            }
        }
    });

    // すべて削除する
    document.getElementById('clearBtn').addEventListener('click', () => {
        if (checkAdmin()) {
            if (confirm('本当にすべての記事をボツ（削除）にしますか？')) {
                posts = [];
                savePosts();
                renderPosts();
                showListView();
                alert('すべての記事をボツにしました。');
            }
        }
    });

    function escapeHTML(str) {
        return str.replace(/[&<>"']/g, function(match) {
            const escape = {
                '&': '&amp;',
                '<': '&lt;',
                '>': '&gt;',
                '"': '&quot;',
                "'": '&#39;'
            };
            return escape[match];
        });
    }
</script>

</body>
</html>
