# Design QA

## Current Study.html QA

final result: blocked

### Comparison Target

- Source visual truth: the first conversation attachment, with the second hand-drawn attachment defining the required content order.
- Implementation: `Study.html` and `styles.css` in this folder.
- Intended CSS viewport: `393x852 px`, device scale factor `1`.
- Implementation screenshot: unavailable; the Browser plugin reported no available browser instance.
- State to verify: learning tab selected, report carousel at first slide, task progress visible, all common app shortcuts visible in the same grid.

### Static Verification

- `Study.html` exists and is linked from the learning tab in `index.html`, `tasks.html`, `extension.html`, and `live.html`.
- The page order matches the requested sketch: top learner/action row, learning-report carousel, task progress, three application cards, and the common-app grid.
- The top row uses `assets/deer-avatar.png`, `learning-record-selected@3x.png`, and `ranking-selected@3x.png`; the two right-side action icons render without a white container background.
- The report carousel uses `learning-report-card-background.png` plus 3x transparent icons, with a larger `184px` carousel area and `168px` banner track.
- The top blue background is now a separate `study-hero::before` layer with `148px` height instead of wrapping the full carousel area.
- The report carousel is stacked above the blue background with `z-index: 2`, so the banner overlaps the top background rather than being contained by it.
- The carousel dots are positioned inside the banner layer so they remain visible after the blue background height reduction.
- The top background remains a short layered blue header behind the banner, and the previously added left/right angled side wings have been removed.
- The hero reserved height is reduced to `284px` and the progress card margin is set to `0`, moving `任務進度` closer to the banner.
- The progress module title is `任務進度`, the former `Red pocket` pill is removed, and the progress bar is set to 70% with the total task copy.
- The task progress module uses a light rounded background panel with no visible outer border/frame.
- The visible `常用應用` heading has been removed from `Study.html`.
- The common app shortcuts now sit inside a light rounded background panel matching the reference block treatment.
- The three application cards are Traditional Chinese: `口語`, `練習`, `作文`.
- The three application-card icons now load from `3x-V2`: `口语_选中_108x108_透明Icon.png`, `练习_选中_108x108_透明Icon.png`, and `作文_选中_108x108_透明Icon.png`.
- The common apps are Traditional Chinese and visible by default: `發音評測`, `場景對話`, `個人短講`, `看圖說話`, `拼音學習`, `拼音練習`, `小鹿認字`, `聆聽練習`, `作文批改`, `作文批改DSE`.
- The "更多" control has been removed; `作文批改` and `作文批改DSE` render inside the same common-app grid/background block by default.
- All local `img src` paths in the HTML files exist.
- The new page uses local image assets and icons from `3x-透明版` where matching 3x assets are available.

### Known Asset Mapping Notes

- `3x-透明版` does not contain exact `拼音學習` or `聆聽練習` file names.
- `拼音學習` is mapped to `hsk-video-learning-selected@3x.png`.
- `聆聽練習` is mapped to `learning-record-selected@3x.png`.

### Finding

- [P2] Browser-rendered comparison is unavailable.
  - Evidence: `agent.browsers.list()` returned an empty list, so no in-app browser instance was available.
  - Impact: final screenshot comparison against the reference image cannot receive a valid pass.
  - Fix: open `Study.html` in an available browser at `393x852`, compare against the supplied reference and sketch, then update this report.

---

## Previous Learning Page QA

final result: blocked

## Comparison Target

- Source visual truth: conversation attachment comparing the current top background placement with the target deer reveal.
- Implementation: `index.html` and `styles.css` in this folder.
- Intended CSS viewport: `393x1128 px`, device scale factor `1`.
- Implementation screenshot: unavailable; the in-app browser reported no available browser instance.
- Existing exports `学习页-普通话app第3版.png` and `学习页-普通话app第3版@2x.png` are previous renders and were not used as evidence for this revision.
- State: learning tab selected, fixed bottom navigation, iOS status and home-indicator chrome visible.

