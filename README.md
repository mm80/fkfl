<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>판교어 번역기</title>
  <style>
    :root {
      --bg: #f5f5f7;
      --white: #ffffff;
      --primary: #4f46e5;
      --primary-light: #eef2ff;
      --primary-dark: #3730a3;
      --text: #1a1a2e;
      --text-muted: #6b7280;
      --border: #e5e7eb;
      --tag-bg: #f0fdf4;
      --tag-text: #16a34a;
      --card-shadow: 0 2px 8px rgba(0,0,0,0.07);
      --radius: 14px;
    }

    * { box-sizing: border-box; margin: 0; padding: 0; }

    body {
      font-family: -apple-system, BlinkMacSystemFont, 'Pretendard', 'Noto Sans KR', sans-serif;
      background: var(--bg);
      color: var(--text);
      min-height: 100vh;
    }

    /* ── 헤더 ── */
    header {
      background: var(--white);
      border-bottom: 1px solid var(--border);
      padding: 20px 24px 0;
      position: sticky;
      top: 0;
      z-index: 100;
      box-shadow: 0 1px 4px rgba(0,0,0,0.05);
    }

    .header-top {
      display: flex;
      align-items: center;
      gap: 10px;
      margin-bottom: 16px;
    }

    .logo {
      font-size: 22px;
      font-weight: 800;
      color: var(--primary);
      letter-spacing: -0.5px;
    }

    .logo span { color: var(--text); }

    .badge {
      background: var(--primary-light);
      color: var(--primary);
      font-size: 11px;
      font-weight: 700;
      padding: 3px 8px;
      border-radius: 20px;
    }

    /* ── 탭 ── */
    .tabs {
      display: flex;
      gap: 4px;
    }

    .tab-btn {
      padding: 10px 20px;
      border: none;
      background: none;
      font-size: 15px;
      font-weight: 600;
      color: var(--text-muted);
      cursor: pointer;
      border-bottom: 3px solid transparent;
      transition: all 0.2s;
    }

    .tab-btn.active {
      color: var(--primary);
      border-bottom-color: var(--primary);
    }

    .tab-btn:hover:not(.active) {
      color: var(--text);
    }

    /* ── 메인 ── */
    main {
      max-width: 820px;
      margin: 0 auto;
      padding: 28px 20px;
    }

    .tab-panel { display: none; }
    .tab-panel.active { display: block; }

    /* ══════════════════════════════
       탭 1 — 사전
    ══════════════════════════════ */

    .dict-search-wrap {
      position: relative;
      margin-bottom: 20px;
    }

    .dict-search-wrap svg {
      position: absolute;
      left: 14px;
      top: 50%;
      transform: translateY(-50%);
      color: var(--text-muted);
    }

    #dict-search {
      width: 100%;
      padding: 13px 16px 13px 42px;
      border: 1.5px solid var(--border);
      border-radius: var(--radius);
      font-size: 15px;
      background: var(--white);
      outline: none;
      transition: border-color 0.2s;
    }

    #dict-search:focus { border-color: var(--primary); }

    .dict-category-row {
      display: flex;
      flex-wrap: wrap;
      gap: 8px;
      margin-bottom: 20px;
    }

    .cat-btn {
      padding: 6px 14px;
      border-radius: 20px;
      border: 1.5px solid var(--border);
      background: var(--white);
      font-size: 13px;
      font-weight: 600;
      color: var(--text-muted);
      cursor: pointer;
      transition: all 0.2s;
    }

    .cat-btn.active, .cat-btn:hover {
      background: var(--primary);
      border-color: var(--primary);
      color: #fff;
    }

    .dict-count {
      font-size: 13px;
      color: var(--text-muted);
      margin-bottom: 14px;
    }

    .dict-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 14px;
    }

    @media (max-width: 600px) {
      .dict-grid { grid-template-columns: 1fr; }
    }

    .dict-card {
      background: var(--white);
      border-radius: var(--radius);
      padding: 18px;
      box-shadow: var(--card-shadow);
      border: 1.5px solid transparent;
      cursor: pointer;
      transition: all 0.2s;
      position: relative;
    }

    .dict-card:hover {
      border-color: var(--primary);
      transform: translateY(-2px);
      box-shadow: 0 6px 20px rgba(79,70,229,0.12);
    }

    .dict-card-header {
      display: flex;
      align-items: flex-start;
      justify-content: space-between;
      margin-bottom: 8px;
    }

    .dict-word {
      font-size: 18px;
      font-weight: 800;
      color: var(--primary);
    }

    .dict-cat-tag {
      font-size: 11px;
      font-weight: 700;
      padding: 3px 8px;
      border-radius: 10px;
      background: var(--primary-light);
      color: var(--primary);
      white-space: nowrap;
    }

    .dict-meaning {
      font-size: 14px;
      color: var(--text);
      font-weight: 600;
      margin-bottom: 6px;
    }

    .dict-example {
      font-size: 12px;
      color: var(--text-muted);
      line-height: 1.6;
    }

    .dict-example em {
      color: var(--primary);
      font-style: normal;
      font-weight: 600;
    }

    /* 카드 펼침 */
    .dict-card-detail {
      display: none;
      margin-top: 12px;
      padding-top: 12px;
      border-top: 1px solid var(--border);
    }

    .dict-card.open .dict-card-detail { display: block; }

    .detail-row {
      display: flex;
      gap: 8px;
      margin-bottom: 8px;
      align-items: flex-start;
    }

    .detail-label {
      font-size: 11px;
      font-weight: 700;
      color: var(--white);
      background: var(--primary);
      padding: 2px 7px;
      border-radius: 6px;
      white-space: nowrap;
      margin-top: 2px;
    }

    .detail-label.intent { background: #f59e0b; }
    .detail-label.todo   { background: #10b981; }
    .detail-label.reply  { background: #6366f1; }

    .detail-text {
      font-size: 13px;
      color: var(--text);
      line-height: 1.6;
    }

    .no-result {
      text-align: center;
      padding: 60px 0;
      color: var(--text-muted);
      font-size: 15px;
    }

    /* ══════════════════════════════
       탭 2 — 번역기
    ══════════════════════════════ */

    .translator-input-area {
      background: var(--white);
      border-radius: var(--radius);
      border: 1.5px solid var(--border);
      padding: 18px;
      box-shadow: var(--card-shadow);
      margin-bottom: 16px;
    }

    .translator-input-area label {
      display: block;
      font-size: 13px;
      font-weight: 700;
      color: var(--text-muted);
      margin-bottom: 10px;
      letter-spacing: 0.3px;
    }

    #input-text {
      width: 100%;
      min-height: 100px;
      border: none;
      outline: none;
      font-size: 15px;
      color: var(--text);
      resize: none;
      font-family: inherit;
      line-height: 1.7;
    }

    .translator-actions {
      display: flex;
      gap: 10px;
      justify-content: flex-end;
      margin-top: 10px;
      padding-top: 10px;
      border-top: 1px solid var(--border);
    }

    .example-chips {
      display: flex;
      flex-wrap: wrap;
      gap: 8px;
      margin-bottom: 16px;
    }

    .chip {
      background: var(--white);
      border: 1.5px solid var(--border);
      border-radius: 20px;
      padding: 6px 12px;
      font-size: 12px;
      color: var(--text-muted);
      cursor: pointer;
      transition: all 0.2s;
    }

    .chip:hover {
      border-color: var(--primary);
      color: var(--primary);
      background: var(--primary-light);
    }

    .btn-translate {
      background: var(--primary);
      color: #fff;
      border: none;
      border-radius: 10px;
      padding: 10px 22px;
      font-size: 14px;
      font-weight: 700;
      cursor: pointer;
      transition: background 0.2s;
      display: flex;
      align-items: center;
      gap: 6px;
    }

    .btn-translate:hover { background: var(--primary-dark); }

    .btn-clear {
      background: none;
      border: 1.5px solid var(--border);
      border-radius: 10px;
      padding: 10px 16px;
      font-size: 14px;
      color: var(--text-muted);
      cursor: pointer;
      transition: all 0.2s;
    }

    .btn-clear:hover { border-color: #ef4444; color: #ef4444; }

    /* 결과 카드 */
    .result-container { display: none; }
    .result-container.visible { display: block; }

    .result-steps {
      display: flex;
      flex-direction: column;
      gap: 12px;
    }

    .result-step {
      background: var(--white);
      border-radius: var(--radius);
      padding: 18px 20px;
      box-shadow: var(--card-shadow);
      border-left: 4px solid var(--primary);
      animation: slideUp 0.3s ease both;
    }

    .result-step:nth-child(2) { animation-delay: 0.07s; border-left-color: #f59e0b; }
    .result-step:nth-child(3) { animation-delay: 0.14s; border-left-color: #10b981; }
    .result-step:nth-child(4) { animation-delay: 0.21s; border-left-color: #6366f1; }

    @keyframes slideUp {
      from { opacity: 0; transform: translateY(12px); }
      to   { opacity: 1; transform: translateY(0); }
    }

    .step-header {
      display: flex;
      align-items: center;
      gap: 8px;
      margin-bottom: 10px;
    }

    .step-num {
      width: 24px;
      height: 24px;
      border-radius: 50%;
      background: var(--primary);
      color: #fff;
      font-size: 12px;
      font-weight: 800;
      display: flex;
      align-items: center;
      justify-content: center;
      flex-shrink: 0;
    }

    .result-step:nth-child(2) .step-num { background: #f59e0b; }
    .result-step:nth-child(3) .step-num { background: #10b981; }
    .result-step:nth-child(4) .step-num { background: #6366f1; }

    .step-title {
      font-size: 13px;
      font-weight: 700;
      color: var(--text-muted);
    }

    .step-body {
      font-size: 15px;
      color: var(--text);
      line-height: 1.75;
    }

    .step-body .highlight {
      background: #fef9c3;
      border-radius: 4px;
      padding: 0 3px;
      font-weight: 600;
    }

    .step-body .translated-word {
      color: var(--primary);
      font-weight: 700;
    }

    .detected-words {
      display: flex;
      flex-wrap: wrap;
      gap: 6px;
      margin-top: 10px;
    }

    .detected-tag {
      display: flex;
      align-items: center;
      gap: 4px;
      background: var(--primary-light);
      border-radius: 20px;
      padding: 4px 10px;
      font-size: 12px;
    }

    .detected-tag .orig { color: var(--primary); font-weight: 700; }
    .detected-tag .arrow { color: var(--text-muted); }
    .detected-tag .trans { color: var(--text); font-weight: 600; }

    .reply-box {
      background: #f8faff;
      border: 1px solid #c7d2fe;
      border-radius: 10px;
      padding: 14px 16px;
      font-size: 14px;
      line-height: 1.8;
      color: var(--text);
      position: relative;
    }

    .copy-btn {
      position: absolute;
      top: 10px;
      right: 10px;
      background: var(--white);
      border: 1px solid var(--border);
      border-radius: 7px;
      padding: 4px 10px;
      font-size: 12px;
      color: var(--text-muted);
      cursor: pointer;
      transition: all 0.2s;
    }

    .copy-btn:hover { border-color: var(--primary); color: var(--primary); }
    .copy-btn.copied { background: #d1fae5; border-color: #10b981; color: #10b981; }

    /* 판교어 없을 때 */
    .no-pangyo {
      text-align: center;
      padding: 30px;
      color: var(--text-muted);
      font-size: 14px;
    }

    /* 풋터 */
    footer {
      text-align: center;
      padding: 30px 20px;
      font-size: 12px;
      color: var(--text-muted);
    }
  </style>
</head>
<body>

<header>
  <div class="header-top">
    <div class="logo">판교어<span>번역기</span></div>
    <div class="badge">BETA</div>
  </div>
  <div class="tabs">
    <button class="tab-btn active" onclick="switchTab('dict', this)">📖 판교어 사전</button>
    <button class="tab-btn" onclick="switchTab('translator', this)">🔄 번역기</button>
  </div>
</header>

<main>
  <!-- ═══════════ 탭 1: 사전 ═══════════ -->
  <div id="tab-dict" class="tab-panel active">

    <div class="dict-search-wrap">
      <svg width="16" height="16" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
        <circle cx="11" cy="11" r="8"/><path d="m21 21-4.35-4.35"/>
      </svg>
      <input id="dict-search" type="text" placeholder="판교어 검색... (예: 얼라인, 스프린트)" oninput="renderDict()" />
    </div>

    <div class="dict-category-row" id="cat-row"></div>

    <div class="dict-count" id="dict-count"></div>

    <div class="dict-grid" id="dict-grid"></div>

  </div>

  <!-- ═══════════ 탭 2: 번역기 ═══════════ -->
  <div id="tab-translator" class="tab-panel">

    <div class="example-chips" id="example-chips"></div>

    <div class="translator-input-area">
      <label>판교어가 섞인 문장을 입력하세요</label>
      <textarea id="input-text" placeholder="예: 이번 건은 얼라인 맞추고 리소스 태워서 빠르게 이터레이션 돌려봅시다."></textarea>
      <div class="translator-actions">
        <button class="btn-clear" onclick="clearInput()">지우기</button>
        <button class="btn-translate" onclick="translate()">
          <svg width="14" height="14" fill="none" stroke="currentColor" stroke-width="2.5" viewBox="0 0 24 24">
            <path d="M5 12h14M12 5l7 7-7 7"/>
          </svg>
          번역하기
        </button>
      </div>
    </div>

    <div class="result-container" id="result-container">
      <div class="result-steps" id="result-steps"></div>
    </div>

  </div>
</main>

<footer>판교어 번역기 · 스타트업·IT 직장인 용어 해석 도구</footer>

<script>
// ════════════════════════════════════════
//  사전 데이터
// ════════════════════════════════════════
const DICT = [
  {
    word: "얼라인", eng: "Align",
    cat: "소통",
    meaning: "서로 의견이나 방향을 맞추다",
    example: "팀장이랑 먼저 얼라인 맞추고 진행합시다.",
    plain: "서로 의견을 맞추다",
    intent: "지금 당신과 나, 또는 여러 팀 사이에 생각 차이가 있을 수 있으니 먼저 확인하자는 뜻",
    todo: "짧은 미팅을 잡거나, 메신저로 '이 방향으로 이해했는데 맞나요?'라고 먼저 확인",
    reply: "네, 제가 이해한 방향은 ○○인데 맞을까요? 한 번 짧게 얘기 나눌 수 있을까요?"
  },
  {
    word: "싱크", eng: "Sync",
    cat: "소통",
    meaning: "서로 정보나 현황을 공유하다",
    example: "주 1회 싱크 미팅 하면 어떨까요?",
    plain: "서로 상황을 공유하고 맞추다",
    intent: "지금 각자 아는 정보가 다를 수 있으니 한자리에서 맞추자는 뜻",
    todo: "짧은 정기 미팅 일정 잡기 또는 슬랙/메신저로 현황 공유 메시지 보내기",
    reply: "좋습니다. ○요일 ○시 어떠세요? 간단히 15분이면 될 것 같아요."
  },
  {
    word: "리소스", eng: "Resource",
    cat: "자원",
    meaning: "사람, 시간, 예산 등 투입 가능한 자원",
    example: "이번 프로젝트에 리소스를 더 태워야 할 것 같아요.",
    plain: "사람과 시간(및 돈)을 더 투입해야 한다",
    intent: "지금 인력이나 시간이 부족하니 추가 지원이 필요하다는 신호",
    todo: "어떤 리소스가 얼마나 필요한지 구체적으로 정리해서 보고하기",
    reply: "현재 ○명이 ○업무에 붙어 있는데, ○주 내 완료하려면 ○명이 더 필요합니다."
  },
  {
    word: "스프린트", eng: "Sprint",
    cat: "일정",
    meaning: "짧은 기간 동안 집중해서 일하는 개발 단위 (보통 1~2주)",
    example: "이번 스프린트 목표는 로그인 기능 완료입니다.",
    plain: "1~2주 단위로 목표를 정해 집중 작업하는 기간",
    intent: "짧은 주기로 성과를 내고 방향을 조정하겠다는 의미",
    todo: "이번 스프린트 목표와 내 담당 업무를 명확히 확인하고 우선순위 정리",
    reply: "이번 스프린트 제 담당 항목은 ○○, ○○이고 ○일까지 완료 예정입니다."
  },
  {
    word: "이터레이션", eng: "Iteration",
    cat: "일정",
    meaning: "만들고 → 확인하고 → 수정하는 과정을 반복하다",
    example: "일단 MVP 만들고 이터레이션 돌리면서 개선해봅시다.",
    plain: "빠르게 만들어보고 계속 수정·개선하다",
    intent: "완벽하게 만들기보다 빠르게 시도하고 고쳐가자는 뜻",
    todo: "첫 버전을 작게 빨리 만들어 공유하고, 피드백 받아 수정하는 사이클 준비",
    reply: "초안을 ○일까지 먼저 공유드리고, 피드백 주시면 바로 반영하겠습니다."
  },
  {
    word: "컨펌", eng: "Confirm",
    cat: "의사결정",
    meaning: "최종 승인·확인을 받다",
    example: "대표님 컨펌 떨어지면 바로 진행합니다.",
    plain: "윗사람의 최종 승인·OK를 받다",
    intent: "아직 결정권자의 승인이 나지 않았으니 기다리거나 먼저 받아오라는 의미",
    todo: "결정권자에게 명확하게 '이 건 진행해도 될까요?'라고 확인 요청",
    reply: "○○ 건 진행 전에 컨펌 필요한데, ○월 ○일까지 확인 가능하실까요?"
  },
  {
    word: "팔로업", eng: "Follow-up",
    cat: "소통",
    meaning: "이전에 논의한 내용을 계속 챙기고 확인하다",
    example: "지난번 팔로업 해주세요.",
    plain: "지난번에 얘기한 거 어떻게 됐는지 확인해주세요",
    intent: "당신이 그 건을 잊지 말고 다시 확인·진행해달라는 요청",
    todo: "해당 건의 현황을 파악하고, 담당자에게 진행 상황 메시지 보내기",
    reply: "지난번 ○○ 건 현황 확인했습니다. 현재 ○○ 단계이며 ○일 완료 예정입니다."
  },
  {
    word: "딥다이브", eng: "Deep Dive",
    cat: "분석",
    meaning: "어떤 주제를 깊고 집중적으로 파고들다",
    example: "이 지표 왜 이러는지 딥다이브 해볼게요.",
    plain: "이 문제를 깊게 파헤쳐서 원인을 찾아볼게요",
    intent: "표면적 현상이 아니라 근본 원인을 제대로 분석하겠다는 의지 표현",
    todo: "관련 데이터, 로그, 히스토리 등을 수집하고 원인 분석 문서 작성 시작",
    reply: "이번 주 중으로 딥다이브 결과를 정리해서 공유드리겠습니다."
  },
  {
    word: "온보딩", eng: "Onboarding",
    cat: "조직",
    meaning: "새 구성원이 조직·업무에 적응하도록 돕는 과정",
    example: "신규 입사자 온보딩 프로그램 준비 중입니다.",
    plain: "새로 들어온 사람이 빨리 적응하도록 도와주는 과정",
    intent: "새 구성원이 헤매지 않도록 체계적으로 안내해야 한다는 의미",
    todo: "온보딩 체크리스트 작성, 주요 문서 링크 정리, 첫 주 일정 안내",
    reply: "온보딩 자료 정리해서 첫날 공유드리겠습니다. 필요한 계정·접근권한도 미리 준비할게요."
  },
  {
    word: "레버리지", eng: "Leverage",
    cat: "전략",
    meaning: "자원을 최대한 효율적으로 활용해 큰 효과를 내다",
    example: "기존 고객 데이터를 레버리지해서 마케팅에 써봅시다.",
    plain: "기존에 가진 것을 잘 활용해서 더 큰 효과를 내다",
    intent: "새 비용을 들이지 않고 기존 자산을 활용해 효율을 높이자는 제안",
    todo: "활용 가능한 기존 자원(데이터, 채널, 관계)이 무엇인지 목록화",
    reply: "기존 ○○ 자산을 활용하면 ○○ 효과를 볼 수 있을 것 같습니다. 구체안 공유드릴게요."
  },
  {
    word: "피벗", eng: "Pivot",
    cat: "전략",
    meaning: "사업이나 전략의 방향을 크게 바꾸다",
    example: "지표가 안 나오면 피벗해야 할 수도 있어요.",
    plain: "지금 하는 방향이 안 되면 완전히 방향을 바꿔야 할 수 있어요",
    intent: "현재 방식이 한계에 왔으니 큰 방향 전환을 고려해야 한다는 경고",
    todo: "현재 지표와 문제점을 정리하고, 새로운 방향에 대한 가설 수립",
    reply: "현재 성과 지표와 문제 상황 정리해서 피벗 여부 논의 자료 준비하겠습니다."
  },
  {
    word: "MVp", eng: "MVP",
    cat: "개발",
    meaning: "최소한의 기능만 담은 첫 번째 제품 (Minimum Viable Product)",
    example: "MVP 먼저 뽑고 반응 보죠.",
    plain: "핵심 기능만 넣은 가장 간단한 첫 버전을 먼저 만들어보죠",
    intent: "완벽하게 만들지 말고 빠르게 시장 반응을 보자는 의미",
    todo: "핵심 기능 1~3개만 정의하고, 나머지는 다음 버전으로 미루기",
    reply: "핵심 기능 ○○, ○○만 넣어 ○주 안에 MVP 출시 목표로 진행하겠습니다."
  },
  {
    word: "KPI", eng: "KPI",
    cat: "성과",
    meaning: "목표 달성 여부를 측정하는 핵심 지표 (Key Performance Indicator)",
    example: "이번 분기 KPI가 뭔지 명확히 해주세요.",
    plain: "이번 분기 성공했는지 판단하는 주요 숫자 목표가 뭔지 알려주세요",
    intent: "지금 어떤 숫자를 목표로 일하는지 명확히 하자는 요구",
    todo: "내 KPI 항목과 목표 수치 확인, 현재 달성 현황 정리",
    reply: "제 KPI는 ○○이며, 현재 ○○% 달성했습니다. ○월까지 ○○ 목표입니다."
  },
  {
    word: "오너십", eng: "Ownership",
    cat: "조직",
    meaning: "어떤 업무나 프로젝트에 대한 책임감을 갖고 주도적으로 이끌다",
    example: "이 프로젝트 오너십은 김 대리가 갖고 가세요.",
    plain: "이 프로젝트를 김 대리가 책임지고 끝까지 맡아서 이끌어주세요",
    intent: "당신이 이 일의 책임자이므로 주도적으로 움직이라는 기대",
    todo: "내가 담당하는 업무 범위 명확히 정의, 의사결정 사항 직접 챙기기",
    reply: "해당 프로젝트 오너십 갖고 진행하겠습니다. 주요 의사결정 사항은 사전 공유드리겠습니다."
  },
  {
    word: "액션 아이템", eng: "Action Item",
    cat: "소통",
    meaning: "회의 등에서 나온 구체적으로 실행할 일",
    example: "오늘 미팅 액션 아이템 정리해서 공유해주세요.",
    plain: "오늘 회의에서 각자 해야 할 구체적인 일들 정리해서 공유해주세요",
    intent: "회의가 말로만 끝나지 않도록 실제로 누가 뭘 할지 명확히 하자는 의미",
    todo: "담당자·기한 포함해서 할 일 목록 정리 후 공유",
    reply: "오늘 액션 아이템 정리했습니다. ○○(담당:○○, ○일까지), ○○(담당:○○, ○일까지)"
  },
  {
    word: "에스컬레이션", eng: "Escalation",
    cat: "의사결정",
    meaning: "해결 안 되는 문제를 상위 결정권자에게 올려 처리하다",
    example: "이건 팀장 선에서 안 되면 에스컬레이션 해야 해요.",
    plain: "팀장이 해결 못 하면 더 높은 사람에게 보고해서 결정받아야 해요",
    intent: "지금 단계에서 해결이 어려우니 더 높은 권한이 필요하다는 판단",
    todo: "현재 상황, 시도한 해결책, 필요한 결정 사항을 정리해서 보고 준비",
    reply: "○○ 건은 팀 내 해결이 어려워 임원 보고 후 결정 받으려 합니다. 보고 자료 준비 중입니다."
  },
  {
    word: "트래킹", eng: "Tracking",
    cat: "성과",
    meaning: "목표나 지표의 진행 상황을 주기적으로 확인·기록하다",
    example: "주간 KPI 트래킹 시트 업데이트 해주세요.",
    plain: "목표 수치가 얼마나 달성됐는지 주기적으로 기록·확인해주세요",
    intent: "현재 목표 대비 어디에 와 있는지 가시화하려는 요청",
    todo: "해당 지표 최신 데이터 수집 후 트래킹 시트 업데이트",
    reply: "이번 주 트래킹 업데이트했습니다. ○○ 지표 현재 ○○, 목표 대비 ○○% 수준입니다."
  },
  {
    word: "그루밍", eng: "Grooming",
    cat: "개발",
    meaning: "다음 작업 목록을 미리 검토하고 우선순위를 정리하는 회의",
    example: "백로그 그루밍 미팅 내일 오후 3시에 잡겠습니다.",
    plain: "앞으로 할 일 목록을 함께 검토하고 중요도와 순서를 정하는 회의",
    intent: "다음 개발 주기를 원활히 시작하기 위해 사전 준비 미팅을 하자는 의미",
    todo: "현재 백로그(할 일 목록)에서 본인 담당 항목 미리 검토하고 우선순위 의견 준비",
    reply: "백로그 그루밍 참석하겠습니다. 사전에 제 담당 항목 검토해서 의견 가져오겠습니다."
  },
  {
    word: "스케일업", eng: "Scale-up",
    cat: "전략",
    meaning: "사업이나 시스템의 규모를 빠르게 키우다",
    example: "지역 검증 끝났으면 이제 스케일업 해야죠.",
    plain: "한 지역에서 검증됐으니 이제 더 크게 확장해야죠",
    intent: "검증 단계를 넘어 본격적으로 성장시킬 때가 됐다는 신호",
    todo: "확장에 필요한 추가 인력, 예산, 시스템 요건 정리",
    reply: "스케일업 위한 필요 조건 정리해서 공유드리겠습니다. 우선 ○○부터 확장 제안드립니다."
  },
  {
    word: "페인포인트", eng: "Pain Point",
    cat: "기획",
    meaning: "사용자나 고객이 불편하게 느끼는 핵심 문제점",
    example: "고객 페인포인트를 먼저 정확히 파악해야 해요.",
    plain: "고객이 가장 불편하고 힘들어하는 문제가 뭔지 먼저 정확히 알아야 해요",
    intent: "문제를 제대로 이해해야 제대로 된 해결책을 만들 수 있다는 강조",
    todo: "고객 인터뷰, 리뷰, CS 데이터 등을 통해 핵심 불편 사항 수집·정리",
    reply: "고객 인터뷰 및 리뷰 데이터 분석해서 주요 페인포인트 ○가지 정리해 공유드리겠습니다."
  }
];

// ════════════════════════════════════════
//  번역기용 예시 문장
// ════════════════════════════════════════
const EXAMPLES = [
  "이번 건은 일단 얼라인 맞추고, 리소스 태워서 스프린트 단위로 빠르게 이터레이션 돌려보죠.",
  "대표님 컨펌 받기 전에 팀장님이랑 먼저 싱크 한 번 맞추고 액션 아이템 정리해주세요.",
  "지난번 팔로업 아직 안 됐죠? 이번 주 안으로 KPI 트래킹 업데이트하고 에스컬레이션 여부 판단해야 해요.",
  "MVP에 집중해서 페인포인트 해결하고, 그다음 스케일업 타이밍 보죠.",
];

// ════════════════════════════════════════
//  번역 사전 (단어 치환용)
// ════════════════════════════════════════
const TRANS_MAP = [
  { re: /\bmvp\b/gi,         ko: "MVP", plain: "핵심 기능만 넣은 첫 버전" },
  { re: /얼라인/g,            ko: "얼라인",    plain: "서로 의견 맞추기" },
  { re: /싱크/g,              ko: "싱크",      plain: "상황 공유" },
  { re: /리소스/g,            ko: "리소스",    plain: "사람·시간·예산" },
  { re: /스프린트/g,          ko: "스프린트",  plain: "1~2주 집중 작업 기간" },
  { re: /이터레이션/g,        ko: "이터레이션",plain: "빠른 반복 개선" },
  { re: /컨펌/g,              ko: "컨펌",      plain: "최종 승인" },
  { re: /팔로업/g,            ko: "팔로업",    plain: "진행 상황 재확인" },
  { re: /딥다이브/g,          ko: "딥다이브",  plain: "깊이 파고들기" },
  { re: /온보딩/g,            ko: "온보딩",    plain: "새 구성원 적응 지원" },
  { re: /레버리지/g,          ko: "레버리지",  plain: "기존 자원 최대 활용" },
  { re: /피벗/g,              ko: "피벗",      plain: "방향 전환" },
  { re: /kpi/gi,             ko: "KPI",       plain: "핵심 성과 지표" },
  { re: /오너십/g,            ko: "오너십",    plain: "주인의식·책임감" },
  { re: /액션\s*아이템/g,     ko: "액션 아이템",plain: "구체적 실행 과제" },
  { re: /에스컬레이션/g,      ko: "에스컬레이션",plain: "상위 보고·결정 요청" },
  { re: /트래킹/g,            ko: "트래킹",    plain: "진행 상황 추적" },
  { re: /그루밍/g,            ko: "그루밍",    plain: "작업 목록 사전 검토" },
  { re: /스케일업/g,          ko: "스케일업",  plain: "규모 확장" },
  { re: /페인\s*포인트/g,     ko: "페인포인트",plain: "고객 핵심 불편 사항" },
  { re: /백로그/g,            ko: "백로그",    plain: "대기 중인 작업 목록" },
];

// ════════════════════════════════════════
//  카테고리 목록 추출
// ════════════════════════════════════════
const CATS = ["전체", ...new Set(DICT.map(d => d.cat))];

let currentCat = "전체";
let openCardWord = null;

// ════════════════════════════════════════
//  탭 전환
// ════════════════════════════════════════
function switchTab(id, btn) {
  document.querySelectorAll(".tab-panel").forEach(p => p.classList.remove("active"));
  document.querySelectorAll(".tab-btn").forEach(b => b.classList.remove("active"));
  document.getElementById("tab-" + id).classList.add("active");
  btn.classList.add("active");
}

// ════════════════════════════════════════
//  사전 렌더
// ════════════════════════════════════════
function initCats() {
  const row = document.getElementById("cat-row");
  CATS.forEach(cat => {
    const btn = document.createElement("button");
    btn.className = "cat-btn" + (cat === "전체" ? " active" : "");
    btn.textContent = cat;
    btn.onclick = () => {
      currentCat = cat;
      document.querySelectorAll(".cat-btn").forEach(b => b.classList.remove("active"));
      btn.classList.add("active");
      renderDict();
    };
    row.appendChild(btn);
  });
}

function renderDict() {
  const q = document.getElementById("dict-search").value.trim().toLowerCase();
  let items = DICT;

  if (currentCat !== "전체") items = items.filter(d => d.cat === currentCat);
  if (q) items = items.filter(d =>
    d.word.toLowerCase().includes(q) ||
    d.eng.toLowerCase().includes(q) ||
    d.meaning.includes(q)
  );

  document.getElementById("dict-count").textContent = `총 ${items.length}개 용어`;

  const grid = document.getElementById("dict-grid");
  grid.innerHTML = "";

  if (items.length === 0) {
    grid.innerHTML = `<div class="no-result" style="grid-column:1/-1">🔍 검색 결과가 없어요</div>`;
    return;
  }

  items.forEach(d => {
    const card = document.createElement("div");
    card.className = "dict-card" + (openCardWord === d.word ? " open" : "");
    card.innerHTML = `
      <div class="dict-card-header">
        <div class="dict-word">${d.word} <span style="font-size:12px;color:#9ca3af;font-weight:500">${d.eng}</span></div>
        <div class="dict-cat-tag">${d.cat}</div>
      </div>
      <div class="dict-meaning">${d.meaning}</div>
      <div class="dict-example">"<em>${d.word}</em>"이 쓰인 문장:<br>${d.example}</div>
      <div class="dict-card-detail">
        <div class="detail-row">
          <div class="detail-label">번역</div>
          <div class="detail-text">${d.plain}</div>
        </div>
        <div class="detail-row">
          <div class="detail-label intent">의도</div>
          <div class="detail-text">${d.intent}</div>
        </div>
        <div class="detail-row">
          <div class="detail-label todo">할 일</div>
          <div class="detail-text">${d.todo}</div>
        </div>
        <div class="detail-row">
          <div class="detail-label reply">답장</div>
          <div class="detail-text">${d.reply}</div>
        </div>
      </div>
    `;
    card.onclick = () => {
      const isOpen = card.classList.contains("open");
      document.querySelectorAll(".dict-card").forEach(c => c.classList.remove("open"));
      openCardWord = isOpen ? null : d.word;
      if (!isOpen) card.classList.add("open");
    };
    grid.appendChild(card);
  });
}

// ════════════════════════════════════════
//  예시 칩
// ════════════════════════════════════════
function initChips() {
  const wrap = document.getElementById("example-chips");
  EXAMPLES.forEach(ex => {
    const chip = document.createElement("div");
    chip.className = "chip";
    chip.textContent = "💬 " + ex.slice(0, 24) + "…";
    chip.title = ex;
    chip.onclick = () => {
      document.getElementById("input-text").value = ex;
      translate();
    };
    wrap.appendChild(chip);
  });
}

// ════════════════════════════════════════
//  번역 로직
// ════════════════════════════════════════
function translate() {
  const raw = document.getElementById("input-text").value.trim();
  if (!raw) return;

  // 1) 감지된 판교어 & 치환
  const detected = [];
  let translated = raw;
  TRANS_MAP.forEach(({ re, ko, plain }) => {
    if (re.test(raw)) {
      detected.push({ ko, plain });
      re.lastIndex = 0;
    }
    re.lastIndex = 0;
    translated = translated.replace(re, `__${plain}__`);
  });

  // 2) 번역문 — __...__ 를 강조 span으로
  const translatedHtml = translated.replace(/__(.+?)__/g,
    (_, p) => `<span class="translated-word">${p}</span>`);

  // 판교어 없을 경우
  if (detected.length === 0) {
    document.getElementById("result-container").classList.add("visible");
    document.getElementById("result-steps").innerHTML = `
      <div class="no-pangyo">🙂 판교어가 감지되지 않았어요. 일반적인 문장인 것 같아요!</div>
    `;
    return;
  }

  // 3) 의도 분석 (감지 단어 기반)
  const intentMap = {
    "얼라인": "의견 불일치 가능성을 우려해 먼저 방향을 맞추고 싶어 합니다.",
    "싱크": "정보 차이가 생기지 않도록 정기적으로 소통하길 원합니다.",
    "리소스": "현재 인력·시간이 부족하거나, 추가 투입이 필요한 상황임을 알리고 있습니다.",
    "스프린트": "단기 집중 개발 주기로 빠르게 성과를 내자는 의도입니다.",
    "이터레이션": "완벽함보다 속도를 중시하며 반복 개선으로 나아가자는 뜻입니다.",
    "컨펌": "아직 결정이 안 났으며, 승인 절차가 남아 있음을 의미합니다.",
    "팔로업": "이전 논의 사항이 처리됐는지 당신이 직접 확인해주길 기대합니다.",
    "딥다이브": "표면적 해석에 그치지 말고 근본 원인까지 철저히 분석하길 바랍니다.",
    "오너십": "당신이 이 업무의 최종 책임자임을 명확히 하는 발언입니다.",
    "액션 아이템": "회의 내용이 실행으로 이어지도록 구체적 과제를 정의하려 합니다.",
    "에스컬레이션": "현재 단계에서 해결이 불가능하니 상위 결정권자가 나서야 한다는 의미입니다.",
    "KPI": "어떤 숫자를 목표로 삼아 일하는지 명확히 하자는 요구입니다.",
    "트래킹": "목표 대비 현재 진행 상황을 수치로 가시화하려 합니다.",
    "페인포인트": "고객이 겪는 핵심 불편 사항을 정확히 짚어야 한다는 강조입니다.",
    "스케일업": "검증이 끝났으니 이제 본격적으로 사업 규모를 키울 때가 됐다는 신호입니다.",
    "피벗": "현재 방향이 한계에 달해 큰 전략 변경이 필요할 수 있다는 경고입니다.",
    "MVP": "완성도보다 속도를 중시하며 빠른 시장 검증을 원합니다.",
    "핵심 기능만 넣은 첫 버전": "완성도보다 속도를 중시하며 빠른 시장 검증을 원합니다.",
    "그루밍": "다음 개발 주기를 원활히 준비하기 위한 사전 검토를 요청합니다.",
    "레버리지": "새 비용 없이 기존 자산을 활용해 효율을 높이자는 제안입니다.",
    "백로그": "현재 대기 중인 작업 목록을 관리·정리해야 한다는 맥락입니다.",
  };

  const intents = [...new Set(detected.map(d => intentMap[d.ko] || "").filter(Boolean))];
  const intentText = intents.length
    ? intents.join("<br>• ")
    : "빠른 실행과 효율적인 협업을 중시하는 스타트업 문화가 반영된 발언입니다.";

  // 4) 할 일
  const todoItems = detected
    .map(d => {
      const entry = DICT.find(e => e.word === d.ko || e.plain === d.ko);
      return entry ? `• ${entry.todo}` : null;
    })
    .filter(Boolean);

  const todoText = [...new Set(todoItems)].join("<br>") ||
    "• 발언 내용을 정리해 담당자와 일정을 확인하세요.";

  // 5) 답장 초안 (첫 번째 감지어 기반)
  const firstEntry = DICT.find(e => e.word === detected[0]?.ko);
  const replyText = firstEntry ? firstEntry.reply
    : "말씀 주신 내용 확인했습니다. 구체적인 일정 조율 후 다시 공유드리겠습니다.";

  // ── 렌더 ──
  document.getElementById("result-container").classList.add("visible");
  document.getElementById("result-steps").innerHTML = `

    <div class="result-step">
      <div class="step-header">
        <div class="step-num">1</div>
        <div class="step-title">사람말 번역</div>
      </div>
      <div class="step-body">${translatedHtml}</div>
      <div class="detected-words">
        ${detected.map(d => `
          <div class="detected-tag">
            <span class="orig">${d.ko}</span>
            <span class="arrow">→</span>
            <span class="trans">${d.plain}</span>
          </div>
        `).join("")}
      </div>
    </div>

    <div class="result-step">
      <div class="step-header">
        <div class="step-num">2</div>
        <div class="step-title">이 말의 진짜 의도</div>
      </div>
      <div class="step-body">• ${intentText}</div>
    </div>

    <div class="result-step">
      <div class="step-header">
        <div class="step-num">3</div>
        <div class="step-title">내가 해야 할 일</div>
      </div>
      <div class="step-body">${todoText}</div>
    </div>

    <div class="result-step">
      <div class="step-header">
        <div class="step-num">4</div>
        <div class="step-title">답장 초안</div>
      </div>
      <div class="step-body">
        <div class="reply-box" id="reply-box">
          ${replyText}
          <button class="copy-btn" onclick="copyReply()">복사</button>
        </div>
      </div>
    </div>

  `;
}

function clearInput() {
  document.getElementById("input-text").value = "";
  document.getElementById("result-container").classList.remove("visible");
  document.getElementById("result-steps").innerHTML = "";
}

function copyReply() {
  const box = document.getElementById("reply-box");
  const text = box.innerText.replace("복사", "").trim();
  navigator.clipboard.writeText(text).then(() => {
    const btn = box.querySelector(".copy-btn");
    btn.textContent = "✓ 복사됨";
    btn.classList.add("copied");
    setTimeout(() => { btn.textContent = "복사"; btn.classList.remove("copied"); }, 2000);
  });
}

// ════════════════════════════════════════
//  초기화
// ════════════════════════════════════════
initCats();
renderDict();
initChips();
</script>
</body>
</html>
