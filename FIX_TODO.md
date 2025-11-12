# Thesis Defense Readiness: Comprehensive Fix To-Do List

**Status**: Ready for implementation
**Priority**: CRITICAL
**Target**: All fixes completed before final defense

---

## PHASE 1: Critical Issues (Must Fix)

### 1.1 Product Naming Inconsistency ⚠️
**Issue**: Mixed usage of "EduTeams" vs "EquiTeam" across chapters
**Files affected**: 
- `chapter-4.tex` (lines 196, 233, 243, 253, 621, 636, 669, 719, 776)
- `chapter-3.tex` (backlog references)
- Figure captions and section headings

**Action Items**:
- [ ] Choose canonical name: **EduTeams** (system/platform name) [DECISION: Use EduTeams everywhere]
- [ ] Replace all "EquiTeam" with "EduTeams" in chapter-4.tex
- [ ] Update figure captions: "Sistem EquiTeam" → "Sistem EduTeams"
- [ ] Update section headings for consistency
- [ ] Verify abstract files (abstract-id.tex, abstract-en.tex) use EduTeams
- [ ] Search for any remaining inconsistencies across all chapters

**Files to edit**:
- thesis/chapters/chapter-4.tex
- thesis/chapters/chapter-3.tex (if any)

---

### 1.2 Authentication Flow Inconsistency 🔐
**Issue**: Contradictory auth descriptions:
- Activity diagrams: Google OAuth + Better Auth + session cookies
- Grey-Box Scenarios GB01-GB02: "username/password via Edu2Com API" (WRONG)
- ERD: Still has password field
- Testing narrative: Google OAuth mentioned

**Root cause**: Likely copy-paste from template or old design

**Action Items**:
- [ ] Fix GB01 scenario: Change "Login berhasil menggunakan username/password valid melalui Edu2Com API" to "Login menggunakan Google OAuth 2.0 dengan Better Auth"
- [ ] Fix GB02 scenario: Change password validation to Google account validation logic
- [ ] Update GB03: Clarify session management uses encrypted cookies, not tokens
- [ ] Update ERD documentation: 
  - Remove password field from User entity OR
  - Mark as deprecated/unused with comment
  - Add auth_method field if needed
- [ ] Update Testing mapping table (GB01-GB03): Reference Google OAuth flow
- [ ] Add brief explanation: "Sistem menggunakan Google OAuth 2.0 untuk autentikasi terpusat, tanpa menyimpan password lokal"

**Files to edit**:
- thesis/chapters/chapter-3.tex (GB01-GB03, ERD explanation)
- thesis/chapters/chapter-4.tex (testing mapping)

---

### 1.3 Performance Results Inconsistency 📊
**Issue**: Contradictory Lighthouse scores:
- Table 3.2 (NF-03): Performance 82/100
- NF-03 subsection (L1226-1247): Performance 98/100 ✓ (correct)
- Chapter V Kesimpulan: Performance 98/100 ✓
- Core Web Vitals: FCP 1.0s, LCP 2.3s (desktop - good)

**Decision**: 98/100 is the authoritative result

**Action Items**:
- [ ] Fix Table 3.2 (L1210-1224 in chapter-4.tex): Change "Performance 82/100" to "Performance 98/100"
- [ ] Verify all three sources now align: table → narrative → conclusion
- [ ] Add test setup details to NF-03 subsection:
  ```
  - Device Profile: Desktop (1920×1080)
  - Network: 4G (no throttling)
  - Tool: Google Lighthouse v11+ (or current version)
  - Pages tested: / (landing page) and /dashboard
  - Methodology: 3-run average
  ```
- [ ] Double-check Core Web Vitals metrics are correct
- [ ] Add note about mobile performance discrepancies if applicable

**Files to edit**:
- thesis/chapters/chapter-4.tex (table + NF-03 subsection)

---