## Static Verification

- All three section headings use `#4D4D4D`.
- All three title marks use `#00A1F6`.
- Oral-practice cards use `rgba(255, 154, 77, 0.04)`.
- Pinyin cards use `rgba(77, 148, 255, 0.04)`.
- More-practice cards use `rgba(0, 194, 138, 0.04)`.
- The learning Tab remains selected; tasks, extension class, and live class now use their `*-default.png` unselected assets.
- The ranking statistic no longer contains `07`; its label remains explicitly placed on the second stat row to align with `練習記錄`.
- The listening-practice selected icon now uses a deep-teal/high-saturation green palette with a specified `4.68:1` key-detail-to-plate contrast.
- The status bar and learner profile now share one edge-to-edge blue gradient wrapper with no independent status-bar background.
- Status-bar text uses translucent white and the supplied iOS status asset is rendered white through a CSS filter.
- The profile surface is reduced to `142px`, showing only the avatar, learner name, and class over the supplied full-page background.
- The learner name is rendered at `24px`; the app shell now uses the supplied `app-bg-pure.png` as the full-page background, shifted upward by `18px`, with the profile header transparent over it.
- The former standalone cloud-mounted deer asset has been removed; the visible top illustration now comes from `app-bg-pure.png`.
- The fixed tab bar now sits `12px` above the home-indicator area and uses a translucent blurred surface with two-layer soft shadowing.
- The learning-growth card now uses the exact Traditional Chinese title `7月學習成長報告出爐啦！` and subtitle `看看這個月的學習進步吧`.
- Its generated transparent icon contains one open report book, three stars, and one upward growth arrow; the action remains a circular right-chevron button.
- The learning-growth card surface now uses CSS gradients, a subtle border, and a soft curve decoration instead of the full framed PNG background, removing the clipped top and bottom frame edges.
- All 22 referenced image assets exist locally.
- All 18 business-icon references now use `./1x-V2/`; no `logo2x` reference remains.
- The three new default Tab assets and revised listening icon are `36x36 px` RGBA PNGs with fully transparent canvas corners.

## Required Fidelity Surfaces

- Fonts and typography: requested heading color is confirmed in CSS; browser-rendered weight, antialiasing, and wrapping remain unverified.
- Spacing and layout rhythm: the status bar is absolutely positioned within the compact `142px` profile surface, and the navigation-to-home-indicator gap is confirmed in CSS; visible overlap and final vertical rhythm remain unverified.
- Colors and visual tokens: all requested hex and 4% alpha values are confirmed in CSS.
- Image quality and asset fidelity: the active learning Tab uses the selected asset, the other three Tabs use unselected assets, and the revised listening icon uses the stronger selected-state palette at native size. Browser sharpness remains unverified.
- Copy and content: `9:41`, Traditional Chinese labels, and the existing learning-page content are present.

## Findings

- [P2] Browser-rendered comparison is unavailable.
  - Evidence: no in-app browser instance was available, so the revised implementation could not be captured at `393x1128` or placed beside the source attachment.
  - Impact: status-bar spacing, fixed-tab/home-indicator separation, and final visual polish cannot receive a valid pass.
  - Fix: capture the revised page in the in-app browser at the intended viewport, compare it beside the annotated source, and refresh both PNG exports.

## Comparison History

- Current pass: supplied full-page background, removed standalone cloud-mounted deer asset, compact profile header, and redesigned learning-growth card implemented; static checks passed; visual comparison remains blocked before the first screenshot pass.

## Focused Region Evidence

- Not available. Required focused captures are the top status bar and the bottom tab/home-indicator region.

## Implementation Checklist

- Capture the revised page at `393x1128` and `786x2256`.
- Compare the full page plus focused top and bottom regions against the source.
- Fix any P0/P1/P2 visual mismatch, then update this report to `final result: passed`.
