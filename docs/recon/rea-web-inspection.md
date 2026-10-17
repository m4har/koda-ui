# Rea web inspection — kodacademy.id

Tool: `rea` MCP (`inspect_web_page` via CDP `http://127.0.0.1:9333`), headless Chrome 152, origin `https://www.kodacademy.id`.
Evidence: `rea-inspect-evidence.json` (trimmed) · full 1.5 MB capture: `/home/mahar/.hermes/cache/spillover/call_3f7e86d24f41.txt`.

## Completeness (honest limits)

- `completeness.status`: `policy_filtered` · `attach_limited` — inspection attached after load, so:
  - `network.requests`: 0 (no requests observed in window)
  - `script_sources`: filtered, `scripts.items[].url` collapsed to the page URL (9 script entries, keys only)
  - `metadata.dom_urls`: 307 cross-origin `href`/`src` reported as `outside_policy` (URLs withheld)
  - `accessibility.text_capture`: 3 policy-status entries, node names available per-node instead
- Storage: `localStorage`/`sessionStorage`/IndexedDB/Cache all **empty** for this origin; `usage_bytes: 0`.

## DOM inventory

- Total nodes: **7155**; Accessibility nodes: **5198**
- Tags: DIV 4023, ::after 1109, #text 750, P 601, IMG 244, #comment 105, BUTTON 43, svg 39, ::before 30, path 29, LINK 24, use 21

## Accessibility roles

- generic: 2971
- InlineTextBox: 692
- StaticText: 594
- paragraph: 579
- none: 316
- button: 20
- link: 9
- heading: 6
- list: 3
- listitem: 2
- RootWebArea: 1
- form: 1
- LabelText: 1
- tooltip: 1
- group: 1
- textbox: 1

## Named controls (structure contract for the kit)

**Headings (page section order):**
1. Fokus Kami untuk Karirmu
2. Jadwal Bootcamp Terdekat
3. Proses Pendaftaran Simpel Dalam 4 Langkah
4. Kamu fokus belajar, sisanya kami siapkan.
5. Pertanyaan yang Sering Diajukan
6. Jadi Programmer Profesional dalam 14 Minggu

**Buttons (20):** Langganan, Putar slide 1, Putar slide 2, Putar slide 3, Putar slide 4, Putar slide 5, Putar slide 6, Putar slide 7, Putar slide 8, Putar slide 9, Putar slide 10, Previous, Next, 01 Dasar Pemrograman Web LIHAT 6 MATERI, 02 Front End Development LIHAT 4 MATERI, 03 Back End Development LIHAT 8 MATERI, 04 DevOps & Deployment LIHAT 2 MATERI, 05 Capstone Project LIHAT 1 MATERI, 06 Career Preparation LIHAT 1 MATERI, Tonton cerita lengkap

**Links (9):** Daftar Sekarang, Daftar Sekarang, Chat Tim Koda, Instagram, Linkedin, Youtube, NEXT DIRIMU, Daftar Sekarang, Daftar Sekarang

## Cross-check vs manual CDP recon

| Item | Manual recon | Rea | Match |
| --- | --- | --- | --- |
| Section order | hero → stats → fokus karir → jadwal → proses 4 langkah → FAQ → CTA 14 minggu | same 6 headings + CTA | yes |
| Alumni carousel | not captured | 10 slides (`Putar slide 1..10`), `Previous`, pagination group, alumni tooltip `M. Faisal Ilham #Alumni 2025 SOFTWARE ENGINEER` | rea found more |
| CTA labels | "Daftar Sekarang" | 4× `Daftar Sekarang`, `Chat Tim Koda`, newsletter `Langganan`, social links Instagram/Linkedin/Youtube | yes |
| Storage / PII | not checked | none persisted | new |
