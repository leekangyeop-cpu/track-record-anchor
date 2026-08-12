# Track Record Anchor

**EN** — Daily SHA-256 hash-chain anchors for a private quantitative research
system's prediction logs. The content stays private; its **existence,
timestamp, and immutability** become publicly verifiable.

Each line in [`anchors.jsonl`](anchors.jsonl) is one trading day:

```json
{
  "date": "YYYY-MM-DD",
  "files": { "<log name>": "<sha256 of the private file>" },
  "code":  { "git_head": "...", "src_tree_sha256": "..." },
  "prev_chain": "<yesterday's chain hash>",
  "chain": "SHA256(prev_chain + canonical_payload)"
}
```

**What this proves** (once the private repository is opened):

1. *Point-in-time existence* — each prediction log hashed here existed in
   exactly that state on that date (GitHub's commit history is the witness).
2. *No retroactive edits* — the logs are append-only; any later tampering
   changes the file hash and breaks every subsequent chain link.
3. *No cherry-picking* — a single unbroken daily chain means no parallel
   "better" version of history was kept.
4. *Model lineage* — the code fingerprint binds every prediction to the exact
   model version that produced it, making methodology evolution auditable.

**How to verify**: recompute SHA-256 of the published files, compare against
`anchors.jsonl`, then re-derive the chain from genesis (`prev_chain` of the
first line is 64 zeros). Nothing here can be reversed into the private
content — hashes only.

---

**KO** — 비공개 퀀트 리서치 시스템의 예측 기록에 대한 일일 SHA-256 해시 체인
공증입니다. 내용은 비공개로 유지되며, 그 **존재 시점과 불변성**만 공개
검증 가능해집니다. 예측·판단 로그는 append-only로 축적되고, 사후 수정은
파일 해시와 이후 체인 전체를 깨뜨리므로 구조적으로 불가능합니다. 코드
지문이 함께 앵커되어 "어떤 버전의 모델이 그 예측을 만들었는지"까지
감사(audit) 가능합니다. 본체 저장소 공개 시점에 전체가 소급 검증됩니다.

*Anchored automatically at 16:05 KST on trading days.*
