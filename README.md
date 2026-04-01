# Investment Discipline Console Skill

* * *

[English](#english)涓╗涓枃](#涓枃)

## English

This repository is natively packaged as a Codex skill. Its workflow and prompt structure can be adapted to other AI agents, but native compatibility depends on each agent's own extension mechanism. It turns scattered trade ideas, holdings screenshots, review notes, and recurring behavior patterns into a repeatable operating system:

- First-run portfolio bootstrap
- Holdings review from manual input or broker screenshots
- Multi-account portfolio aggregation
- Holdings delta review across two dates
- Watchlist intake
- Pre-trade review
- Post-trade attribution
- Discipline memory and user-profile refinement
- Behavior correction and mistake tagging

This skill is designed to behave like a discipline system, not a research-only assistant. It prioritizes portfolio context, risk budgets, and invalidation rules before deeper company analysis.

### When It Triggers

This skill is typically triggered in two cases:

- You explicitly call `$investment-discipline-console`
- Your request is about holdings review, trade review, comparing two portfolio snapshots, writing a pre-trade memo, post-trade attribution, or setting up the investing discipline system for the first time

Common trigger scenarios include:

- You upload a broker screenshot and want a review of current holdings
- You provide two snapshots across time and want to explain why the book changed so much
- You ask whether a trade should be done at all
- You are using the system for the first time and want to define portfolio size, drawdown, and position limits before any review
- You want a weekly discipline review that summarizes repeated mistakes and process drift

### Repository Structure

```text
investment-discipline-console/
  SKILL.md
  agents/openai.yaml
  references/
    doctrine.md
    schemas.md
    workflow-bootstrap.md
    workflow-portfolio-review.md
    workflow-holdings-delta-review.md
    workflow-discipline-memory.md
    workflow-watchlist.md
    workflow-pre-trade.md
    workflow-attribution.md
    behavior-tags.md
    examples.md
    end-to-end-examples.md
```

### What It Covers

- `bootstrap`: define portfolio size, target return, drawdown tolerance, single-position cap, single-theme cap, leverage cap, profit-taking or deleveraging trigger, macro view, and industry view
- `portfolio review`: review current holdings, leverage exposure, concentration, profit-take candidates, and cross-account risk
- `holdings delta review`: compare T-day and T+N-day holdings, identify major adds, trims, exits, and new positions, and require the user to explain large changes
- `discipline memory`: summarize user style, confirmed rules, repeated mistakes, and weekly discipline patterns so future reviews become more targeted
- `watchlist`: convert vague ideas into explicit thesis + catalyst records
- `pre-trade review`: return `allow`, `review`, `reduce_size`, `delay`, or `block`
- `attribution`: separate result from process and turn mistakes into reusable rules

Pre-trade action meanings:

- `allow`: execution is reasonable because the core information and sizing constraints are largely complete
- `review`: the direction may be right, but it is still too early to act because key fields or evidence are missing
- `reduce_size`: the direction may still be valid, but the position, leverage, or overlapping risk is too large and should be expressed with less size
- `delay`: do not act yet; this is better handled by collecting more information, waiting for new facts, or waiting for discipline conditions to be met
- `block`: do not proceed; the trade clearly violates the existing discipline or risk budget

### Install

From GitHub:

```bash
npx skills add https://github.com/yuanlusi/investment-discipline-console-skill/tree/main/investment-discipline-console
```

Manual install:

```bash
cp -R investment-discipline-console "${CODEX_HOME:-$HOME/.codex}/skills/"
```

### Usage

Typical prompts:

```text
Use $investment-discipline-console to help me set up my portfolio context before I review any trade.

Use $investment-discipline-console to combine my HK and US accounts into one portfolio view and tell me which limits I am breaching.

Use $investment-discipline-console to review whether I should open a Tencent starter position.

Use $investment-discipline-console to tell me which positions in my current portfolio need review first.

Use $investment-discipline-console to compare my T-day holdings with my T+3-day holdings and tell me which changes need explanation.

Use $investment-discipline-console to run a weekly discipline review and summarize what mistakes I repeated this week.

Use $investment-discipline-console to summarize what kind of trader I am becoming from my recent reviews and tell me what mistakes I repeat.
```

### Notes

- This skill is for structured decision support and review.
- It can build discipline memory, user-profile patterns, and weekly review summaries from prior reviews.
- It focuses on trade discipline, process quality, risk alignment, and behavior correction.
- It does not make symbol-selection or buy/sell recommendations for specific assets.
- It does not replace independent judgment.
- It is intentionally conservative when portfolio context is missing.

## 涓枃

杩欎釜浠撳簱褰撳墠鍘熺敓閲囩敤 Codex skill 鏍煎紡鎵撳寘锛涘叾涓殑鏂规硶璁哄拰鎻愮ず缁撴瀯涔熷彲浠ヨ縼绉诲埌鍏朵粬 AI Agent锛屼絾鏄惁鍘熺敓鍏煎鍙栧喅浜庡鏂硅嚜宸辩殑鎵╁睍鏈哄埗銆?
瀹冩妸闆舵暎鐨勪氦鏄撴兂娉曘€佹寔浠撴埅鍥俱€佸鐩樼瑪璁板拰閲嶅琛屼负妯″紡锛屾暣鐞嗘垚涓€濂楀彲閲嶅鎵ц鐨勬搷浣滅郴缁燂細

- 棣栨浣跨敤鐨勭粍鍚堝垵濮嬪寲
- 鎵嬪伐鎸佷粨 / 鍒稿晢鎴浘鎸佷粨 review
- 澶氳处鎴风粍鍚堟眹鎬?
- 涓ゆ湡鎸佷粨鍙樺寲 review
- 瑙傚療姹?intake
- 浜ゆ槗鍓嶅鏌?
- 浜ゆ槗鍚庡綊鍥?
- 绾緥璁板繂 / 鐢ㄦ埛鐢诲儚杩唬
- 琛屼负鍋忓樊淇涓庨敊璇爣绛炬矇娣€

杩欏 skill 鐨勫畾浣嶄笉鏄€滃彧鍋氱爺绌垛€濈殑鍔╂墜锛岃€屾槸鈥滅邯寰嬬郴缁熲€濄€傚畠浼氫紭鍏堣姹傜粍鍚堜笂涓嬫枃銆侀闄╅绠楀拰澶辨晥鏉′欢锛屽啀杩涘叆鏇存繁鐨勫叕鍙稿垎鏋愩€?

### 浠€涔堟椂鍊欎細瑙﹀彂

涓€鑸湁涓ょ鎯呭喌浼氳Е鍙戣繖濂?skill锛?

- 浣犵洿鎺ョ偣鍚嶄娇鐢?`$investment-discipline-console`
- 浣犵殑璇锋眰鏈韩灏卞湪鍋氭寔浠?review銆佷氦鏄撳鏌ャ€佷袱鏈熸寔浠撳姣斻€佷氦鏄撳墠 memo銆佷氦鏄撳悗澶嶇洏锛屾垨鑰呴娆″缓绔嬫姇璧勭邯寰嬬郴缁?

甯歌瑙﹀彂鍦烘櫙鍖呮嫭锛?

- 浣犱笂浼犳寔浠撴埅鍥撅紝甯屾湜 review 褰撳墠鎸佷粨
- 浣犵粰鍑轰袱涓椂鐐圭殑鎸佷粨锛屽笇鏈涜В閲婁负浠€涔堝彉鍖栬繖涔堝ぇ
- 浣犻棶鈥滆繖绗斾氦鏄撴垜璇ヤ笉璇ュ仛鈥?
- 浣犵涓€娆＄敤杩欏绯荤粺锛屽笇鏈涘厛鎶婅处鎴疯妯°€佸洖鎾ゃ€佷粨浣嶄笂闄愯繖浜涜鍒欏畾涓嬫潵
- 浣犲笇鏈涘仛涓€娆″懆搴︾邯寰嬪鐩橈紝鐪嬬湅杩欏懆閲嶅浜嗗摢浜涢敊璇?

### 浠撳簱缁撴瀯

```text
investment-discipline-console/
  SKILL.md
  agents/openai.yaml
  references/
    doctrine.md
    schemas.md
    workflow-bootstrap.md
    workflow-portfolio-review.md
    workflow-holdings-delta-review.md
    workflow-discipline-memory.md
    workflow-watchlist.md
    workflow-pre-trade.md
    workflow-attribution.md
    behavior-tags.md
    examples.md
    end-to-end-examples.md
```

### 瑕嗙洊鍐呭

- `bootstrap`锛氬厛瀹氫箟璐︽埛瑙勬ā銆佺洰鏍囨敹鐩婄巼銆佸洖鎾ゅ蹇嶅害銆佸崟浠撲笂闄愩€佷富棰樹笂闄愩€佹潬鏉嗕笂闄愩€佹鐩堥檷鏉犳潌瑙﹀彂鏉′欢銆佸畯瑙傚垽鏂€佷骇涓氬垽鏂?
- `portfolio review`锛歳eview 褰撳墠鎸佷粨銆佹潬鏉嗘毚闇层€侀泦涓害銆佹鐩堝€欓€夊拰璺ㄨ处鎴烽闄?
- `holdings delta review`锛氬姣?T 鏃ュ拰 T+N 鏃ユ寔浠擄紝璇嗗埆澶у箙鍔犱粨銆佸噺浠撱€佹竻浠撱€佹柊寮€浠擄紝骞惰姹傜敤鎴疯В閲婂ぇ鍙樺寲
- `discipline memory`锛氭矇娣€鐢ㄦ埛椋庢牸銆佸凡纭瑙勫垯銆侀噸澶嶉敊璇拰鍛ㄥ害绾緥妯″紡锛岃鍚庣画 review 鏇存湁閽堝鎬?
- `watchlist`锛氭妸妯＄硦鎯虫硶鍙樻垚鏄庣‘鐨?thesis + catalyst 璁板綍
- `pre-trade review`锛氳緭鍑?`allow`銆乣review`銆乣reduce_size`銆乣delay`銆乣block`
- `attribution`锛氭妸缁撴灉涓庤繃绋嬫媶寮€锛屾矇娣€鎴愬彲澶嶇敤瑙勫垯

`pre-trade review` 鍑犱釜鐘舵€佺殑鍚箟锛?

- `allow`锛氬彲浠ユ墽琛岋紝鏍稿績淇℃伅鍜屼粨浣嶇害鏉熷熀鏈畬鏁?
- `review`锛氭柟鍚戝彲鑳藉锛屼絾杩樹笉鑳界洿鎺ヤ笅鍗曪紝浠嶇己灏戝叧閿瓧娈垫垨璇佹嵁
- `reduce_size`锛氭柟鍚戞湭蹇呴敊锛屼絾浠撲綅銆佹潬鏉嗘垨椋庨櫓閲嶅彔杩囧ぇ锛岄渶瑕佺缉灏忚〃杈?
- `delay`锛氬厛鍒姩锛屽綋鍓嶆洿閫傚悎琛ヤ俊鎭€佺瓑鏂颁簨瀹炴垨绛夌邯寰嬫潯浠舵弧瓒?
- `block`锛氬綋鍓嶄笉搴旀墽琛岋紝杩欑瑪浜ゆ槗鏄庢樉杩濆弽鏃㈠畾绾緥鎴栭闄╅绠?

### 瀹夎

浠?GitHub 瀹夎锛?

```bash
npx skills add https://github.com/yuanlusi/investment-discipline-console-skill/tree/main/investment-discipline-console
```

鎵嬪姩瀹夎锛?

```bash
cp -R investment-discipline-console "${CODEX_HOME:-$HOME/.codex}/skills/"
```

### 浣跨敤绀轰緥

```text
浣跨敤 $investment-discipline-console锛屽厛甯垜寤虹珛缁勫悎涓婁笅鏂囷紝鍐嶅紑濮嬪鏌ヤ换浣曚氦鏄撱€?

浣跨敤 $investment-discipline-console锛屾妸鎴戠殑娓偂鍜岀編鑲¤处鎴峰悎骞舵垚涓€涓粍鍚堣瑙掞紝骞跺憡璇夋垜鍝簺浠撲綅闄愬埗宸茬粡瓒呬簡銆?

浣跨敤 $investment-discipline-console锛屽府鎴戝鏌ヤ竴涓嬫垜鏄惁搴旇鍏堝紑涓€涓吘璁殑鍒濆浠撲綅銆?

浣跨敤 $investment-discipline-console锛岀湅鐪嬫垜褰撳墠鎸佷粨閲屽摢浜涗粨浣嶆渶闇€瑕佸鐩樸€?

浣跨敤 $investment-discipline-console锛屽姣旀垜 T 鏃ュ拰 T+3 鏃ョ殑鎸佷粨鍙樺寲锛屽苟鎸囧嚭鍝簺澶у彉鍖栭渶瑕佹垜瑙ｉ噴鍘熷洜銆?

浣跨敤 $investment-discipline-console锛屽府鎴戝仛涓€娆″懆搴︾邯寰嬪鐩橈紝鎬荤粨杩欏懆鎴戦噸澶嶄簡鍝簺閿欒銆?

浣跨敤 $investment-discipline-console锛屾牴鎹垜鏈€杩戝嚑娆?review锛屾€荤粨涓€涓嬫垜姝ｅ湪鍙樻垚浠€涔堟牱鐨勪氦鏄撹€咃紝浠ュ強鎴戞渶甯搁噸澶嶇殑閿欒銆?
```

### 璇存槑

- 杩欏 skill 鐢ㄤ簬缁撴瀯鍖栧喅绛栨敮鎸佸拰澶嶇洏锛屼笉浠ｆ浛鐙珛鍒ゆ柇銆?
- 瀹冧細鍩轰簬鍘嗗彶 review 娌夋穩绾緥璁板繂銆佺敤鎴风敾鍍忓拰鍛ㄥ害澶嶇洏鎽樿锛屼絾杩欎簺璁板繂鍙湇鍔′簬杩囩▼寤鸿锛屼笉鏈嶅姟浜庤崘鑲℃垨棰勬祴锛屼笉閽堝鍏蜂綋鏍囩殑鏄惁鍊煎緱涔板崠缁欏缓璁€?
- 褰撶粍鍚堜笂涓嬫枃缂哄け鏃讹紝瀹冧細鍒绘剰淇濆畧銆?
- 瀹冨己璋冣€滃厛鍒跺害锛屽悗鐮旂┒锛涘厛缁勫悎锛屽悗鍗曠瑪鈥濄€?
