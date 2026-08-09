<script setup>
import { onMounted, onUnmounted, ref } from 'vue';
import {
  Mail,
  Server,
  Database,
  Cloud,
  Sparkles,
  Code2,
  Github,
  Youtube,
  ShieldCheck,
  GraduationCap,
  BadgeCheck,
  ChevronLeft,
  ChevronRight
} from 'lucide-vue-next';

const profileImage = new URL('./static/images/profile/profile_image.jpg', import.meta.url).href;
const fillyImages = {
  main: new URL('./static/images/filly-images/main.png', import.meta.url).href,
  systemArchitecture: new URL('./static/images/filly-images/system_architecture.png', import.meta.url).href,
  writeDiary: new URL('./static/images/filly-images/write_diary.png', import.meta.url).href,
  diaryDetail: new URL('./static/images/filly-images/diary_detail.png', import.meta.url).href,
  archives: new URL('./static/images/filly-images/archives.png', import.meta.url).href,
  contents: new URL('./static/images/filly-images/contents.png', import.meta.url).href,
  stats: new URL('./static/images/filly-images/stats.png', import.meta.url).href,
  id_card: new URL('./static/images/filly-images/id_card.png', import.meta.url).href
};

const cjFinalProjectImages = {
  classroom: new URL('./static/images/cj-final-projects/classroom.png', import.meta.url).href,
  examEdit: new URL('./static/images/cj-final-projects/exam-edit.png', import.meta.url).href,
  examReport: new URL('./static/images/cj-final-projects/exam-report.png', import.meta.url).href,
  learningStatus: new URL('./static/images/cj-final-projects/learning-status.png', import.meta.url).href,
  systemArchitecture: new URL('./static/images/cj-final-projects/system-architecture.png', import.meta.url).href
};

