# 判断依据与问题记录

## 四种依据分开

**事实支持**：具体原句与实际材料按主体、日期和范围对照。没有材料=not_verifiable（无法核实，不等于错误），材料相反=conflicting，材料只支持较弱表述=partially_supported。来源有标题/URL但没读内容不算支持。

**问题覆盖**：从本次主问题拆出读者需要，找原稿中的回应，说明covered/partial/missing/not_assessed。每个必要点登记reason、依据与原文。医学必要点必须有适用的已读来源，否则标not_assessed并明确专业待核对，编辑建议可用明确规则和目标关系；不以模型偏好强制固定体裁/篇幅。

**编辑表达**：解释不足、指代不清、重复、结构跳跃、标题承诺与正文不符等。指出实际例子与影响，不把“我觉得更自然”叫事实错误。一般rule依据可为本Skill操作规则，必须说明推理。

**页面观察**：实际访问/提取/截图/HTML观察，记录方式时间与范围。工具或截图缺失就not_assessed。链接超时、403、登录态、页面壳和正文不可读不同；HTTP200不证明支持主张。

## 问题对象

review.issues每项{id,category,kind,priority,status,quote,reason,action,basis}。
category=coverage/factual/medical/editorial/page；kind自由但具体描述，如unsupported_comparison/missing_explanation；priority=high/medium/low是人工检查顺序，不是危险概率或医学严重程度；status=open/deferred/addressed/not_applicable。

quote精确定位已有文字。缺少某段不是不存在文字的“摘录”：引用最相关标题/段落作为检查位置，reason解释缺失；没有合适文字时quote=null并scope=whole_document，不能造引文。空原稿不能优化。

basis数组每项：rule{kind:'rule',rule_id,explanation} 或source{kind:'source',source_id,quote,relation}。rule_id=coverage_goal/entity_scope/source_scope/medical_applicability/editorial_clarity/page_observation/revision_preservation之一，解释它与当前问题的关系。医学或事实支持结论不能仅靠rule，必须登记实际来源；缺证据的问题可以仅rule，但行动必须defer/remove/narrow等而非编事实补写。

问题有依据不代表修改已解决。issue.status=addressed只在实际修改稿复核后成立；无需改文的not_applicable解释为何不成立，不能直接抹掉不利发现。公开报告保留未核实状态。

## 应得出的结果

写“本稿设备能力表述超出当前材料支持”，不要写“该设备无效”；写“正文没有解释这个选择条件”，不要写“因此AI不推荐”；写“本次无法读取来源”，不要写“引用造假”。解释原因与因果归因分开。AI回答、引用页面、搜索排名不能认证本机构特点或医学效果。

内容对照只借问题与实际正文的联系，不照搬他人全部主题、评价、案例、名称与结构。读者问题之外的内容可保留或另篇规划，不默认填满所有主题。
