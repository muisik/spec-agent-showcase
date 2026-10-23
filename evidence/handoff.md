# Implementation Handoff - PARTIAL

## Handoff Status
- Status: `partial`
- Readiness score: `69/100`
- Critical warning: This package is usable as an implementation draft, but missing information or assumptions must be reviewed.

## Project Summary
- Project: İade Operasyonları — Canlı API
- Project id: `fd14d1b8-79d2-4ab0-9cc0-e9f2a189a9d1`
- Description: missing
- Generated at: 2026-10-23T12:53:06.130746+00:00
- Known facts: missing

## Required Intake
These records are mandatory project-understanding inputs, not implementation features.

- `PROFILE-001` Ürün / alan profili (profile, ready_for_handoff)
- `PROFILE-002` Hedef kullanıcılar ve kullanım bağlamı (profile, ready_for_handoff)
- `PROFILE-003` Kapsam düzeyi, kapsam dışı ve sınırlar (profile, ready_for_handoff)
- `PROFILE-004` Technical profile (profile, in_detailing)
- `PROFILE-005` Handoff target and output language (profile, in_detailing)
- `CHARTER-001` Product charter and implementation principles (charter, in_detailing)

Incomplete required intake:
- PROFILE-004 Technical profile
- PROFILE-005 Handoff target and output language
- CHARTER-001 Product charter and implementation principles

## Product Direction And Boundaries
- Target users: missing
- Usage context: missing
- Scope level: missing
- Strictness: standard

Product decisions:
- Pilot sürümde müşteri erişim modeli: tek kullanımlık talep bağlantısı. Operasyon uzmanı bağlantıyı müşterinin sipariş e-postasına manuel gönderir. ERP/Shopify entegrasyonu ve müşteri hesabı açma ilk pilotta kapsam dışı.

Missing direction inputs:
- target users
- usage context

## Methodology Profile
- Scope level: `missing`
- Strictness: `standard`
- Voice posture: Use one high-impact question per turn while maintaining coding-agent-ready detail.
- Handoff posture: Partial packages can be exported for review; READY requires profile, intake and REQ completeness alignment.
- Completeness posture: Missing dimensions keep the package partial and are listed under the related REQ.
- Active methodology checks:
- project profile
- functional behavior
- acceptance criteria
- dependencies and out-of-scope

## Technical Profile
- Source: project profile, project meta and current included REQs.
- Platform/runtime: `missing`: not captured
- Language/framework/stack: `missing`: not captured
- Database/storage: `not_explicit_in_current_reqs`
- Auth approach: `not_explicit_in_current_reqs`
- External integrations: `not_explicit_in_current_reqs`
- Deployment assumption: `not_explicit_in_current_reqs`
- Test/smoke command: `not_explicit_in_current_reqs`
- Handoff target: `missing`: not captured

Missing technical profile inputs:
- target platform
- implementation stack
- scope level
- handoff target

## Included And Excluded Scope
- Include backlog requested: `false`
- Priority filter: `none`
- Status filter: `default accepted/in_detailing/ready_for_handoff`

Included requirements:
- `REQ-001` Müşteri iade talebi oluşturma formu (accepted, must)
- `REQ-002` Operasyon uzmanı inceleme ve kabul/ret kararı (accepted, must)
- `REQ-003` Tek kullanımlık iade talep bağlantısı ve manuel e-posta gönderimi (accepted, must)

Excluded / pending requirements:
- No excluded requirements.

## Source Coverage Review
- Status: `needs_review`
- Current for spec revision: `false`
- Summary: Artifact agent changed project scope.