const projects = [
  {
    title: 'Filly — AI 일기 생성 서비스',
    period: '2026.03 ~ 2026.06',
    role: '팀장 / 백엔드 개발 / 인프라 구축',
    stack: ['Java', 'Spring Boot', 'Spring Security', 'Spring Data JPA', 'MySQL', 'OAuth2', 'JWT', 'Docker', 'Google Cloud Run', 'Cloud SQL', 'Google Cloud Storage', 'Caffeine Cache', 'Gemini API'],
    summary: '사용자가 짧은 문장과 이미지를 기반으로 일기를 쉽게 작성할 수 있도록 돕는 AI 일기 생성 서비스입니다.',
    highlights: [
      'Naver / Kakao / Google OAuth2 로그인 및 JWT 기반 인증 구현',
      'Spring Data JPA 기반 사용자 및 일기 데이터 처리, REST API 개발',
      'Google Cloud Storage 이미지를 비공개로 관리하고 Signed URL 기반 이미지 접근 제어 구현',
      'Docker 기반 Spring Boot 애플리케이션을 Google Cloud Run에 배포'
    ],
    problem: '메인 페이지에서 일기 약 10개와 이미지 약 30개를 조회할 때 Signed URL 생성이 반복되어 최초 로딩이 약 12초까지 지연됐습니다.',
    solution: 'Signed URL 유효기간 1시간에 맞춰 Caffeine Cache TTL을 50분, maximumSize를 10,000으로 설정했습니다. 반복 요청은 캐시의 Signed URL을 재사용하고, 최초 캐시 미스는 CompletableFuture + ExecutorService로 여러 Signed URL을 병렬 생성했습니다.',
    result: '메인 페이지 최초 로딩 약 12초 → 1~2초',
    cacheDecision: 'Cloud Run은 최대 3개 인스턴스로 확장될 수 있어 local cache가 인스턴스 간 공유되지 않는 한계가 있었지만, Signed URL은 재생성 가능한 파생 데이터이므로 데이터 정합성에 영향을 주지 않는다고 판단했습니다. 별도 Redis 인프라의 운영 복잡도 대비 이점이 제한적이라 Caffeine Cache를 선택했습니다.',
    aiUsage: '문제와 적용 범위를 먼저 정의한 뒤 AI 코딩 도구(Codex)를 활용해 병렬 처리 구현안을 빠르게 구체화했습니다. 생성된 코드는 동작 방식과 기존 서비스 구조의 적합성을 확인한 뒤 적용했습니다.',
    award: '2026-1 한성대학교 캡스톤디자인 작품우수상',
    links: [
      { label: 'Backend GitHub', url: 'https://github.com/hansung-2026-capstone/filly-backend', icon: Github },
      { label: '시연영상', url: 'https://www.youtube.com/watch?v=BMViDPydEdY', icon: Youtube }
    ],
    media: {
      slides: [
        { label: '메인', src: fillyImages.main, alt: 'Filly 메인 캘린더 화면' },
        { label: '일기 작성', src: fillyImages.writeDiary, alt: 'Filly 일기 작성 화면' },
        { label: '일기 상세', src: fillyImages.diaryDetail, alt: 'Filly 일기 상세 화면' },
        { label: '보관함', src: fillyImages.archives, alt: 'Filly 보관함 화면' },
        { label: '콘텐츠', src: fillyImages.contents, alt: 'Filly 콘텐츠 화면' },
        { label: '통계', src: fillyImages.stats, alt: 'Filly 통계 화면' },
        { label: '사원증', src: fillyImages.id_card, alt: 'Filly 사원증 컨텐츠', fit: 'contain' },
        { label: '시스템 아키텍처', src: fillyImages.systemArchitecture, alt: 'Filly 시스템 아키텍처', fit: 'contain' },
      ]
    }
  },
  {
    title: '사내 백오피스 OCR 자동화',
    period: '2025.08 ~ 2025.10',
    role: '서비스개발팀 인턴',
    stack: ['Spring Boot', 'JSP', 'Vue.js', 'MySQL', 'GitLab', 'OpenAI API'],
    summary: '천재교육 디지털사업본부 서비스개발팀에서 사내 백오피스 OCR 자동화 기능을 개발했습니다.',
    highlights: [
      'PDF 자동 캡처 로직과 OpenAI API 호출·응답 처리 로직 구현',
      'OCR 처리용 프롬프트를 설계하고 단계별 처리 지침과 제약조건을 구체화',
      '수동 캡처 후 영역별 OCR 요청 프로세스를 PDF 전체 캡처와 OCR이 이어지는 자동화 흐름으로 개선',
      '구현 기능이 인턴 종료 후 실제 사내 백오피스에 반영된 것을 담당 선임을 통해 확인'
    ],
    problem: '사용자가 PDF 영역을 직접 확인·캡처한 뒤 영역별 OCR을 요청해야 했고, 비정형 문서는 결과 편차가 발생했습니다.',
    solution: 'PDF 전체 캡처와 OCR 요청이 한 번의 기능 실행으로 이어지도록 구현하고, 비정형 문서의 결과 편차를 줄이기 위해 처리 절차·제약조건·가이드라인을 구체화했습니다. GPT-4o 등 모델별 결과도 검토했습니다.'
  },
  {
    title: 'AI 디지털 교과서 클론 프로젝트',
    period: '2025.06 ~ 2025.07',
    role: '백엔드 / 화면 개발',
    stack: ['Spring Boot', 'Thymeleaf', 'MyBatis', 'MySQL'],
    summary: '천재교육 Java 풀스택 부트캠프 최종 프로젝트로, AI 디지털 교과서의 일부 기능을 Spring Boot와 Thymeleaf 기반으로 클론 코딩했습니다.',
    highlights: [
      'Spring Boot 기반 웹 애플리케이션 구현',
      'Thymeleaf 기반 서버 사이드 렌더링 화면 구성',
      'MyBatis 기반 데이터 조회 및 처리',
      'MySQL 데이터베이스 연동',
      'Controller, Service, Mapper 계층을 통한 요청 처리 흐름 구현'
    ],
    problem: '화면 요구사항을 서버 로직과 데이터베이스 조회 구조로 연결하고, 조회된 데이터를 Thymeleaf 화면에 적절히 렌더링해야 했습니다.',
    solution: '사용자 요청이 Controller, Service, Mapper, DB를 거쳐 다시 Thymeleaf 화면으로 반환되는 SSR 기반 흐름을 구현하며 Spring Boot 웹 서비스 개발의 기본기를 다졌습니다.',
    media: {
      slides: [
        { label: '우리 반 수업', src: cjFinalProjectImages.classroom, alt: 'AI 디지털 교과서 클론 우리 반 수업 화면' },
        { label: '평가 문항 편집', src: cjFinalProjectImages.examEdit, alt: 'AI 디지털 교과서 클론 평가 문항 편집 화면' },
        { label: '평가 리포트', src: cjFinalProjectImages.examReport, alt: 'AI 디지털 교과서 클론 평가 리포트 화면' },
        { label: '학습 현황', src: cjFinalProjectImages.learningStatus, alt: 'AI 디지털 교과서 클론 학습 현황 화면' },
        { label: '시스템 아키텍처', src: cjFinalProjectImages.systemArchitecture, alt: 'AI 디지털 교과서 클론 시스템 아키텍처', fit: 'contain' }
      ]
    }
  }

];

