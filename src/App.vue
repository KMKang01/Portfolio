<script setup>
import { onMounted, onUnmounted, ref } from 'vue';
import {
  Mail,
  Calendar,
  Server,
  Database,
  Cloud,
  Sparkles,
  Code2,
  Github,
  Youtube,
  UserRound,
  ShieldCheck,
  GraduationCap,
  BadgeCheck,
  ChevronLeft,
  ChevronRight
} from 'lucide-vue-next';

const profileImage = new URL('./static/images/profile/IMG_5490-25 (일반사진).jpg', import.meta.url).href;
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
    role: '팀장 / 백엔드 / 인프라 담당',
    stack: ['Spring Boot', 'MySQL', 'GCP Cloud Run', 'Firebase Hosting', 'React', 'TanStack Query', 'Tailwind CSS', 'Gemini API', 'OAuth'],
    summary: '사용자가 짧은 문장과 이미지를 기반으로 일기를 쉽게 작성할 수 있도록 돕는 AI 일기 생성 서비스입니다.',
    highlights: [
      'OAuth 기반 소셜 로그인 및 사용자별 일기 데이터 저장 구조 설계',
      'Gemini API 연동을 통한 AI 일기 초안 생성 기능 구현',
      'GCP Bucket 기반 이미지 저장 및 Signed URL 접근 처리',
      'GCP Cloud Run 기반 백엔드 배포와 프론트엔드 배포 환경 구성'
    ],
    problem: '메인 페이지에서 여러 이미지 조회 시 Signed URL을 반복 생성하며 로딩이 지연되는 문제가 발생했습니다.',
    solution: 'Caffeine Cache를 적용해 Signed URL을 캐싱하고, 최초 생성 시 병렬 처리를 적용해 불필요한 오버헤드를 줄였습니다. 프로젝트 규모와 단일 서버 운영 환경을 고려해 Redis 대신 애플리케이션 내부 캐시를 선택했습니다.',
    links: [
      { label: 'GitHub', url: 'https://github.com/hansung-2026-capstone', icon: Github },
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
    title: '천재교육 서비스개발팀 인턴 — 백오피스 OCR 고도화',
    period: '2025.08 ~ 2025.10',
    role: '서비스개발팀 인턴',
    stack: ['Spring Boot', 'Thymeleaf', 'MySQL', 'GitLab', 'OpenAI API'],
    summary: '천재교육 디지털사업본부 서비스개발팀에서 실무 개발 환경과 협업 방식을 경험했습니다.',
    highlights: [
      '천재교육 백오피스 고도화 작업 참여',
      'OpenAI API 기반 OCR 처리 기능 담당',
    ],
    problem: '문서 영역이 정형화되어 있지 않아 자동 캡처 정확도가 떨어지고, API 요청 비용과 처리 시간도 함께 고려해야 했습니다.',
    solution: '프롬프트 제약 조건을 세분화하고 GPT-4o-mini, GPT-4-turbo 등 모델별 결과를 비교하며 정확도와 비용 효율성의 균형을 맞추는 방향으로 개선했습니다.'
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
  { icon: Server, label: 'Backend', items: ['Java', 'Spring', 'Spring Data JPA', 'Spring Boot', 'MyBatis'] },
  { icon: Code2, label: 'Frontend', items: ['Vue.js', 'JSP', 'JavaScript', 'TypeScript'] },
  { icon: Database, label: 'Database', items: ['MySQL', 'PostgreSQL', 'MongoDB'] },
  { icon: Cloud, label: 'Infra / DevOps', items: ['AWS EC2', 'GCP Cloud Run', 'Vercel', 'GitHub Actions'] },
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
        <p class="tag">Backend / Platform Developer</p>
        <h1>더 나은 내일을 위해 배우는 <br> 백엔드 개발자</h1>
        <p class="hero-desc">
          Spring Boot 기반 백엔드 개발을 중심으로 사용자 데이터 저장, API 연동, 인증, 클라우드 배포,
          성능 개선 경험을 쌓아왔습니다.
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
                <Calendar /> 2001.07.02
              </span>
              <span>
                <UserRound /> 남자
              </span>
              <span>
                <ShieldCheck /> 군필
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
              <li>천재교육 Java 풀스택 10기 · 2024.12 ~ 2025.07</li>
              <li>한성대학교 컴퓨터공학부 · 2020.03 ~ 재학중</li>
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
        <span>천재교육 서비스개발팀 인턴으로 실무 개발 환경을 경험했습니다.</span>
      </div>
      <div class="experience-card">
        <div>
          <p class="date">2025.08 ~ 2025.10</p>
          <h3>천재교육 디지털사업본부 서비스개발팀 인턴</h3>
          <p>
            Vue.js와 Spring Boot 기반 클래스보드 클론 프로젝트를 진행했고, 이후 백오피스 고도화 작업에서
            OpenAI API 기반 OCR 처리 기능을 담당했습니다.
          </p>
        </div>
        <ul>
          <li>문서 업로드 후 자동 캡처 및 OCR 처리 흐름 구현 참여</li>
          <li>프롬프트 제약 조건 설계 및 모델별 결과 비교</li>
          <li>AI API 연동 시 정확도, 처리 시간, 비용 효율성 고려</li>
        </ul>
      </div>
    </section>

    <section id="projects" class="section">
      <div class="section-title">
        <p>PROJECTS</p>
        <h2>주요 프로젝트</h2>
        <!-- <span>AiTStory 플랫폼 개발 직무와 연결되는 프로젝트 중심으로 정리했습니다.</span> -->
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
            </div>
          </div>
        </article>
      </div>
    </section>

    <section id="contact" class="contact">
      <h2>사용자 데이터 기반 플랫폼 개발에 기여하고 싶습니다.</h2>
      <p>
        Spring Boot 기반 API 개발, AI API 연동, 인증, 클라우드 배포, 성능 개선 경험을 바탕으로
        안정적인 플랫폼 개발자가 되겠습니다.
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