## Requirements
### REQ-001: Müşteri iade talebi oluşturma formu
- Status: `accepted`
- Priority: `must`
- Type: `feature`
- Details: Müşteri, sipariş numarası, iade nedeni ve en az bir ürün fotoğrafı girerek iade talebi açar. Form yalnızca REQ-003 kapsamındaki geçerli ve daha önce kullanılmamış tek kullanımlık bağlantı üzerinden açılır; bağlantı olmadan veya geçersiz/kullanılmış bağlantıyla forma erişilemez. Üç alan da zorunludur: sipariş numarası, iade nedeni ve en az bir ürün fotoğrafı. Eksik alan varsa talep oluşturulmaz ve ilgili alanda hata mesajı gösterilir. Geçerli gönderimde talep "inceleme bekliyor" durumunda oluşur ve operasyon ekibinin inceleme kuyruğuna düşer; aynı bağlantı tekrar kullanılamaz. Pilot kapsamında müşteri hesabı/oturum açma gerekmez; talep sipariş numarası üzerinden ilişkilendirilir.
- Rationale: Müşteri talebini izlenebilir ve kontrollü toplamak: her talep geçerli bir siparişe bağlı tek kullanımlık bağlantıdan gelir, zorunlu alanlar eksiksiz toplanır ve talep operasyon incelemesine düşer.
- Done definition: Form yalnız geçerli ve kullanılmamış tek kullanımlık bağlantıyla açılıyor; üç zorunlu alan eksikse talep oluşmuyor ve alan hatası gösteriliyor; geçerli gönderimde inceleme bekleyen talep oluşuyor ve bağlantı tekrar kullanılamıyor.
- Handoff quality warning: this REQ can be exported for review, but deterministic readiness is not complete.
- Missing completeness dimensions: dependencies
- Pre-conditions:
- Operasyon uzmanı ilgili sipariş için tek kullanımlık iade talep bağlantısı üretmiş ve müşteriye iletmiş olmalı (REQ-003).
- Bağlantı geçerli (süresi dolmamış) ve daha önce kullanılmamış olmalı.
- Post-conditions:
- Geçerli gönderimde 'inceleme bekliyor' durumunda bir iade talebi kaydı oluşur ve operasyon inceleme kuyruğunda görünür.
- Kullanılan bağlantı geçersiz hale gelir ve tekrar kullanılamaz.
- Eksik alanlı gönderimde hiçbir talep kaydı oluşmaz ve bağlantı kullanılmamış kalır.
- Acceptance criteria:
  - Acceptance scenario: Given Operasyon uzmanının ürettiği geçerli ve kullanılmamış tek kullanımlık bağlantı; When Müşteri bağlantıyı açar; Then İade talebi formu açılır ve sipariş numarası, iade nedeni ve ürün fotoğrafı alanları gösterilir.
  - Acceptance scenario: Given Açık formda sipariş numarası, iade nedeni veya ürün fotoğrafı alanlarından en az biri boş; When Müşteri formu göndermeye çalışır; Then Talep oluşturulmaz, eksik alanlarda alan hatası gösterilir ve bağlantı kullanılmamış kalır.
  - Acceptance scenario: Given Açık formda sipariş numarası, iade nedeni ve en az bir ürün fotoğrafı doldurulmuş; When Müşteri formu gönderir; Then İnceleme bekleyen bir iade talebi oluşur ve aynı bağlantı tekrar kullanılamaz.
- Notes: S1 talebi: yalnız REQ-001 revizyonu; diğer kayıtlar değiştirilmedi. Bağlantı üretimi ve geçerlilik/süre kuralları REQ-003 kapsamında kalır.
- Completeness checklist:
  - need_problem: `filled` (source: req_fields)
  - functional_requirement: `filled` (source: req_fields)
  - inputs: `filled` (source: req_fields)
  - outputs: `filled` (source: req_fields)
  - behavior: `filled` (source: req_fields)
  - edge_cases: `filled` (source: req_fields)
  - acceptance_criteria: `filled` (source: req_fields)
  - rationale: `filled` (source: req_fields)
  - priority: `filled` (source: req_fields)
  - dependencies: `missing` (source: not_explicit)
  - out_of_scope: `filled` (source: req_fields)
  - source_traceability: `filled` (source: req_fields)
- Source events: evt_93a2a24f5d964d4aad763c7b9724d093, evt_d0a4175b6fbb4f52b9be2250318bf24e, evt_6196f52f7462493297560352934620db
- Decisions: missing

