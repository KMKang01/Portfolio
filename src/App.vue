<script setup>
import { ref } from 'vue';
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
    solution: 'Signed URL 유효기간 1시간에 맞춰 Caffeine Cache TTL을 50분, 최대 저장 개수는 10,000개로 설정했습니다. 반복 요청은 캐시의 Signed URL을 재사용하고, 최초 캐시 미스는 CompletableFuture + ExecutorService로 여러 Signed URL을 병렬 생성했습니다.',
    result: '메인 페이지 최초 로딩 약 12초 → 1~2초',
    cacheDecision: 'Cloud Run은 최대 3개 인스턴스로 확장될 수 있어 local cache가 인스턴스 간 공유되지 않는 한계가 있었지만, Signed URL은 재생성 가능한 파생 데이터이므로 데이터 정합성에 영향을 주지 않는다고 판단했습니다. 별도 Redis 인프라의 운영 복잡도 대비 이점이 제한적이라 Caffeine Cache를 선택했습니다.',
    award: '2026-1 한성대학교 캡스톤디자인 작품우수상',
    links: [
      { label: 'Backend GitHub', url: 'https://github.com/hansung-2026-capstone/filly-backend', icon: Github },
      { label: '시연영상', url: 'https://www.youtube.com/watch?v=BMViDPydEdY', icon: Youtube }
    ],
    media: {
      slides: [
        { label: '메인', src: fillyImages.main, alt: 'Filly 메인 캘린더 화면' },
        { label: '일기 작성', src: fillyImages.writeDiary, alt: 'Filly 일기 작성 화면' },
        { label: '보관함', src: fillyImages.archives, alt: 'Filly 보관함 화면' },
        { label: '콘텐츠', src: fillyImages.contents, alt: 'Filly 콘텐츠 화면' },
        { label: '통계', src: fillyImages.stats, alt: 'Filly 통계 화면' },
        { label: '사원증', src: fillyImages.id_card, alt: 'Filly 사원증 컨텐츠', fit: 'contain' },
        { label: '시스템 아키텍처', src: fillyImages.systemArchitecture, alt: 'Filly 시스템 아키텍처', fit: 'contain' },
      ]
    }
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
    caseTitle: '구현 과정',
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

const featuredProject = projects[0];
const otherProjects = [projects[1]];

const activeMediaIndexes = ref({});
const selectedImage = ref(null);

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

const openImage = (slide) => {
  selectedImage.value = slide;
};

const closeImage = () => {
  selectedImage.value = null;
};

</script>