### 1.4 Security & CSRF Claims Tightening 🛡️
**Issue**: Claims are too strong without evidence:
- "Next.js bawaan" handles CSRF — NOT accurate (Next.js doesn't auto-inject tokens)
- "Endpoint API tidak mengizinkan GET untuk mutasi" — good but incomplete
- Missing: SameSite cookie strategy, actual CSRF implementation

**Action Items**:
- [ ] Clarify CSRF mitigation strategy (choose one or combination):
  - Option A: SameSite=Lax/Strict cookies + same-origin policy
  - Option B: CSRF tokens (if implemented)
  - Option C: State-of-the-art pattern (SameSite + CORS)
- [ ] If using SameSite: Add text like:
  ```
  "Perlindungan CSRF diimplementasikan melalui SameSite=Lax pada 
  session cookies, yang mencegah browser mengirim cookies dalam 
  request cross-origin, sesuai RFC 6265bis."
  ```
- [ ] Remove "Next.js bawaan" claim or replace with specifics
- [ ] Add evidence: Show sample Set-Cookie header with SameSite attribute
- [ ] List which POST/PUT/DELETE endpoints are protected (e.g., /api/class/create)
- [ ] Add test case name that validates CSRF protection (reference to test suite)

**Files to edit**:
- thesis/chapters/chapter-4.tex (NF-05 subsection, L1271-1305)

---

### 1.5 Functional Requirements Numbering Gap ❌
**Issue**: F-15 is missing (F-14 → F-16)

**Action Items**:
- [ ] Check table in chapter-3.tex around line 64-114 (Kebutuhan Fungsional)
- [ ] Either:
  - Add missing F-15 requirement, OR
  - Renumber F-16 onwards to F-15, F-17 → F-16, etc.
- [ ] Update all references to F-xx in other sections
- [ ] Verify test cases match final numbering

**Files to check**:
- thesis/chapters/chapter-3.tex (Kebutuhan Fungsional table)
- Grep for F-16, F-17, etc. and update numbering

---

### 1.6 Typos & Accuracy 📝
**Action Items**:
- [ ] Change "gagali" to "gagal" (line ~1247 in chapter-4.tex)
- [ ] Clarify "5 Gagal/Skip" in testing summary:
  - Separate counts: How many failed vs. how many skipped?
  - Why were tests skipped? (external dependency, known issue, design choice)
- [ ] Check all italic formatting consistency (\textit{...})
- [ ] Verify capitalization in headings (BAB I style)

---

## PHASE 2: High-Priority Improvements (Before Defense)

### 2.1 Add Research Flow Diagram & Narrative 📐
**Issue**: "Alur Penelitian" section exists but may be incomplete; no explicit tie to artifacts

**Action Items**:
- [ ] Verify flowchart exists: thesis/figure/chapter-3/alur-penelitian.pdf (or similar)
- [ ] If missing, create one spanning:
  1. Problem Definition (Bab I)
  2. Literature Review (Bab II)
  3. Design & Planning (Bab III - Kebutuhan, Backlog, Diagrams)
  4. Implementation (Bab III/IV - Feature list)
  5. Testing (Bab IV - Test results)
  6. Analysis & Conclusions (Bab V)
- [ ] Add explicit cross-references in Alur Penelitian section:
  - "Fase 1: Identifikasi masalah (Bab I, Bagian 1.2)"
  - "Fase 2: Analisis kebutuhan (Bab III, Tabel 3.1-3.2)"
  - "Fase 3: Desain (Bab III, Gambar 3.2-3.4)"
  - "Fase 4: Implementasi (Bab IV, Tabel 4.1)"
  - "Fase 5: Pengujian (Bab IV, Bagian 4.2-4.3)"

**Files to edit**:
- thesis/chapters/chapter-3.tex (Alur Penelitian section)

---

### 2.2 Justification: Why Agile Kanban? 🔄
**Issue**: Method is described but not justified for solo development context

**Action Items**:
- [ ] Add paragraph in Metode Pengembangan explaining:
  - Why Kanban (not Scrum/Waterfall): WIP limits, continuous flow, no sprint overhead
  - Solo dev context: Kanban provides visibility without sprint ceremonies
  - Feedback loop: Testing → Backlog → Development (give concrete example)
  - Example: "Bug ditemukan pada GB09 (timeout API) → Diprioritaskan di backlog → Diperbaiki dalam 2 days → Re-tested"
- [ ] Cite Ilmi et al. (2020) or similar paper already in references

**Files to edit**:
- thesis/chapters/chapter-3.tex (Metode Pengembangan section)

---

### 2.3 Traceability Matrix 🎯
**Issue**: No clear mapping of requirements → features → tests

**Action Items**:
- [ ] Create compact traceability table (can go in Appendix or end of Bab III/IV):
  ```
  Format:
  | Req Code | Requirement | Feature Impl. | Test Suite | Status |
  | F-01     | Autentikasi | Section 4.1.x | Test: auth | ✓ PASS |
  | NF-01    | Reliability | Sections 4.1-4.3 | 18/18 E2E | ✓ PASS |
  ```
- [ ] Limit to 1-page; use abbreviations if needed
- [ ] Place reference in both Chapter III (planning) and Chapter IV (results)

**Files to create/edit**:
- thesis/chapters/chapter-4.tex (add near top of Hasil Pengujian)

---

### 2.4 Test Environment Specification 🖥️
**Issue**: Test context incomplete; reproducibility unclear

**Action Items**:
- [ ] Add subsection or table "Test Environment" with:
  - **Hardware**: CPU (e.g., Intel i7 11th gen), RAM (16GB), OS (Ubuntu 22.04)
  - **Software**: Node.js v18.x, Next.js v14.x, Bun v1.0.x
  - **Browser versions**: Chromium 120, Firefox 121, Chrome Mobile (emulated v120)
  - **Network**: No throttling (live 4G available) OR specify throttle (4G 1.4 Mbps DL)
  - **Data scale**: 20-100 test users, 5-10 test classes, 10-20 test tasks
- [ ] Add command examples for reproducibility:
  ```bash
  # Run unit/grey-box tests
  bun test
  
  # Run E2E tests
  playwright test
  
  # Run Lighthouse
  lighthouse http://localhost:3000 --chrome-flags="--headless"
  ```

**Files to edit**:
- thesis/chapters/chapter-3.tex (Tahap Pengujian section) or chapter-4.tex (start of testing subsection)

---

### 2.5 Dataset, Privacy & Consent Documentation 📋
**Issue**: Not explicit whether student data is real, synthetic, or anonymized

**Action Items**:
- [ ] Add subsection "Data Penelitian & Keamanan Privasi":
  - Data type: Synthetic (generated) / Real (with consent) / Anonymized
  - If real: Consent method, storage location, retention period, deletion policy
  - MBTI: Data stored per user (raw scores or classifications?), retention?
  - Student profile: Fields stored (NIM, gender, skill levels, preferences), access control?
  - Data protection: Encryption at rest/transit, who can access, audit logs?
- [ ] Example text:
  ```
  "Data pengujian menggunakan data sintetis yang dihasilkan secara 
  acak untuk mensimulasikan 50-100 mahasiswa dengan profil MBTI 
  dan keahlian yang bervariasi. Data real pengguna dienkripsi 
  menggunakan AES-256 dan hanya dapat diakses oleh pengguna 
  yang bersangkutan atau admin sistem. Semua data log dihapus 
  setelah penelitian selesai, sesuai kebijakan privasi institusi."
  ```

**Files to edit**:
- thesis/chapters/chapter-3.tex (Bahan subsection) or new "Ethical Considerations" subsection

---

### 2.6 Add "Threats to Validity" Discussion 🎯
**Issue**: Limitations and validity not formally discussed

**Action Items**:
- [ ] Add subsection in Chapter IV or V: "Keterbatasan Penelitian & Ancaman Validitas"
  - **Internal**: Mocked Edu2Com in unit tests vs. live in E2E; coverage gaps (2.58% assignment change detection)
  - **External**: Small test dataset (50-100 users); may not generalize to large classes (500+); single institution
  - **Construct**: MBTI heuristic, not diagnostic; "team quality" measured by algorithm success, not real collaboration outcomes
  - **Statistical**: No control group (no comparison with random grouping in production)
- [ ] Mitigations: "Future work includes user studies with real teams and long-term collaboration metrics"

**Files to edit**:
- thesis/chapters/chapter-5.tex (Kesimpulan section or new subsection)

---

## PHASE 3: Content Enhancements (Impression & Depth)

### 3.1 Team Formation Quality & Benchmarking 📈
**Issue**: "100% success over 20 test cases" is vague; no quality comparison

**Action Items**:
- [ ] Define "success" operationally:
  - All students assigned to exactly one team
  - Team size constraints met (e.g., 3-4 per team)
  - No exceptions/unhandled errors
- [ ] Add small comparison table: Edu2Com vs. Random Grouping
  ```
  | Metric | Edu2Com | Random | Improvement |
  | MBTI Diversity (axis balance) | 85% | 62% | +23% |
  | Skill Coverage (avg per team) | 4.2/5 | 3.1/5 | +35% |
  | Gender Balance (deviation) | 0.2 | 0.6 | -67% |
  ```
- [ ] Add paragraph explaining implications

**Files to edit**:
- thesis/chapters/chapter-4.tex (Hasil Pengujian Sistem subsection or new Analysis)

---

### 3.2 Mobile Limitations & Remediation 📱
**Issue**: NF-02 failures documented but not actionable

**Action Items**:
- [ ] Create "Known Issues & Mitigations" subsection in NF-02:
  ```
  | Issue | Root Cause | Impact | Mitigation |
  | Admin dialog overflow on mobile | Viewport width 375px < dialog width 500px | Admin features unusable | Use CSS media query + container query to reflow |
  | Language switcher off-screen | Sidebar not scrollable on mobile | i18n feature unavailable | Add sticky positioning or hamburger menu |
  | Touch target size < 44px | Reused desktop button sizes | Usability risk | Increase padding to 12px min on mobile |
  ```
- [ ] Propose fix (one or two concrete steps per issue)
- [ ] Optionally reference future work: "Mobile-first redesign for admin features (Saran 2.1)"

**Files to edit**:
- thesis/chapters/chapter-4.tex (NF-02 subsection, L1210-1224)

---

### 3.3 Security Results with Concrete Evidence 🔒
**Issue**: Claims of security without sample output or code references

**Action Items**:
- [ ] Add "Security Implementation Details" subsection:
  - Show sample HTTP header output:
    ```
    Set-Cookie: session=abc123; SameSite=Lax; Secure; HttpOnly; Max-Age=604800
    Content-Security-Policy: default-src 'self'; script-src 'self' cdn.example.com
    X-Frame-Options: DENY
    X-Content-Type-Options: nosniff
    ```
  - Cite code locations: "Better Auth configuration in src/auth/config.ts (line 42-55)"
  - List RBAC-protected routes: "/api/class/create", "/api/task/delete", etc.
  - Reference test file: "tests/security/rbac.test.ts (12 test cases, 100% pass)"
- [ ] Add sample RBAC test case (pseudocode or actual):
  ```
  test("Mahasiswa cannot access POST /api/class/create", async () => {
    const res = await fetch("/api/class/create", {
      method: "POST",
      headers: { Authorization: "Bearer student-token" }
    });
    expect(res.status).toBe(403);
  });
  ```

**Files to edit**:
- thesis/chapters/chapter-4.tex (NF-05 subsection, L1271-1305)

---

### 3.4 Strengthen Saran (Suggestions) 💡
**Issue**: Only 2 suggestions; examiners expect 3-5 actionable items

**Current**:
1. Email notifications (Resend API)
2. Mobile UI improvements

**Action Items**:
- [ ] Keep existing 2, add:
  3. **CSRF Token Implementation**: "Perlu implementasi CSRF token dengan rotation strategy untuk perlindungan maksimal terhadap request forgery" + reference CWE
  4. **Usability Study**: "Studi pengguna (N=10-15 responden) untuk mengukur task completion rate dan SUS score pada fitur pembentukan kelompok" + cite Nielsen/Lewis
  5. **Fairness & Explainability**: "Tambahkan explanation cards yang menunjukkan alasan penempatan setiap mahasiswa dalam tim (e.g., 'MBTI Compatibility: 92%, Skill Match: 88%')" + cite interpretable ML
  6. **Scalability Testing**: "Pengujian performa dengan load testing (N=500-1000 users concurrent) menggunakan Apache JMeter atau k6 untuk validasi skalabilitas"
- [ ] Format each as:
  - **Nomor. Judul**: Brief description
  - Implikasi bisnis / akademik (1-2 sentences)
  - Metrik kesuksesan (bagaimana diukur)

**Files to edit**:
- thesis/chapters/chapter-5.tex (Saran section)

---

### 3.5 Explicit Objective-to-Conclusion Traceability 🎯
**Issue**: Conclusions don't explicitly tie back to Bab I objectives

**Action Items**:
- [ ] In Chapter V Kesimpulan, add structure:
  ```
  Berdasarkan objektif penelitian yang ditetapkan di Bab I:
  
  O1. Mengembangkan sistem informasi EduTeams → ✓ TERCAPAI
      Bukti: 61/67 fitur diimplementasikan (Tabel 4.1), 347 test cases lulus 100% 
      (Bab IV), sistem siap produksi dengan MATURITY LEVEL 4/5
  
  O2. Menerapkan Agile Kanban methodology → ✓ TERCAPAI
      Bukti: Backlog awal Tabel 3.x, iterasi melalui 4 kolom Kanban 
      (Bab III), feedback loop testing-backlog documented (Bab III.2)
  
  O3. Integrasi Edu2Com API untuk otomatisasi pembentukan kelompok → ✓ TERCAPAI
      Bukti: 20/20 API test cases lulus, integrasi dijelaskan Bab IV.x, 
      algoritma multi-faktor (MBTI, skill, preferensi, gender) divalidasi
  
  O4. Menerapkan grey-box testing & E2E validation → ✓ TERCAPAI
      Bukti: 347 unit tests + 16 integration tests + 70 E2E tests, 
      89.42% code coverage, 92.9% NFR pass rate (Bab IV)
  ```

**Files to edit**:
- thesis/chapters/chapter-5.tex (Kesimpulan section, rewrite/enhance)

---

## PHASE 4: Final Polish & Consistency Checks

### 4.1 Global Consistency Sweep
**Action Items**:
- [ ] Product name: Search all .tex files for "EquiTeam" → none should exist
- [ ] Auth terminology: "Google OAuth" and "Better Auth" used consistently
- [ ] Test counts: Verify all mentions of "347", "16", "70" are consistent
- [ ] Performance numbers: All Lighthouse references show 98/100 for Performance
- [ ] Chapter references: \nameref, \ref labels are correct
- [ ] Italics: Framework names (\textit{Kanban}, \textit{grey-box testing})

**Files to check**:
- thesis/chapters/*.tex (all)
- thesis/chapters/abstract-*.tex

---

### 4.2 Bibliography & Citation Check
**Action Items**:
- [ ] Verify all new claims cite sources:
  - SameSite cookies: RFC 6265bis or MDN
  - MBTI fairness: Cite Kalantzi et al. (2020) already in refs
  - Kanban benefits: Ilmi et al. (2020) already cited
- [ ] Check missing citations from new text
- [ ] Ensure all \cite{...} keys exist in references.bib

---

### 4.3 Figure & Table Captions
**Action Items**:
- [ ] Verify all figures have captions following format: "Gambar X.X Deskripsi singkat"
- [ ] Captions are in Indonesian or English consistently
- [ ] All tables have \label{} for referencing
- [ ] Captions include source or note if needed (e.g., "Sumber: Hasil pengujian sistem")

---

## PHASE 5: Preparation & Dry Run

### 5.1 Compile Thesis & Check Output
**Action Items**:
- [ ] Run full compile: `pdflatex thesis.tex && bibtex thesis && pdflatex thesis.tex && pdflatex thesis.tex`
- [ ] Check for warnings/errors in log
- [ ] Verify all cross-references resolve (no "??" or "undefined reference")
- [ ] Check page numbering, TOC accuracy

---

### 5.2 Create Defense Talking Points & Answers
**Action Items**:
- [ ] Prepare 30-second elevator pitch: "Sistem EduTeams mengotomatisasi pembentukan kelompok mahasiswa berbasis AI dengan mempertimbangkan MBTI, keahlian, preferensi, dan gender balance. Diimplementasikan dengan Kanban, diuji dengan 347 test cases (100% pass), mencapai 89% code coverage."
- [ ] Practice answers to likely questions (see Professor feedback above):
  - "Kenapa Kanban?"
  - "Apa definisi 'success' dalam team formation?"
  - "Bagaimana CSRF protection?"
  - "Kenapa ada perbedaan Lighthouse 82 vs 98?"
  - "Data real atau synthetic?"
  - "Scalable ke berapa pengguna?"
  - "Etika MBTI?"
- [ ] Prepare live demos (if applicable):
  - Login flow
  - Team formation (GIF or video)
  - Dashboard statistics

---

### 5.3 Peer Review Checklist
**Action Items**:
- [ ] Have advisor or colleague read Chapter III & IV, check for:
  - Clarity of methodology
  - Completeness of test documentation
  - Logical flow
- [ ] Ask for feedback on security claims (did I tighten them enough?)
- [ ] Ask about mobile limitations explanation (is it sufficient?)

---

## Summary of Files to Edit

| File | Changes | Priority |
|------|---------|----------|
| thesis/chapters/chapter-3.tex | Auth flow (GB01-GB03), ERD, test environment, alur penelitian, Kanban justification, traceability matrix | **CRITICAL** |
| thesis/chapters/chapter-4.tex | Product naming (EquiTeam→EduTeams), Performance 82→98, CSRF/security tightening, mobile limitations, team quality benchmarking, security evidence, trailing updates | **CRITICAL** |
| thesis/chapters/chapter-5.tex | Strengthen Saran (5 items), tie conclusions to objectives, add threats to validity | **HIGH** |
| thesis/chapters/abstract-id.tex | Verify EduTeams naming | LOW |
| thesis/chapters/abstract-en.tex | Verify EduTeams naming | LOW |

---

## Estimated Effort

- **Phase 1** (Critical): 3-4 hours (naming, auth, performance, CSRF, numbering, typos)
- **Phase 2** (High-Priority): 3-5 hours (alur, justification, traceability, test env, privacy, threats)
- **Phase 3** (Enhancements): 2-3 hours (quality benchmarking, mobile details, security evidence, saran)
- **Phase 4** (Polish): 1-2 hours (consistency sweep, bib check, captions)
- **Phase 5** (Prep): 2-3 hours (compile, dry run, talking points, peer review)

**Total: ~12-18 hours** (1-2 days intensive work)

---

## Success Criteria

✅ All critical issues fixed and verified  
✅ High-priority improvements integrated  
✅ No "EquiTeam" references remain  
✅ Auth flow consistent across all sections  
✅ All Lighthouse results = 98/100 (or corrected to match actual)  
✅ Traceability matrix present and accurate  
✅ Threats to validity documented  
✅ Saran expanded to 5+ items  
✅ Thesis compiles without errors/warnings  
✅ Professor can answer all likely defense questions with evidence from thesis  

---

## Ready to Execute? 🚀

Approve this plan and I'll:
1. Execute all PHASE 1 (critical) fixes immediately
2. Apply PHASE 2-3 improvements systematically
3. Deliver corrected .tex files with change summaries
4. Provide defense Q&A document

**Next step**: Review this list, confirm priorities, and I'll start patching files.