### REQ-002: Operasyon uzmanı inceleme ve kabul/ret kararı
- Status: `accepted`
- Priority: `must`
- Type: `feature`
- Details: Operasyon uzmanı gelen iade taleplerini listeler, bir talebi açar; sipariş numarası, iade nedeni ve ürün fotoğrafını inceler; ardından talebi kabul veya ret olarak sonuçlandırır. Karar talebin durumunu günceller. Karar yalnızca operasyonel kayıttır; ödeme/muhasebe/para iadesi tetiklemez.
- Rationale: S1'in ikinci açık yeteneği: operasyon uzmanının inceleme ve karar verme akışı.
- Done definition: missing
- Handoff quality warning: this REQ can be exported for review, but deterministic readiness is not complete.
- Missing completeness dimensions: inputs, outputs, behavior, edge_cases, acceptance_criteria, dependencies
- Acceptance criteria: missing
- Notes: Ret gerekçesi zorunlu mu, karar sonrası düzeltme/geri alma var mı — sonraki turda netleştirilecek.
- Completeness checklist:
  - need_problem: `filled` (source: req_fields)
  - functional_requirement: `filled` (source: req_fields)
  - inputs: `missing` (source: not_explicit)
  - outputs: `missing` (source: not_explicit)
  - behavior: `missing` (source: not_explicit)
  - edge_cases: `missing` (source: not_explicit)
  - acceptance_criteria: `missing` (source: not_explicit)
  - rationale: `filled` (source: req_fields)
  - priority: `filled` (source: req_fields)
  - dependencies: `missing` (source: not_explicit)
  - out_of_scope: `filled` (source: req_fields)
  - source_traceability: `filled` (source: req_fields)
- Source events: evt_93a2a24f5d964d4aad763c7b9724d093, evt_d0a4175b6fbb4f52b9be2250318bf24e
- Decisions: missing

### REQ-003: Tek kullanımlık iade talep bağlantısı ve manuel e-posta gönderimi
- Status: `accepted`
- Priority: `must`
- Type: `feature`
- Details: Operasyon uzmanı, bir sipariş için tek kullanımlık iade talep bağlantısı üretir ve bu bağlantıyı müşterinin sipariş e-postasına manuel olarak gönderir (uygulama otomatik e-posta göndermez; uzman kendi e-posta istemcisini kullanır). Bağlantı yalnızca ilgili sipariş için geçerlidir, tek kullanımdır ve süresi dolabilir. Müşteri bağlantıyı açtığında hesap açmadan iade talebi formunu görür. Pilot kapsamında ERP/Shopify entegrasyonu ve müşteri hesabı yoktur.
- Rationale: S1'in açıkça istediği yeni yetenek: tek kullanımlık bağlantı seçeneği, manuel gönderim, entegrasyon ve hesap açmanın pilotta olmaması.
- Done definition: missing
- Handoff quality warning: this REQ can be exported for review, but deterministic readiness is not complete.
- Missing completeness dimensions: inputs, outputs, behavior, edge_cases, acceptance_criteria, dependencies
- Acceptance criteria: missing
- Notes: Bağlantı geçerlilik süresi, tek kullanım sonrası davranış ve e-posta adresinin nereden geldiği (manuel giriş) sonraki detaylandırma turunda netleştirilmeli.
- Completeness checklist:
  - need_problem: `filled` (source: req_fields)
  - functional_requirement: `filled` (source: req_fields)
  - inputs: `missing` (source: not_explicit)
  - outputs: `missing` (source: not_explicit)
  - behavior: `missing` (source: not_explicit)
  - edge_cases: `missing` (source: not_explicit)
  - acceptance_criteria: `missing` (source: not_explicit)
  - rationale: `filled` (source: req_fields)
  - priority: `filled` (source: req_fields)
  - dependencies: `missing` (source: not_explicit)
  - out_of_scope: `filled` (source: req_fields)
  - source_traceability: `filled` (source: req_fields)
- Source events: evt_fb1ac5356905405ea92c5529dd0619af, evt_d0a4175b6fbb4f52b9be2250318bf24e
- Decisions: missing


## Dependencies
No explicit dependencies captured.

## Assumptions
No explicit assumptions captured.

## Open Questions
No open questions captured.

