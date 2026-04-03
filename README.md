# -
지우 포카 
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>지우 포카</title>
    
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@400;700&display=swap" rel="stylesheet">

    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { font-family: 'Noto Sans KR', sans-serif; background-color: #f8f9fa; color: #333; line-height: 1.6; }
        .container { max-width: 500px; margin: 0 auto; min-height: 100vh; background-color: #fff; box-shadow: 0 0 20px rgba(0,0,0,0.05); position: relative; }
        .header { display: flex; justify-content: space-between; align-items: center; padding: 15px 20px; background-color: #fff; border-bottom: 1px solid #eee; position: sticky; top: 0; z-index: 1000; }
        .logo { font-size: 22px; font-weight: 700; color: #222; cursor: pointer; }
        .icon-btn { background: none; border: none; cursor: pointer; color: #444; font-size: 1.3rem; padding: 5px; }
        .search-bar-container { display: none; padding: 15px 20px; background: #fff; border-bottom: 1px solid #eee; }
        .search-input-wrapper { display: flex; background: #f1f3f5; padding: 8px 15px; border-radius: 20px; align-items: center; }
        .search-input-wrapper input { flex: 1; border: none; background: none; outline: none; margin-left: 10px; font-size: 0.95rem; }
        .toc-menu { display: none; background-color: #fff; padding: 20px; border-bottom: 1px solid #eee; }
        .sub-items { list-style: none; border-left: 2px solid #007bff; padding-left: 15px; }
        .sub-items li { padding: 12px 0; cursor: pointer; font-size: 1.1rem; font-weight: 500; border-bottom: 1px solid #fafafa; }
        .main-content { padding: 20px; min-height: 80vh; }
        #result-area { display: none; }
        .album-title { font-size: 1.5rem; font-weight: 700; color: #007bff; margin-bottom: 15px; }
        .tab-container { display: flex; flex-wrap: wrap; gap: 6px; margin-bottom: 15px; }
        .tab-btn { min-width: 65px; padding: 7px 10px; border: 1px solid #eee; background: #f9f9f9; border-radius: 8px; cursor: pointer; font-size: 0.68rem; font-weight: 500; color: #666; text-align: center; }
        .tab-btn.active { background: #007bff; color: #fff; border-color: #007bff; }
        .sub-filter-group { background: #f1f3f5; padding: 12px; border-radius: 10px; margin-bottom: 15px; }
        .filter-label { font-size: 0.75rem; color: #888; margin-bottom: 8px; font-weight: 700; }
        .filter-btns { display: flex; flex-wrap: wrap; gap: 6px; }
        .f-btn { flex: 1; min-width: 80px; padding: 6px; border-radius: 6px; border: 1px solid #ddd; background: #fff; font-size: 0.7rem; cursor: pointer; color: #555; }
        .f-btn.active { background: #333; color: #fff; border-color: #333; }
        .card-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 12px; }
        .card-item { aspect-ratio: 5.5 / 8.5; background: #fff; border-radius: 10px; border: 1px solid #eee; text-align: center; padding: 10px; display: flex; flex-direction: column; align-items: center; justify-content: center; }
        .card-name { font-size: 0.82rem; font-weight: 700; margin-top: 10px; }
        .welcome { text-align: center; margin-top: 100px; color: #ccc; }
    </style>
</head>
<body>

<div class="container">
    <header class="header">
        <button id="menu-toggle" class="icon-btn"><i class="fas fa-list-ul"></i></button>
        <h1 class="logo" id="main-logo">지우 포카</h1>
        <button id="search-toggle" class="icon-btn"><i class="fas fa-search"></i></button>
    </header>

    <div id="search-bar" class="search-bar-container">
        <div class="search-input-wrapper">
            <i class="fas fa-search" style="color: #adb5bd;"></i>
            <input type="text" id="pc-search-input" placeholder="포카 이름 검색...">
        </div>
    </div>

    <nav id="toc-menu" class="toc-menu">
        <ul class="sub-items">
            <li onclick="selectAlbum('전체')">전체</li>
            <li onclick="selectAlbum('The Chase')">The Chase</li>
            <li onclick="selectAlbum('STYLE')">STYLE</li>
            <li onclick="selectAlbum('FOCUS')">FOCUS</li>
            <li onclick="selectAlbum('RUDE!')">RUDE!</li>
            <li onclick="selectAlbum('유닛 포카')">유닛 포카</li>
            <li onclick="selectAlbum('MD 포카')">MD 포카</li>
            <li onclick="selectAlbum('기타')">기타</li>
        </ul>
    </nav>

    <main class="main-content">
        <div id="welcome-view" class="welcome">
            <i class="fas fa-search" style="font-size:3rem; display:block; margin-bottom:15px;"></i>
            <p>목차를 눌러 포토카드를 확인하세요.</p>
        </div>

        <div id="result-area">
            <h2 id="display-album-name" class="album-title">Album Name</h2>
            <div id="tab-wrapper" class="tab-container"></div>
            
            <div id="version-filter" class="sub-filter-group" style="display:none;">
                <p class="filter-label">버전 선택</p>
                <div id="version-btn-wrapper" class="filter-btns"></div>
            </div>

            <div id="fansign-filter" class="sub-filter-group" style="display:none;">
                <p class="filter-label">유형 선택</p>
                <div id="fansign-btn-wrapper" class="filter-btns"></div>
            </div>

            <div id="tab-label" style="font-weight: 700; margin-bottom: 10px; font-size: 0.9rem; color: #444;">[전체] 목록</div>
            <div class="card-grid" id="pc-list"></div>
        </div>
    </main>
</div>

<script>
    const pcData = []; 

    const menuToggle = document.getElementById('menu-toggle');
    const tocMenu = document.getElementById('toc-menu');
    const pcSearchInput = document.getElementById('pc-search-input');
    const resultArea = document.getElementById('result-area');
    const pcList = document.getElementById('pc-list');
    const versionFilter = document.getElementById('version-filter');
    const versionBtnWrapper = document.getElementById('version-btn-wrapper');
    const fansignFilter = document.getElementById('fansign-filter');
    const fansignBtnWrapper = document.getElementById('fansign-btn-wrapper');

    let currentAlbum = '';
    let currentTab = '전체';
    let currentVer = '전체';
    let currentFsType = '전체';

    function selectAlbum(name) {
        tocMenu.style.display = 'none';
        document.getElementById('welcome-view').style.display = 'none';
        resultArea.style.display = 'block';
        document.getElementById('display-album-name').innerText = name;
        currentAlbum = name;
        
        let tabs = ['전체'];
        
        if (name === '전체') {
            tabs = ['전체']; // 상위 메뉴 '전체' 클릭 시 탭 구성
        } else if (name === 'RUDE!') {
            tabs.push('럭키드로우');
        } else if (name === 'MD 포카') {
            tabs.push('The Chase', 'STYLE', 'FOCUS', '1st ANNIVERSARY', 'Four Heart Club', '티니핑', '시즌그리팅', 'Hearts2 House', 'ARTIST BIRTHDAY PARTY CARD');
        } else if (name === '기타') {
            tabs.push('메가 커피', 'SUPER STAR SM', 'SMT 25', 'BARENBLISS', '2aN', 'sarlett', 'TELECA 2025 KPOP ROOKIE', 'SM 30th', '응원봉', '국민은행', 'LILY BROWN');
        } else if (name === 'STYLE') {
            tabs.push('예판 특전', '럭키드로우');
        } else {
            tabs.push('앨범 포카', '예판 특전', '럭키드로우', '팬싸 특전');
        }

        document.getElementById('tab-wrapper').innerHTML = tabs.map((tab, i) => `
            <button class="tab-btn ${i === 0 ? 'active' : ''}" onclick="changeTab(this, '${tab}')">${tab}</button>
        `).join('');

        changeTab(null, '전체');
    }

    function changeTab(el, cat) {
        if (el) {
            document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
            el.classList.add('active');
        }
        currentTab = cat;
        currentVer = '전체';
        currentFsType = '전체';

        if (cat === '앨범 포카' && (currentAlbum === 'The Chase' || currentAlbum === 'FOCUS')) {
            versionFilter.style.display = 'block';
            let vers = ['전체'];
            if (currentAlbum === 'The Chase') vers.push('Photobook Ver.', 'Package Ver.', 'Minibook Ver.');
            else vers.push('Rule Book Ver.', 'PhotoBook Ver.', 'Heart Locket Ver.', 'SMini Ver.');
            versionBtnWrapper.innerHTML = vers.map(v => `<button class="f-btn ${v==='전체'?'active':''}" onclick="setVersion(this, '${v}')">${v}</button>`).join('');
        } else {
            versionFilter.style.display = 'none';
        }

        if (cat === '팬싸 특전' && (currentAlbum === 'The Chase' || currentAlbum === 'FOCUS')) {
            fansignFilter.style.display = 'block';
            fansignBtnWrapper.innerHTML = ['전체', '대면', '영통'].map(t => `<button class="f-btn ${t==='전체'?'active':''}" onclick="setFsType(this, '${t}')">${t}</button>`).join('');
        } else {
            fansignFilter.style.display = 'none';
        }

        renderCards();
    }

    function setVersion(el, ver) {
        el.parentElement.querySelectorAll('.f-btn').forEach(b => b.classList.remove('active'));
        el.classList.add('active');
        currentVer = ver;
        renderCards();
    }

    function setFsType(el, type) {
        el.parentElement.querySelectorAll('.f-btn').forEach(b => b.classList.remove('active'));
        el.classList.add('active');
        currentFsType = type;
        renderCards();
    }

    function renderCards() {
        const query = pcSearchInput.value.trim().toLowerCase();
        const filtered = pcData.filter(pc => {
            const matchAlbum = currentAlbum === '전체' || pc.album === currentAlbum;
            const matchTab = currentTab === '전체' || pc.cat === currentTab;
            const matchVer = currentVer === '전체' || pc.ver === currentVer;
            const matchFs = currentFsType === '전체' || pc.type === currentFsType;
            const matchSearch = pc.name.toLowerCase().includes(query);
            return matchAlbum && matchTab && matchVer && matchFs && matchSearch;
        });

        document.getElementById('tab-label').innerText = `[${currentTab}] 결과: ${filtered.length}건`;
        pcList.innerHTML = filtered.length > 0 
            ? filtered.map(pc => `<div class="card-item"><div style="color:#ccc;">이미지</div><div class="card-name">${pc.name}</div></div>`).join('')
            : `<div style="grid-column: span 2; padding: 50px 0; color:#bbb; text-align:center;">결과가 없습니다.</div>`;
    }

    menuToggle.addEventListener('click', () => { tocMenu.style.display = tocMenu.style.display === 'block' ? 'none' : 'block'; });
    pcSearchInput.addEventListener('input', renderCards);
    document.getElementById('main-logo').addEventListener('click', () => { location.reload(); });
</script>

</body>
</html>
