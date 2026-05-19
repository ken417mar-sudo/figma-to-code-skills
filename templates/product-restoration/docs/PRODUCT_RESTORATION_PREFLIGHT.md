# Product Restoration Preflight

Status: `[not-started | in-progress | complete]`

## Source

- Product name: `[PRODUCT_NAME]`
- Figma file: `[FIGMA_FILE_KEY_OR_URL]`
- Source section/page: `[SOURCE_SECTION_OR_PAGE]`
- Target platform: `[web | ios | android | other]`
- Framework/runtime: `[FRAMEWORK]`
- Build command: `[BUILD_COMMAND]`
- Preview/package check: `[PREVIEW_COMMAND_OR_PACKAGE_CHECK]`

## Required Artifacts

| Artifact | Status | Notes |
|---|---|---|
| `FIGMA_BOARD_STATE_MAP.md` | `[ ]` | Board/state nodes mapped before code |
| `LAYOUT_CONSTANTS.md` | `[ ]` | Stable geometry and responsive limits |
| `TOKEN_SNAPSHOT.md` | `[ ]` | Colors, type, radii, shadows, effects |
| `ASSET_MANIFEST.md` | `[ ]` | Export plan and asset paths |
| `INTERACTION_CONTRACT.md` | `[ ]` | Confirmed actions and blocked inventions |

## Implementation Gate

Implementation may start only after:

- [ ] the first board/state has a Figma node;
- [ ] layout constants for the first board are recorded;
- [ ] required assets are classified and exported or scheduled;
- [ ] interaction rules for the first slice are confirmed;
- [ ] verification surface is defined.

## Blockers

| Blocker | Owner | Resolution Needed |
|---|---|---|
| `[BLOCKER]` | `[OWNER]` | `[NEXT_STEP]` |

## Handoff Status

Current status:

- `[ ]` preflight-complete
- `[ ]` implementation-ready
- `[ ]` board-verified
- `[ ]` production-preview-verified
- `[ ]` blocked
