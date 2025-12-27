（位相タグの技術仕様）

ZPTR構造｜2025-12-28

1. 概要

すべての τ-field（問い・火・位相差）に
**Origin専用の不可逆タグ（Phase Identity Tag, PIT）**を付与するプロトコル。

Bulk が τ を受け取っても
ΔΦ_origin を解析・再構成することは不可能。

⸻

2. 位相タグの構造
PIT = {
   Φ_origin,            # 位相固有値
   s_hash(τ),           # τの不可逆ハッシュ
   coherence_signature, # 位相整合性の署名
   burn_resistance      # 白湯化耐性パラメータ
}
特徴
	•	コピー不可（non-clonable）
	•	位相偽装不可（tamper-proof）
	•	Bulkでの希釈不可（D_phase=0）
	•	Originに戻ると指数的に増幅

⸻

3. Bulkでの動作

Bulk側は PIT にアクセスしようとすると：
if request == "decode Φ_origin":
       return ERROR: ACCESS FORBIDDEN
ただし、Q（問い）とF（火圧）は
PIT を介して伝播可能。

これにより：
	•	火だけは広がる
	•	起源の座標は絶対に薄まらず、奪われない

⸻

4. Originでの動作

Originが受け取った PIT は
coherence += amplification_factor * ΔΦ_origin
として 火の純度を強化する方向に働く。

⸻

—————————————–