const skills = [
  { icon: Server, label: 'Backend', items: ['Java', 'Spring Boot', 'Spring Security', 'Spring Data JPA', 'MyBatis'] },
  { icon: Database, label: 'Database', items: ['MySQL'] },
  { icon: ShieldCheck, label: 'Auth / Security', items: ['OAuth2', 'JWT'] },
  { icon: Cloud, label: 'Cloud / Infra', items: ['Docker', 'Google Cloud Run', 'Google Cloud Storage', 'Cloud SQL'] },
  { icon: Sparkles, label: 'AI / API', items: ['OpenAI API', 'Gemini API'] },
  { icon: Code2, label: 'Tools', items: ['Git', 'GitHub', 'GitLab', 'Swagger', 'IntelliJ IDEA', 'VS Code', 'DBeaver'] },
];

const activeMediaIndexes = ref({});
let mediaTimer;

const getMediaSlides = (project) => project.media?.slides ?? [];

const getActiveMediaIndex = (project) => activeMediaIndexes.value[project.title] ?? 0;

const moveMedia = (project, direction) => {
  const slides = getMediaSlides(project);
  if (!slides.length) return;

  activeMediaIndexes.value = {
    ...activeMediaIndexes.value,
    [project.title]: (getActiveMediaIndex(project) + direction + slides.length) % slides.length
  };
};

onMounted(() => {
  mediaTimer = window.setInterval(() => {
    projects
      .filter((project) => project.media?.slides?.length)
      .forEach((project) => moveMedia(project, 1));
  }, 5000);
});

onUnmounted(() => {
  window.clearInterval(mediaTimer);
});
</script>