## Blockers
- Source coverage review is missing or stale.
- REQ-001 (Müşteri iade talebi oluşturma formu): dependencies
- REQ-002 (Operasyon uzmanı inceleme ve kabul/ret kararı): inputs, outputs, behavior, edge_cases, acceptance_criteria, dependencies
- REQ-003 (Tek kullanımlık iade talep bağlantısı ve manuel e-posta gönderimi): inputs, outputs, behavior, edge_cases, acceptance_criteria, dependencies

## Interface / API Expectations
- Source: current included REQs.
- Coverage: `not_explicit_in_current_reqs`
- Missing or not applicable: No explicit API/interface expectation is present in the current included REQs.

## Entity / Data Notes
- Source: current included REQs.
- Coverage: `not_explicit_in_current_reqs`
- Missing or not applicable: No explicit entity model or mock/seed data is present in the current included REQs.

## UI / UX Notes
- Source: current included REQs.
- Coverage: `not_explicit_in_current_reqs`
- Missing or not applicable: No explicit UI/design expectation is present in the current included REQs.

## Implementation Contract
- Treat this package status as `partial`.
- Read order: status, warnings, included scope, requirements, blockers/open questions, trace references.
- Use required intake records to understand the project; do not implement them as feature scope.
- Do not implement excluded, backlog, archived or candidate scope unless explicitly re-approved.
- Start by confirming blockers and missing profile fields before coding if status is not `ready`.
- Use acceptance criteria and done definition as the first test design input.
- Success criteria: implemented scope matches included REQs, excluded scope is not built, and tests cover listed acceptance criteria.

## Trace References
- Canonical timeline: `conversation.jsonl`
- Canonical requirements: `items/REQ-*.md`
- Required intake records: `items/PROFILE-*.md`, `items/CHARTER-*.md`
- Reasoning snapshot: `reasoning_snapshot.json` when present
- Git history endpoint: `/projects/{project_id}/history`

Item traces:
- PROFILE-001: trace `evt_93a2a24f5d964d4aad763c7b9724d093`; affected `PROFILE-001, PROFILE-002, PROFILE-003`
- PROFILE-002: trace `evt_93a2a24f5d964d4aad763c7b9724d093`; affected `PROFILE-001, PROFILE-002, PROFILE-003`
- PROFILE-003: trace `evt_93a2a24f5d964d4aad763c7b9724d093`; affected `PROFILE-001, PROFILE-002, PROFILE-003`
- PROFILE-004: trace `missing`; affected `none`
- PROFILE-005: trace `missing`; affected `none`
- CHARTER-001: trace `missing`; affected `none`
- REQ-001: trace `evt_93a2a24f5d964d4aad763c7b9724d093, evt_d0a4175b6fbb4f52b9be2250318bf24e, evt_6196f52f7462493297560352934620db`; affected `REQ-001, REQ-002, REQ-003`
- REQ-002: trace `evt_93a2a24f5d964d4aad763c7b9724d093, evt_d0a4175b6fbb4f52b9be2250318bf24e`; affected `REQ-001, REQ-002, REQ-003`
- REQ-003: trace `evt_fb1ac5356905405ea92c5529dd0619af, evt_d0a4175b6fbb4f52b9be2250318bf24e`; affected `REQ-001, REQ-002, REQ-003`

## Context Budget Estimate
- Total characters before this section: 13261
- Total estimate before this section: ~3315 tokens
- Handoff Status: ~47 tokens
- Project Summary: ~50 tokens
- Required Intake: ~178 tokens
- Product Direction And Boundaries: ~104 tokens
- Methodology Profile: ~129 tokens
- Technical Profile: ~144 tokens
- Included And Excluded Scope: ~117 tokens
- Source Coverage Review: ~32 tokens
- Requirements: ~1766 tokens
- Dependencies: ~12 tokens
- Assumptions: ~11 tokens
- Open Questions: ~10 tokens
- Blockers: ~99 tokens
- Interface / API Expectations: ~52 tokens
- Entity / Data Notes: ~51 tokens
- UI / UX Notes: ~48 tokens
- Implementation Contract: ~167 tokens
- Trace References: ~299 tokens
