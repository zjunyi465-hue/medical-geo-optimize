# 数据结构与交付

task为schema_version=1.0，review为schema_version=1.1。旧review须逐项重新审读并补齐新字段，不只换版本号。UTF-16 start/end取自原字符串，不能截断emoji等字符的代理对，不按汉字数或行号混算；string SHA256为精确文本UTF-8。task规范化对象哈希按递归键排序、数组顺序保留，用工具fingerprints输出，别手算。

review根为task_sha256、issues、coverage、claims、edits、final、post_review、scope_note。task_sha256绑定整个task；任何问题/主体/资料/保留项变化需实际重核再更新，不只刷新hash。issues/claims里的quote指original.text，basis source.quote指真实已读source.text，均精确匹配。rule字段见decision-basis。

coverage数组每项{id,point,kind,status,reason,original_quotes,basis}，covered/partial需原文证据，missing需说明范围和必要性。kind=editorial/medical，按信息实际性质分类；医学必要点在covered/partial/missing时需实际来源依据，否则not_assessed并具体说明待核实事项。不能改标editorial来绕过医学依据。程序检查来源关联，不判断来源临床适用性。claims启用按医学参考登记，未启用空数组并说明；其status不是文章总体真假。

audit/plan的final及post_review必须null。plan可提供edits方案但不写修改已完成，状态保持open/deferred/not_applicable。revise需final{text,sha256}、post_review。工具会重建全部登记编辑并比对全文，输出修改稿。

完整JSON演练见assets/task-example.json和review-example.json。填写hash的阶段：固定输入→fingerprints取task哈希→模型填写issues/edits→形成精确全文→算final hash→模型全文复核post_review→工具检查。工具fingerprints同时给planned_text、planned_sha256及review_basis_sha256，帮助核对编辑后的实际文本，不负责生成编辑理由。fingerprints只是计算辅助，不执行完整权限/证据/保留校验；不能把它的预览当成审核通过。只有完整check命令成功才代表结构校验通过。

最终输出report.html、review-results.json、issues.csv和revise下revised.md。report显示任务范围、具体问题、依据、编辑前后及待核实/人审/渠道状态；改了多少处不是效果评分。审查待办以实质内容为主，不堆执行错误日志。

结果可留本地，HTML所有外来文字转义，CSV中和公式前缀；大段来源和原文按需展开。不把真实患者/账号/内部路径写进公开演示；公开文件另审，不自动打包本次任务产物。

程序检查仅覆盖：结构、枚举、ID关系、任务/文本版本、精确摘录、编辑不重叠、literal保留及final一致性、复核对象绑定。没有自动语义核验、医学认证、网页读取、优势比例计数或效果预测。退出码0也须如实交付未决项。
