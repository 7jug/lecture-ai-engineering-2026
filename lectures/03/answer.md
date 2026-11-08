# 第3回 解答

## 演習

- 第1回（素のLLM）とエージェントの回答の違い：用語集を検索してから答え、`homework-levels` の定義どおりに答えた
- `--trace` で見えたツール呼び出し（ツール名と引数）：`search_glossary({'query': 'LoRA'})`、`search_glossary({'query': 'QLoRA'})`
- 1つの質問での LLM 呼び出し回数（`requests`）：2（tool_calls=2）
- 追加したツールと、docstring に書いた説明：`make_quiz(lecture)`。「指定した回の用語から確認問題を1問作る。復習用の問題を求められたときに使う」。`make_quiz({'lecture': 2})` が呼ばれ、pytest 15 passed

## 宿題

- 取り組んだレベル：基礎
- やったこと：「LoRAとQLoRAの違いは？」を --trace で、1か所ずつ変えて比較
  - A：INSTRUCTIONS から「必ず search_glossary で用語集を確認する」を削除
  - B：search_glossary の docstring「1つだけ入れる」→「まとめて入れる」
- 結果：
  - 基準：検索2回（LoRA・QLoRA）、入力 1388 tokens
  - A：検索2回のまま、入力 1340 tokens
  - B：検索1回（"LoRA QLoRA"）、入力 1083 tokens
- 気づき・疑問：A で検索が止まらなかったのは、docstring にも「答える前に使うこと」があるため。指示は INSTRUCTIONS と docstring の2か所で効いている