<template>
  <main>
    <nav class="nav">
      <a href="#home" class="logo">KKM</a>
      <div>
        <a href="#skills">Skills</a>
        <a href="#experience">Experience</a>
        <a href="#projects">Projects</a>
        <a href="#contact">Contact</a>
      </div>
    </nav>

    <section id="home" class="hero">
      <div class="hero-text">
        <p class="tag">Backend Developer</p>
        <h1>문제를 분석하고 개선으로 <br> 증명하는 백엔드 개발자</h1>
        <p class="hero-desc">
          Spring Boot 기반 백엔드 개발을 중심으로 실제 업무의 반복 과정을 자동화하고,<br>
          서비스에서 발생한 성능 병목을 찾아 개선해왔습니다.
        </p>
        <div class="hero-actions">
          <a href="#projects" class="btn primary">프로젝트 보기</a>
          <a href="#contact" class="btn secondary">연락처 보기</a>
        </div>
      </div>
      <aside class="hero-card">
        <div class="profile-head">
          <img class="profile-photo" :src="profileImage" alt="강경민 프로필 사진" />
          <div>
            <h3>강경민</h3>
            <div class="basic-info">
              <span>
                <Server /> Backend Developer
              </span>
            </div>
          </div>
        </div>
        <div class="profile-meta">
          <div>
            <h4>
              <GraduationCap /> 교육
            </h4>
            <ul>
              <li>한성대학교 IT공과대학</li>
              <li>모바일소프트웨어트랙 / 웹공학트랙</li>
              <li>천재교육 서비스개발팀 인턴</li>
            </ul>
          </div>
          <div>
            <h4>
              <BadgeCheck /> 자격
            </h4>
            <ul>
              <li>정보처리기사 (2025.09.12)</li>
              <li>SQLD (2026.03.27)</li>
              <li>ADsP (2026.06.05)</li>
            </ul>
          </div>
        </div>
      </aside>
    </section>

    <section id="skills" class="section">
      <div class="section-title">
        <p>SKILLS</p>
        <h2>기술 스택</h2>
        <span>프로젝트와 실무 경험에서 사용한 기술입니다.</span>
      </div>
      <div class="skills-grid">
        <article class="skill-card" v-for="skill in skills" :key="skill.label">
          <div class="skill-icon">
            <component :is="skill.icon" />
          </div>
          <h3>{{ skill.label }}</h3>
          <div class="pill-wrap">
            <span class="pill" v-for="item in skill.items" :key="item">{{ item }}</span>
          </div>
        </article>
      </div>
    </section>

    <section id="experience" class="section highlight-section">
      <div class="section-title">
        <p>EXPERIENCE</p>
        <h2>실무 경험</h2>
        <span>사내 백오피스의 반복 업무를 자동화하는 기능을 구현했습니다.</span>
      </div>
      <div class="experience-card">
        <div>
          <p class="date">2025.08 ~ 2025.10</p>
          <h3>천재교육 디지털사업본부 서비스개발팀 · 인턴</h3>
          <p>
            Spring Boot, JSP, Vue.js, MySQL, GitLab, OpenAI API를 사용해<br>
            사내 백오피스 OCR 자동화 기능을 개발했습니다.
          </p>
        </div>
        <ul>
          <li>PDF 자동 캡처, OpenAI API 호출 및 응답 처리 로직 구현</li>
          <li>수동 캡처·영역별 OCR 요청을 PDF 전체 자동 캡처·OCR 흐름으로 개선</li>
          <li>단계별 처리 지침과 제약조건을 구체화하고 GPT-4o 등 모델별 결과 검토</li>
          <li>구현 기능이 인턴 종료 후 실제 사내 백오피스에 반영된 것을 담당 선임을 통해 확인</li>
        </ul>
      </div>
    </section>

    <section id="projects" class="section">
      <div class="section-title">
        <p>PROJECTS</p>
        <h2>주요 프로젝트</h2>
      </div>
      <div class="project-list">
        <article class="project-card" v-for="(project, idx) in projects" :key="project.title">
          <div class="project-header">
            <span class="number">0{{ idx + 1 }}</span>
            <div>
              <h3>{{ project.title }}</h3>
              <p>{{ project.period }} · {{ project.role }}</p>
            </div>
          </div>
          <p class="project-summary">{{ project.summary }}</p>
          <div class="pill-wrap stack">
            <span class="pill" v-for="item in project.stack" :key="item">{{ item }}</span>
          </div>
          <div class="project-links" v-if="project.links?.length">
            <a v-for="link in project.links" :key="link.url" :href="link.url" target="_blank" rel="noreferrer">
              <component :is="link.icon" />
              {{ link.label }}
            </a>
          </div>
          <div class="project-media" v-if="project.media">
            <div class="project-slider">
              <button class="slider-btn prev" type="button" aria-label="이전 이미지" @click="moveMedia(project, -1)">
                <ChevronLeft />
              </button>
              <div class="slider-viewport">
                <div class="slider-track" :style="{ transform: `translateX(-${getActiveMediaIndex(project) * 100}%)` }">
                  <figure v-for="(slide, slideIdx) in getMediaSlides(project)" :key="slide.label">
                    <img :class="{ contain: slide.fit === 'contain' }" :src="slide.src" :alt="slide.alt" />
                    <figcaption>
                      {{ slide.label }}
                      <span>{{ slideIdx + 1 }} / {{ getMediaSlides(project).length }}</span>
                    </figcaption>
                  </figure>
                </div>
              </div>
              <button class="slider-btn next" type="button" aria-label="다음 이미지" @click="moveMedia(project, 1)">
                <ChevronRight />
              </button>
            </div>
          </div>
          <div class="project-content">
            <div>
              <h4>주요 구현</h4>
              <ul>
                <li v-for="item in project.highlights" :key="item">{{ item }}</li>
              </ul>
            </div>
            <div class="problem-box">
              <h4>문제 해결</h4>
              <p><strong>문제:</strong> {{ project.problem }}</p>
              <p><strong>해결:</strong> {{ project.solution }}</p>
              <p v-if="project.result" class="performance-result"><strong>결과:</strong> {{ project.result }}</p>
              <p v-if="project.cacheDecision"><strong>캐시 선택:</strong> {{ project.cacheDecision }}</p>
              <p v-if="project.aiUsage"><strong>AI 코딩 도구 활용:</strong> {{ project.aiUsage }}</p>
              <p v-if="project.award" class="award"><strong>수상:</strong> {{ project.award }}</p>
            </div>
          </div>
        </article>
      </div>
    </section>

    <section id="contact" class="contact">
      <h2>문제를 발견하고 개선으로 증명하는 백엔드 개발자가 되겠습니다.</h2>
      <p>
        Spring Boot 기반 API 개발과 AI 기술을 활용해 반복되는 업무를 더 효율적인 시스템으로 바꾸겠습니다.
      </p>
      <div class="contact-links">
        <a href="mailto:wowkmini@naver.com">
          <Mail /> wowkmini@naver.com
        </a>
        <a href="https://github.com/KMKang01" target="_blank" rel="noreferrer">
          <Github /> GitHub
        </a>
      </div>
    </section>
  </main>
</template>
