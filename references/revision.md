# 修改和全文复核

## 从问题到修改

先形成问题清单及依据，后写修改。review.edits每项{id,issue_ids,start,end,before,after,reason,basis}，位置基于同一original.text；替换before必须逐字匹配，插入用start=end/before空字符串。重复句要选明确位置。所有实际修改均登记，不只记录几句代表性变化。before和after相同的空操作不登记为修改，也不能用来声称问题已解决。

同一区域多个问题共用一次编辑并关联全部issue_ids，禁止重叠编辑。两个同位置插入需合并为一条明确顺序，不能依赖排序碰巧成功。不要在原稿修改后仍使用旧offset；一个版本一套编辑。

动作应和依据匹配：有证据的具体说明可clarify/add；不可靠绝对表述可narrow/remove；没有依据的必要事实defer；没有问题的特点retain，不关联实际修改；not_applicable问题不作为改文理由。defer动作不标addressed，资料补足后须重新审读并选择实际动作，不能沿用待核实处理却宣称解决。医学/机构事实新增需对应实际材料且人工确认支持关系。编辑rule可以支撑结构/表述优化，不能凭它新增疗效或资质。

audit不产修改稿；plan可以列建议编辑，不标addressed，不表示修改完成；revise才生成实际改稿并进行post_review。重写整篇也要完整编辑映射，无literal保留范围冲突时可用全篇替换，但必须逐项列清问题对应及保留情况，不能用全篇替换躲掉事实核对。

## 保留与复核

literal保留范围与替换/插入侵入冲突时工具拒绝；如要放宽用户保留要求需实际授权并生成新task，而非在review里自己宣布批准。semantic保留要全文核对实际含义，包括人群、限制、时间、出处与真实优势作用；文字相似不是含义没变。

post_review需用review_basis_sha256绑定task/审读范围/问题清单/覆盖/主张/编辑/final的实际组合，再绑定实际final.text hash，保存full_text_check、review_note、issue_outcomes、preservation、new_claims、limitations、professional_review、publication_review。

issue_outcomes每原问题一个状态addressed/open/deferred/not_applicable，理由具体。addressed要有对应edit且人工确认问题解决；仍缺资料用deferred，不用无依据补写改成addressed。检查新增主张、上下文矛盾与词义变化，不只重看旧登记句。

new_claims每项{statement,kind,quote,basis,scope,reason}指修改稿准确位置；kind为factual/medical/editorial；涉及事实须实际source依据，编辑性说明可rule。post_review.full_text_check={status:"completed",scope,new_claims_note}必须明确记录实际阅读全文的范围和新增主张检查结论；数组空时new_claims_note须具体解释为何无新增主张。此为审读声明，程序不能验证是否真的读完；未读完不交全文已复核结果，可转plan或说明任务仍未完成。不能拿空模板当无问题。新风险/限制也属于需要依据的医学说法，不因“更安全”免核。

professional_review和publication_review默认pending/not_requested；completed分别绑定修改稿hash、审核者、日期、范围。正文变更后重核，不复制原稿完成状态。免责声明、source有链接或程序过关不是发布许可。

final.text必须等于按登记编辑生成的全文；不允许工具外未登记的润色。专业/发布未完成时也可交待审核稿，并明确状态。用户只要检查不因为review授权不足擅自扩大任务。
