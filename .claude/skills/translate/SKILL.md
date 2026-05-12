---
name: translate
description: Translate a Bluecom docs page from English to Vietnamese (or vice versa) following the project's bilingual policy. Use when the user wants to translate a `.md` page, generate a `.vi.md`, or update an existing translation.
---

# Translate Bluecom Docs

Produces a Vietnamese sibling for an English Bluecom docs page using the project's bilingual policy.

## When to use

- User says "translate this page", "create Vietnamese version", "dịch trang này", or "/translate".
- A file `docs/.../foo.md` exists and a `.vi.md` sibling is missing or stale.

## Inputs

The user supplies a relative path inside `docs/`, e.g. `docs/integration/authentication.md`.

If the path is omitted, ask which page to translate. Suggest pages that have no `.vi.md` sibling by listing the diff between `*.md` and `*.vi.md`.

## Output

Write `docs/.../foo.vi.md` next to the source. Never overwrite the English source.

## Translation policy

1. **Keep English inline for protocol/API terms.** Do not translate:
   - Identifiers: `partnerCode`, `partnerSecret`, `userId`, `timestamp`, `token`, `partnerCode`.
   - Protocols/standards: `HMAC-SHA256`, `iframe`, `WebView`, `WKWebView`, `Webhook`, `postMessage`, `httpOnly`, `sameSite`, `secure`, `partitioned`, `CSP`, `frame-ancestors`.
   - HTTP semantics: status codes (`400`, `401`), header names, query param names.
   - Bluecom brand: `Bluecom`, `Bluecom eSIM Shop`, `Bluecom Marketplace`, `partnerCode`.
   - Error codes: `UNKNOWN_PROVIDER`, `VERIFICATION_FAILED`.
   - File names, URLs, code samples.

2. **Translate prose and explanations.** Keep tone professional and concise. Match Bluecom's banking-grade voice — neutral, clear, no marketing fluff.

3. **Glossary (use these consistently):**

   | English | Vietnamese |
   |---------|-----------|
   | Partner | Đối tác |
   | Handshake | Bắt tay (kèm `(handshake)` lần đầu xuất hiện trong page) |
   | Session | Phiên |
   | Onboarding | Onboarding (giữ nguyên — đã quen dùng) |
   | Checklist | Danh sách kiểm tra |
   | Environment | Môi trường |
   | Sandbox / Staging | Staging (giữ nguyên) |
   | Production | Production (giữ nguyên) |
   | Embedding | Nhúng |
   | Theming | Giao diện |
   | Localization | Đa ngôn ngữ |
   | Tracking event | Sự kiện theo dõi |
   | Dashboard | Bảng điều khiển |
   | Lead time / Turnaround | Thời gian xử lý |
   | Business day | Ngày làm việc |
   | End user | Người dùng cuối |
   | Webhook | Webhook |
   | Reseller | Đối tác phân phối |
   | Channel | Kênh |
   | Funnel | Phễu chuyển đổi |
   | Conversion rate | Tỷ lệ chuyển đổi |

4. **Preserve markdown structure exactly.** Same heading levels, same number of list items, same table columns. Translate cell contents but keep alignment.

5. **Code blocks:** translate only the comments inside; keep variable names, strings, and API calls in English. Skip code blocks marked language-agnostic (mermaid, plain text).

6. **Admonition titles:** translate the title text but keep the type keyword (e.g. `!!! warning "Trạng thái: Đang xác định"` instead of `!!! warning "Status: TBD"`).

7. **Internal links:** keep paths unchanged (`../integration/authentication.md`). The i18n plugin resolves the Vietnamese sibling automatically.

8. **YAML frontmatter:** copy unchanged.

## Workflow

1. Confirm the path with the user.
2. Read the English source in full.
3. Translate following the policy above. Do not abbreviate, summarize, or restructure.
4. Write the `.vi.md` sibling.
5. Run `uv run mkdocs build --strict` from the docs root to verify the Vietnamese build passes.
6. Report: number of headings translated, anything that was left in English on purpose, and any glossary additions the user should review.

## When NOT to translate

- The `index.md` home page uses raw HTML with `markdown` shortcodes — be careful with the `bc-hero` block; only translate the visible prose, not the class names or markup.
- Skip auto-generated content (none today, but watch for it later).

## Output style

Concise, accurate, banking-professional Vietnamese. Avoid:
- Marketing fluff ("trải nghiệm tuyệt vời", "giải pháp toàn diện").
- Informal pronouns ("bạn" is OK; avoid "mày/tao/cậu").
- Direct word-for-word translation that reads stiff — prefer natural Vietnamese phrasing while preserving meaning.
