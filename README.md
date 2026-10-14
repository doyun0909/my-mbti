<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MBTI로 찾는 나의 포켓몬 파트너</title>
    <style>
        :root {
            --bg-cream: #FFFDF0;
            --bg-yellow-light: #FFF9C4;
            --primary-yellow: #FFE082;
            --accent-orange: #FFA726;
            --accent-dark-orange: #F57C00;
            --text-color: #3E2723;
            --card-bg: #FFFFFF;
            --shadow-color: rgba(255, 167, 38, 0.2);
            --border-radius: 20px;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Apple SD Gothic Neo', 'Malgun Gothic', 'Noto Sans KR', sans-serif;
            -webkit-tap-highlight-color: transparent;
        }

        body {
            background-color: var(--bg-cream);
            color: var(--text-color);
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            width: 100%;
            max-width: 680px;
            background-color: #FFF;
            border-radius: calc(var(--border-radius) + 8px);
            padding: 30px 24px;
            box-shadow: 0 10px 30px var(--shadow-color);
            border: 4px solid var(--primary-yellow);
            text-align: center;
            position: relative;
            overflow: hidden;
        }

        header {
            margin-bottom: 28px;
        }

        .title-badge {
            display: inline-block;
            background-color: var(--bg-yellow-light);
            color: var(--accent-dark-orange);
            font-weight: bold;
            font-size: 0.95rem;
            padding: 6px 16px;
            border-radius: 50px;
            margin-bottom: 12px;
            border: 2px solid var(--primary-yellow);
        }

        h1 {
            font-size: 1.8rem;
            color: var(--text-color);
            margin-bottom: 8px;
            word-break: keep-all;
            line-height: 1.3;
        }

        p.subtitle {
            font-size: 1rem;
            color: #795548;
            word-break: keep-all;
        }

        .mbti-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 12px;
            margin-bottom: 10px;
        }

        @media (max-width: 480px) {
            .mbti-grid {
                grid-template-columns: repeat(2, 1fr);
                gap: 10px;
            }
            .container {
                padding: 20px 16px;
            }
            h1 {
                font-size: 1.5rem;
            }
        }

        .mbti-btn {
            background-color: var(--bg-cream);
            border: 2px solid var(--primary-yellow);
            border-radius: var(--border-radius);
            padding: 16px 8px;
            font-size: 1.15rem;
            font-weight: 800;
            color: var(--text-color);
            cursor: pointer;
            transition: all 0.2s ease-in-out;
            box-shadow: 0 4px 0 var(--primary-yellow);
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            gap: 4px;
        }

        .mbti-btn:hover {
            transform: translateY(-2px);
            background-color: var(--bg-yellow-light);
            border-color: var(--accent-orange);
            box-shadow: 0 6px 0 var(--accent-orange);
        }

        .mbti-btn:active {
            transform: translateY(2px);
            box-shadow: 0 2px 0 var(--accent-orange);
        }

        .mbti-btn .sub-text {
            font-size: 0.75rem;
            font-weight: normal;
            color: #8D6E63;
        }

        .result-section {
            display: none;
            animation: fadeIn 0.4s ease-in-out forwards;
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(12px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .pokemon-card {
            background-color: var(--bg-cream);
            border-radius: var(--border-radius);
            padding: 24px 20px;
            border: 3px solid var(--primary-yellow);
            margin-bottom: 20px;
            position: relative;
        }

        .mbti-tag {
            display: inline-block;
            background-color: var(--accent-orange);
            color: #FFF;
            font-weight: 800;
            font-size: 1.1rem;
            padding: 4px 16px;
            border-radius: 50px;
            margin-bottom: 12px;
            letter-spacing: 1px;
        }

        .pokemon-emoji {
            font-size: 5rem;
            line-height: 1;
            margin: 12px 0;
            filter: drop-shadow(0 6px 10px rgba(0,0,0,0.1));
        }

        .pokemon-name {
            font-size: 1.8rem;
            font-weight: 800;
            color: var(--text-color);
            margin-bottom: 16px;
        }

        .reason-box {
            background-color: #FFF;
            border-radius: 14px;
            padding: 16px;
            font-size: 1.05rem;
            line-height: 1.6;
            color: #4E342E;
            text-align: left;
            word-break: keep-all;
            border: 1px solid var(--primary-yellow);
            box-shadow: inset 0 2px 4px rgba(0,0,0,0.02);
        }

        .match-box {
            background-color: var(--bg-yellow-light);
            border-radius: var(--border-radius);
            padding: 18px 20px;
            border: 2px dashed var(--accent-orange);
            margin-bottom: 24px;
            text-align: left;
            display: flex;
            align-items: center;
            gap: 16px;
        }

        .match-emoji {
            font-size: 2.8rem;
            line-height: 1;
            background: #FFF;
            padding: 10px;
            border-radius: 50%;
            border: 2px solid var(--primary-yellow);
            flex-shrink: 0;
        }

        .match-info h3 {
            font-size: 0.9rem;
            color: var(--accent-dark-orange);
            margin-bottom: 4px;
            font-weight: 700;
        }

        .match-info p {
            font-size: 1.05rem;
            font-weight: 800;
            color: var(--text-color);
        }

        .match-info span {
            font-size: 0.9rem;
            font-weight: normal;
            color: #6D4C41;
            display: block;
            margin-top: 2px;
        }

        .reset-btn {
            background-color: var(--accent-orange);
            color: #FFF;
            border: none;
            border-radius: 50px;
            padding: 14px 36px;
            font-size: 1.1rem;
            font-weight: 800;
            cursor: pointer;
            box-shadow: 0 4px 0 var(--accent-dark-orange);
            transition: all 0.2s ease-in-out;
            width: 100%;
            max-width: 280px;
        }

        .reset-btn:hover {
            background-color: var(--accent-dark-orange);
            transform: translateY(-2px);
            box-shadow: 0 6px 0 #E65100;
        }

        .reset-btn:active {
            transform: translateY(2px);
            box-shadow: 0 2px 0 #E65100;
        }
    </style>
</head>
<body>

<div class="container">
    <header>
        <span class="title-badge">⚡ 포켓몬 MBTI 진단</span>
        <h1>나와 꼭 닮은 포켓몬 파트너는?</h1>
        <p class="subtitle">나의 MBTI 유형을 선택하면 어울리는 포켓몬을 찾아드려요!</p>
    </header>

    <div id="selection-screen" class="mbti-grid">
        <button class="mbti-btn" onclick="showResult('ISTJ')">ISTJ<span class="sub-text">파수꾼</span></button>
        <button class="mbti-btn" onclick="showResult('ISFJ')">ISFJ<span class="sub-text">치유사</span></button>
        <button class="mbti-btn" onclick="showResult('INFJ')">INFJ<span class="sub-text">창시자</span></button>
        <button class="mbti-btn" onclick="showResult('INTJ')">INTJ<span class="sub-text">전략가</span></button>
        <button class="mbti-btn" onclick="showResult('ISTP')">ISTP<span class="sub-text">실전파</span></button>
        <button class="mbti-btn" onclick="showResult('ISFP')">ISFP<span class="sub-text">예술가</span></button>
        <button class="mbti-btn" onclick="showResult('INFP')">INFP<span class="sub-text">꿈꾸는 이</span></button>
        <button class="mbti-btn" onclick="showResult('INTP')">INTP<span class="sub-text">탐구자</span></button>
        <button class="mbti-btn" onclick="showResult('ESTP')">ESTP<span class="sub-text">인싸</span></button>
        <button class="mbti-btn" onclick="showResult('ESFP')">ESFP<span class="sub-text">스타</span></button>
        <button class="mbti-btn" onclick="showResult('ENFP')">ENFP<span class="sub-text">긍정왕</span></button>
        <button class="mbti-btn" onclick="showResult('ENTP')">ENTP<span class="sub-text">아이디어파</span></button>
        <button class="mbti-btn" onclick="showResult('ESTJ')">ESTJ<span class="sub-text">총괄자</span></button>
        <button class="mbti-btn" onclick="showResult('ESFJ')">ESFJ<span class="sub-text">지키미</span></button>
        <button class="mbti-btn" onclick="showResult('ENFJ')">ENFJ<span class="sub-text">리더</span></button>
        <button class="mbti-btn" onclick="showResult('ENTJ')">ENTJ<span class="sub-text">지휘관</span></button>
    </div>

    <div id="result-screen" class="result-section">
        <div class="pokemon-card">
            <span id="res-mbti" class="mbti-tag">MBTI</span>
            <div id="res-emoji" class="pokemon-emoji">⚡</div>
            <div id="res-name" class="pokemon-name">포켓몬 이름</div>
            <div id="res-reason" class="reason-box">어울리는 이유 들어갈 자리</div>
        </div>

        <div class="match-box">
            <div id="res-match-emoji" class="match-emoji">🤝</div>
            <div class="match-info">
                <h3>💖 환상의 짝꿍 파트너</h3>
                <p id="res-match-title">최고의 궁합 MBTI & 포켓몬</p>
                <span id="res-match-desc">궁합 이유 설명</span>
            </div>
        </div>

        <button class="reset-btn" onclick="resetScreen()">🔄 다시 고르기</button>
    </div>
</div>

<script>
    const pokemonData = {
        'ISTJ': {
            name: '아머까오',
            emoji: '🦅',
            reason: '책임감이 강하고 원칙을 철저히 지키는 성격입니다. 묵묵히 자신의 자리를 지키며 주변 사람들에게 절대적인 신뢰를 주는 든든한 파수꾼 모습이 아머까오와 꼭 닮았습니다.',
            matchMbti: 'ENFP',
            matchPokemon: '파이리',
            matchDesc: '새로운 열정을 불어넣어 주는 유쾌한 파트너가 되어줍니다.'
        },
        'ISFJ': {
            name: '해피너스',
            emoji: '🌸',
            reason: '타인의 감정을 깊이 배려하고 정성을 다해 돕는 따뜻한 마음씨를 가졌습니다. 아픈 이들을 감싸 안고 온기를 전하는 치유사 해피너스와 어울립니다.',
            matchMbti: 'ENTP',
            matchPokemon: '팬텀',
            matchDesc: '통발 같은 장난기로 일상에 새로운 즐거움을 선물합니다.'
        },
        'INFJ': {
            name: '뮤',
            emoji: '✨',
            reason: '조용하지만 깊은 통찰력을 가지고 있으며 신비로운 매력을 발산합니다. 세상을 넓은 시야로 바라보고 가능성을 찾아내는 창시자 뮤와 완벽하게 어울립니다.',
            matchMbti: 'ESTP',
            matchPokemon: '피카츄',
            matchDesc: '망설임 없이 행동하는 에너지가 유쾌한 자극이 됩니다.'
        },
        'INTJ': {
            name: '뮤츠',
            emoji: '🔮',
            reason: '냉철한 지성과 주도면밀한 계획으로 목표를 달성해 나가는 전략가입니다. 높은 목표를 향해 끊임없이 사고하는 뮤츠의 강인하고 완벽주의적인 모습과 비슷합니다.',
            matchMbti: 'ESFP',
            matchPokemon: '푸린',
            matchDesc: '밝고 쾌활한 매력으로 긴장을 풀고 웃게 만들어 줍니다.'
        },
        'ISTP': {
            name: '루카리오',
            emoji: '🐺',
            reason: '상황 판단력이 뛰어나고 침착하게 문제를 해결하는 실전파입니다. 말보다는 행동으로 실력을 증명하며 묵묵히 정진하는 루카리오의 기사와 같은 모습입니다.',
            matchMbti: 'ESFJ',
            matchPokemon: '리자몽',
            matchDesc: '따뜻한 의리와 포용력으로 든든한 지원군이 되어줍니다.'
        },
        'ISFP': {
            name: '메타몽',
            emoji: '🫠',
            reason: '유연하고 감수성이 풍부하며 상대를 편안하게 만드는 매력이 있습니다. 환경에 맞게 자유롭게 자신을 변화시키고 수용하는 감성 예술가 메타몽을 닮았습니다.',
            matchMbti: 'ESTJ',
            matchPokemon: '거북왕',
            matchDesc: '체계적이고 확실한 리더십으로 든든한 울타리를 제공합니다.'
        },
        'INFP': {
            name: '이브이',
            emoji: '🦊',
            reason: '다정한 마음과 무한한 가능성, 이상을 품고 살아가는 꿈꾸는 이입니다. 어떤 형태로든 멋지게 진화할 수 있는 잠재력을 가진 이브이와 일치합니다.',
            matchMbti: 'ENTJ',
            matchPokemon: '디아루가',
            matchDesc: '명확한 비전과 방향성을 제시하며 성장을 이끌어 줍니다.'
        },
        'INTP': {
            name: '후딘',
            emoji: '🥄',
            reason: '지적 호기심이 왕성하며 호기심이 생기면 깊게 탐구하는 분석가입니다. 비범한 지능으로 원리를 파악하고 아이디어를 만들어내는 후딘을 떠올리게 합니다.',
            matchMbti: 'ENFJ',
            matchPokemon: '토게키스',
            matchDesc: '넓은 마음으로 생각을 지지해주고 포용해 줍니다.'
        },
        'ESTP': {
            name: '피카츄',
            emoji: '⚡',
            reason: '넘치는 에너지를 가지고 어디서나 즉각 행동에 나서는 인싸입니다. 밝고 당당한 존재감으로 주변 사람들을 즐겁게 만드는 피카츄의 매력과 닮았습니다.',
            matchMbti: 'INFJ',
            matchPokemon: '뮤',
            matchDesc: '깊고 섬세한 이야기로 서로에게 특별한 영감을 줍니다.'
        },
        'ESFP': {
            name: '푸린',
            emoji: '🎤',
            reason: '사람들 앞에 서는 것을 즐기며 주변 분위기를 금세 밝게 만듭니다. 매력적인 노래와 표정으로 모두의 시선을 사로잡는 무대 위 스타 푸린입니다.',
            matchMbti: 'INTJ',
            matchPokemon: '뮤츠',
            matchDesc: '진중한 고민에 깊이 있는 시각과 안정감을 제공해 줍니다.'
        },
        'ENFP': {
            name: '파이리',
            emoji: '🔥',
            reason: '열정이 넘치고 새로운 아이디어와 호기심이 샘솟는 긍정왕입니다. 꼬리의 불꽃처럼 꺼지지 않는 순수한 열정과 창의성을 지닌 파이리와 꼭 맞습니다.',
            matchMbti: 'ISTJ',
            matchPokemon: '아머까오',
            matchDesc: '변함없는 신뢰와 현실적인 조언으로 중심을 잡아줍니다.'
        },
        'ENTP': {
            name: '팬텀',
            emoji: '👻',
            reason: '재치 있는 장난기와 독창적인 시각으로 사람들을 놀라게 만드는 아이디어파입니다. 유쾌하고 예측 불가능한 매력으로 판을 흔드는 팬텀을 닮았습니다.',
            matchMbti: 'ISFJ',
            matchPokemon: '해피너스',
            matchDesc: '무조건적인 배려와 따뜻함으로 편안한 안식처가 되어줍니다.'
        },
        'ESTJ': {
            name: '거북왕',
            emoji: '🐢',
            reason: '책임감이 강하고 체계적으로 조직을 이끄는 카리스마 총괄자입니다. 든든한 방어력과 단호한 결단력으로 무리를 지키는 거북왕의 모습입니다.',
            matchMbti: 'ISFP',
            matchPokemon: '메타몽',
            matchDesc: '따뜻하고 유연한 감성으로 여유와 힐링을 선사합니다.'
        },
        'ESFJ': {
            name: '리자몽',
            emoji: '🐲',
            reason: '동료를 깊이 아끼고 화끈한 의리와 정으로 주변을 챙기는 지키미입니다. 강렬한 화력 뒤에 친근하고 든든한 따뜻함을 지닌 리자몽과 닮았습니다.',
            matchMbti: 'ISTP',
            matchPokemon: '루카리오',
            matchDesc: '해결사다운 침착함으로 실질적인 큰 도움을 줍니다.'
        },
        'ENFJ': {
            name: '토게키스',
            emoji: '🕊️',
            reason: '따뜻하고 포용력 있는 마음으로 주변 사람들에게 축복과 행복을 전하는 리더입니다. 사람들의 가능성을 믿고 격려해 주는 토게키스의 은혜로움과 일치합니다.',
            matchMbti: 'INTP',
            matchPokemon: '후딘',
            matchDesc: '신선하고 지적인 시각으로 새로운 대화의 장을 열어줍니다.'
        },
        'ENTJ': {
            name: '디아루가',
            emoji: '⏱️',
            reason: '압도적인 카리스마와 당당한 비전으로 목표를 향해 진격하는 지휘관입니다. 시공간을 아우르는 웅장한 존재감과 결단력을 보여주는 디아루가를 닮았습니다.',
            matchMbti: 'INFP',
            matchPokemon: '이브이',
            matchDesc: '순수한 이상과 진심 어린 공감으로 마음을 진정시켜 줍니다.'
        }
    };

    function showResult(mbti) {
        const data = pokemonData[mbti];
        if (!data) return;

        // Populate result data
        document.getElementById('res-mbti').textContent = mbti;
        document.getElementById('res-emoji').textContent = data.emoji;
        document.getElementById('res-name').textContent = data.name;
        document.getElementById('res-reason').textContent = data.reason;

        document.getElementById('res-match-emoji').textContent = getEmojiForPokemon(data.matchPokemon);
        document.getElementById('res-match-title').textContent = `${data.matchMbti} (${data.matchPokemon})`;
        document.getElementById('res-match-desc').textContent = data.matchDesc;

        // Toggle UI displays
        document.getElementById('selection-screen').style.display = 'none';
        document.getElementById('result-screen').style.display = 'block';

        // Scroll smoothly to top of container
        window.scrollTo({ top: 0, behavior: 'smooth' });
    }

    function resetScreen() {
        document.getElementById('result-screen').style.display = 'none';
        document.getElementById('selection-screen').style.display = 'grid';
        window.scrollTo({ top: 0, behavior: 'smooth' });
    }

    function getEmojiForPokemon(name) {
        for (let key in pokemonData) {
            if (pokemonData[key].name === name) {
                return pokemonData[key].emoji;
            }
        }
        return '⭐';
    }
</script>
</body>
</html>