<template>
  <main class="screen-layout">
    <nav class="nav"><div class="site-frame nav-frame"><a href="#home" class="logo">KKM</a><div class="nav-links"><a href="#experience">Experience</a><a href="#projects">Projects</a><a href="#skills">Skills</a><a href="#contact">Contact</a></div><div class="nav-mobile"><a href="#projects">Projects</a><a href="https://github.com/KMKang01" target="_blank" rel="noreferrer">GitHub</a></div></div></nav>

    <section id="home" class="hero site-frame">
      <div class="hero-text">
        <p class="tag">Backend Developer</p>
        <h1>문제를 분석하고 개선으로 <br> 증명하는 백엔드 개발자</h1>
        <p class="hero-desc">
          Spring Boot 기반 백엔드 개발을 중심으로 실제 업무의 반복 과정을 자동화하고,<br>
          서비스에서 발생한 성능 병목을 찾아 개선해왔습니다.
        </p>
        <div class="hero-actions">
          <a href="#projects" class="hero-primary-action">프로젝트 보기</a>
          <a href="https://github.com/KMKang01" class="hero-github-link" target="_blank" rel="noopener noreferrer"><Github /><span>GitHub</span><span aria-hidden="true">↗</span></a>
        </div>
      </div>
      <aside class="hero-card">
        <div class="profile-head">
          <img class="profile-photo" :src="profileImage" alt="강경민 프로필 사진" />
          <div>
            <h3>강경민</h3>
            <p>Backend Developer</p>
          </div>
        </div>
        <div class="profile-meta">
          <div>
            <h4>교육</h4>
            <ul>
              <li>한성대학교 IT공과대학</li>
              <li>모바일소프트웨어트랙 / 웹공학트랙</li>
            </ul>
          </div>
          <div>
            <h4>자격</h4>
            <ul>
              <li>정보처리기사 (2025.09.12)</li>
              <li>SQLD (2026.03.27)</li>
              <li>ADsP (2026.06.05)</li>
            </ul>
          </div>
        </div>
      </aside>
    </section>

    <section id="experience" class="section experience-section">
      <div class="section-title">
        <h2>실무 경험</h2><span>사내 백오피스의 반복 업무를 자동화하는 기능을 구현했습니다.</span>
      </div>
      <div class="experience-card">
        <div>
          <p class="date">2025.08 ~ 2025.10</p>
          <h3>천재교육<br>서비스개발팀 인턴</h3>
          <p>
            Spring Boot, JSP, Vue.js, MySQL, GitLab, OpenAI API를 사용해<br>
            사내 백오피스 OCR 자동화 기능을 개발했습니다.
          </p>
        </div>
        <ul>
          <li>PDF 자동 캡처, OpenAI API 호출 및 응답 처리 로직 구현</li>
          <li>수동 캡처·영역별 OCR 요청을 PDF 전체 자동 캡처·OCR 흐름으로 개선</li>
          <li>단계별 처리 지침과 제약조건을 구체화하고, GPT-4o 등 모델별 결과를 검토</li>
          <li>구현 기능이 인턴 종료 후 실제 사내 백오피스에 반영된 것을 담당 선임을 통해 확인</li>
        </ul>
      </div>
    </section>

    <section id="projects" class="section featured-section">
      <div class="section-title">
        <h2>Filly</h2><span>AI 기반 개인 일기 생성 서비스</span>
      </div>
      <article class="project-card featured-project">
          <div class="featured-topline"><span>2026.03 ~ 2026.06</span><span>Team Leader · Backend · Infrastructure</span></div>
          <div class="featured-intro"><div><p class="project-summary">{{ featuredProject.summary }}</p><p class="project-tech">{{ featuredProject.stack.join(' · ') }}</p></div><div class="performance-kpi"><span>메인 페이지 최초 이미지 로딩</span><strong>약 12초 → 1~2초</strong></div></div>
          <div class="project-links"><a v-for="link in featuredProject.links" :key="link.url" :href="link.url" target="_blank" rel="noreferrer">{{ link.label }} ↗</a></div>
          <div class="project-media" v-if="featuredProject.media"><div class="project-slider"><button class="slider-btn prev" type="button" aria-label="이전 이미지" @click="moveMedia(featuredProject, -1)"><ChevronLeft /></button><div class="slider-viewport"><div class="slider-track" :style="{ transform: `translateX(-${getActiveMediaIndex(featuredProject) * 100}%)` }"><figure v-for="(slide, slideIdx) in getMediaSlides(featuredProject)" :key="slide.label"><img :class="{ contain: slide.fit === 'contain' }" :src="slide.src" :alt="slide.alt" loading="lazy" role="button" tabindex="0" @click="openImage(slide)" @keydown.enter="openImage(slide)" @keydown.space.prevent="openImage(slide)"/><figcaption>{{ slide.label }}<span>{{ slideIdx + 1 }} / {{ getMediaSlides(featuredProject).length }}</span></figcaption></figure></div></div><button class="slider-btn next" type="button" aria-label="다음 이미지" @click="moveMedia(featuredProject, 1)"><ChevronRight /></button></div></div>
          <div class="project-content featured-content"><div><h4>주요 구현</h4><ul><li v-for="item in featuredProject.highlights" :key="item">{{ item }}</li></ul></div><div class="problem-box"><h4>성능 개선 — Signed URL 생성 병목</h4><p class="flow-label">원인</p><p>{{ featuredProject.problem }}</p><p class="flow-label">개선</p><p>{{ featuredProject.solution }}</p><p class="flow-label">결과</p><p class="performance-result">{{ featuredProject.result }}</p><p class="flow-label">기술 선택</p><p>{{ featuredProject.cacheDecision }}</p><p class="award">{{ featuredProject.award }}</p></div></div>
      </article>
    </section>

    <section id="skills" class="section skills-section">
      <div class="section-title"><h2>기술 스택</h2><span>프로젝트와 실무 경험에서 사용한 기술입니다.</span></div>
      <div class="skills-grid"><article class="skill-card" v-for="skill in skills" :key="skill.label"><h3>{{ skill.label }}</h3><p>{{ skill.items.join(' · ') }}</p></article></div>
    </section>

    <section class="section other-projects">
      <div class="section-title"><h2>추가 프로젝트</h2></div>
      <div class="project-list">
        <article class="project-card" v-for="(project, idx) in otherProjects" :key="project.title">
          <div class="project-header">
            <div>
              <h3>{{ project.title }}</h3>
              <p>{{ project.period }} · {{ project.role }}</p>
            </div>
          </div>
          <p class="project-summary">{{ project.summary }}</p>
          <p class="project-tech">{{ project.stack.join(' · ') }}</p>
          <div class="project-links" v-if="project.links?.length">
            <a v-for="link in project.links" :key="link.url" :href="link.url" target="_blank" rel="noreferrer">
              {{ link.label }} ↗
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
                    <img loading="lazy"
                      :class="{ contain: slide.fit === 'contain' }"
                      :src="slide.src"
                      :alt="slide.alt"
                      role="button"
                      tabindex="0"
                      @click="openImage(slide)"
                      @keydown.enter="openImage(slide)"
                      @keydown.space.prevent="openImage(slide)"
                    />
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
              <h4>{{ project.caseTitle ?? '문제 해결' }}</h4>
              <p><strong>문제:</strong> {{ project.problem }}</p>
              <p><strong>해결:</strong> {{ project.solution }}</p>
              <p v-if="project.result" class="performance-result"><strong>결과:</strong> {{ project.result }}</p>
              <p v-if="project.cacheDecision"><strong>캐시 선택:</strong> {{ project.cacheDecision }}</p>
              <p v-if="project.award" class="award"><strong>수상:</strong> {{ project.award }}</p>
            </div>
          </div>
        </article>
      </div>
    </section>

    <div v-if="selectedImage" class="image-lightbox" role="dialog" aria-modal="true" :aria-label="`${selectedImage.label} 이미지 확대 보기`" @click.self="closeImage">
      <button class="lightbox-close" type="button" aria-label="이미지 확대 닫기" @click="closeImage">×</button>
      <img :src="selectedImage.src" :alt="selectedImage.alt" />
    </div>

    <section id="contact" class="contact">
      <div class="contact-inner">
        <div><h2>강경민</h2><p>Backend Developer</p></div>
        <div class="contact-links"><a href="mailto:wowkmini@naver.com">wowkmini@naver.com</a><a href="https://github.com/KMKang01" target="_blank" rel="noreferrer">GitHub ↗</a></div>
      </div>
    </section>
  </main>

  <section class="print-document print-only" aria-label="강경민 백엔드 개발자 포트폴리오">
    <section class="print-page print-profile">
      <header class="print-identity">
        <div>
          <p class="print-eyebrow">BACKEND DEVELOPER PORTFOLIO</p>
          <h1>문제를 분석하고 개선으로<br>증명하는 백엔드 개발자</h1>
          <p>Spring Boot 기반 백엔드 개발을 중심으로 실제 업무의 반복 과정을 자동화하고, 서비스에서 발생한 성능 병목을 찾아 개선해왔습니다.</p>
        </div>
        <div class="print-profile-card">
          <img :src="profileImage" alt="강경민 프로필 사진" />
          <div>
            <strong>강경민</strong>
            <span>Backend Developer</span>
            <a href="mailto:wowkmini@naver.com">wowkmini@naver.com</a>
            <a href="https://github.com/KMKang01">GitHub</a>
          </div>
        </div>
      </header>
      <div class="print-profile-details">
        <div>
          <h2>교육</h2>
          <p>한성대학교 IT공과대학<br>모바일소프트웨어트랙 / 웹공학트랙</p>
        </div>
        <div>
          <h2>자격</h2>
          <p>정보처리기사 (2025.09.12)<br>SQLD (2026.03.27)<br>ADsP (2026.06.05)</p>
        </div>
      </div>
      <section class="print-skills">
        <div class="print-section-heading"><p>SKILLS</p><h2>기술 스택</h2></div>
        <div class="print-skills-grid">
          <article v-for="skill in skills" :key="`print-${skill.label}`">
            <h3>{{ skill.label }}</h3>
            <p>{{ skill.items.join(' · ') }}</p>
          </article>
        </div>
      </section>
    </section>

    <section class="print-page print-experience">
      <div class="print-section-heading"><p>EXPERIENCE</p><h2>실무 경험</h2></div>
      <article class="print-experience-card">
        <div class="print-project-meta"><span>2025.08 ~ 2025.10</span><span>서비스개발팀 인턴</span></div>
        <h3>천재교육 디지털사업본부 서비스개발팀</h3>
        <p class="print-lead">Spring Boot, JSP, Vue.js, MySQL, GitLab, OpenAI API를 사용해 사내 백오피스 OCR 자동화 기능을 개발했습니다.</p>
        <div class="print-two-column">
          <div><h4>핵심 담당 업무</h4><ul><li>PDF 자동 캡처, OpenAI API 호출 및 응답 처리 로직 구현</li><li>수동 캡처·영역별 OCR 요청을 PDF 전체 자동 캡처·OCR 흐름으로 개선</li></ul></div>
          <div><h4>품질 개선</h4><ul><li>단계별 처리 지침과 제약조건을 구체화하고, GPT-4o 등 모델별 결과를 검토</li><li>구현 기능이 인턴 종료 후 실제 사내 백오피스에 반영된 것을 담당 선임을 통해 확인</li></ul></div>
        </div>
      </article>
    </section>

    <section class="print-page print-project-page">
      <div class="print-project-heading"><p>01 · PROJECT</p><h2>{{ projects[0].title }}</h2><div class="print-project-meta"><span>{{ projects[0].period }}</span><span>{{ projects[0].role }}</span></div><p class="print-lead">{{ projects[0].summary }}</p><div class="print-tags"><span v-for="item in projects[0].stack" :key="`filly-tag-${item}`">{{ item }}</span></div><div class="print-links"><a v-for="link in projects[0].links" :key="`print-${link.url}`" :href="link.url">{{ link.label }}</a></div></div>
      <div class="print-project-gallery print-gallery-four">
        <figure v-for="slide in getMediaSlides(projects[0]).slice(0, 4)" :key="`print-filly-overview-${slide.label}`"><img :src="slide.src" :alt="slide.alt"><figcaption>{{ slide.label }}</figcaption></figure>
      </div>
    </section>

    <section class="print-page print-project-page">
      <div class="print-section-heading"><p>01 · FILLY</p><h2>핵심 화면과 주요 구현</h2></div>
      <div class="print-project-gallery print-gallery-two">
        <figure v-for="slide in [getMediaSlides(projects[0])[4], getMediaSlides(projects[0])[6]]" :key="`print-filly-detail-${slide.label}`" :class="{ 'print-architecture': slide.fit === 'contain' }"><img :src="slide.src" :alt="slide.alt"><figcaption>{{ slide.label }}</figcaption></figure>
      </div>
      <div class="print-implementation"><h3>주요 구현</h3><ul><li v-for="item in projects[0].highlights" :key="`print-filly-highlight-${item}`">{{ item }}</li></ul></div>
    </section>

    <section class="print-page print-project-page print-filly-case">
      <div class="print-section-heading"><p>01 · FILLY</p><h2>문제 해결</h2></div>
      <div class="print-case-grid">
        <article><h3>문제</h3><p>{{ projects[0].problem }}</p></article>
        <article><h3>해결</h3><p>{{ projects[0].solution }}</p></article>
        <article class="print-result"><h3>결과</h3><p>{{ projects[0].result }}</p></article>
        <article><h3>기술 선택 근거</h3><p>{{ projects[0].cacheDecision }}</p></article>
        <article class="print-award"><h3>성과</h3><p>{{ projects[0].award }}</p></article>
      </div>
    </section>

    <section class="print-page print-project-page">
      <div class="print-project-heading"><p>02 · PROJECT</p><h2>{{ otherProjects[0].title }}</h2><div class="print-project-meta"><span>{{ otherProjects[0].period }}</span><span>{{ otherProjects[0].role }}</span></div><p class="print-lead">{{ otherProjects[0].summary }}</p><div class="print-tags"><span v-for="item in otherProjects[0].stack" :key="`textbook-tag-${item}`">{{ item }}</span></div></div>
      <div class="print-project-gallery print-gallery-four">
        <figure v-for="slide in getMediaSlides(otherProjects[0]).slice(0, 4)" :key="`print-textbook-overview-${slide.label}`"><img :src="slide.src" :alt="slide.alt"><figcaption>{{ slide.label }}</figcaption></figure>
      </div>
    </section>

    <section class="print-page print-project-page print-final-page">
      <div class="print-section-heading"><p>02 · AI 디지털 교과서 클론 프로젝트</p><h2>구현 과정</h2></div>
      <div class="print-project-gallery print-gallery-architecture"><figure><img :src="getMediaSlides(otherProjects[0])[4].src" :alt="getMediaSlides(otherProjects[0])[4].alt"><figcaption>{{ getMediaSlides(otherProjects[0])[4].label }}</figcaption></figure></div>
      <div class="print-two-column"><div class="print-implementation"><h3>주요 구현</h3><ul><li v-for="item in otherProjects[0].highlights" :key="`print-textbook-highlight-${item}`">{{ item }}</li></ul></div><div class="print-ocr-case"><h3>{{ otherProjects[0].caseTitle }}</h3><h4>문제</h4><p>{{ otherProjects[0].problem }}</p><h4>해결</h4><p>{{ otherProjects[0].solution }}</p></div></div>
      <footer class="print-contact"><strong>서비스의 안정성과 유지보수성을 함께 고민하는 백엔드 개발자가 되겠습니다.</strong><span><a href="mailto:wowkmini@naver.com">wowkmini@naver.com</a> · <a href="https://github.com/KMKang01">GitHub</a></span></footer>
    </section>
  </section>
</template>
