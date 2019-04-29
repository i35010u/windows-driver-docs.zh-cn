---
title: 排查 GDL 分析问题
description: 排查 GDL 分析问题
ms.assetid: 8c678a2f-b15b-4693-9bed-0edec06b3485
keywords:
- GDL WDK 分析器
- 分析器 WDK GDL，故障排除分析
- 分析 GDL 数据 WDK
- 故障排除分析 WDK GDL
- GDL WDK，分析错误
- GDL WDK 错误
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8a060a271f712cce685299b3d6b81ce52592cf9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392782"
---
# <a name="troubleshooting-gdl-parsing"></a>排查 GDL 分析问题


以下信息介绍了一些分析 GDL 文件时可能遇到的意外行为的原因。

<a href="" id="symptom--you-include-the-schema-file--but-the-parser-emits-an-error-message-that-says---no--root--template-found--gdl-entries-will-not-be--templatized--and-ignores-the-schema---"></a>症状：包含的架构文件，但分析器会发出错误消息，指出"ROOT 找到任何模板，GDL 条目将不一定要模板化"，并忽略架构。   
解决方案：检查以查看是否定义根模板。 如果定义此类模板，则确保\#Include: schema.gdl 指令位于之前的任何实例数据。 否则，分析器将忽略该架构。

<a href="" id="symptom--you-define-an-attribute-multiples-times-in-the-gdl-file--and-i-see-it-appear-in-the-xml-snapshot-only-once---"></a>症状：在 GDL 文件中，定义属性序列图时间并看到它一次快照在 XML 中显示。   
解决方案：必须定义一个模板，用于将多次出现在 XML 快照中的任何属性。 必须定义\*累加性指令。 否则，只有最新的定义会显示。

<a href="" id="symptom---the-parser-complains-that---production-defined-in-template----template-name---is-not-satisfied-by-actual-construct-----and-it-appears-that-the-number-of-occurrences-of-each-member-is-within-the-bounds-that-the-production-defines-"></a>症状：分析器错误的报告"\[生产模板中定义:"{template name}"不满足的实际构造。\]"，且它出现的每个成员的出现次数是生产定义的边界内。  
解决方案：首先，检查哪个模板通过使用-i 绑定到每个 GDL 条目 GDL 分析器选项。 绑定可能不出现您预期的方式。 如果绑定似乎工作，请记住在生产中名为模板的实例和任何派生自命名模板的任何的模板实例满足生产环境。 因此，如果生产指定特定的模板的一个实例可能会出现，并且如果实际数据文件包含一个模板，该模板派生的两个实例，将违反生产。 即使派生的模板重新定义跟踪模板继承\*名称指令。

<a href="" id="symptom--you-receive-a-warning-message-that-references-an--invalidcombination-that-does-not-exist-in-the-gdl-file-that-is-being-parsed-"></a>症状：你收到一条警告消息引用\*InvalidCombination 正在分析的 GDL 文件中不存在。  
解决方案：GDL 分析器将转换\*约束到的指令\*InvalidCombination 指令在内部。 因此，转换后检测到错误后，该消息是指\*约束作为\*InvalidCombination。 此外，订单的每个元素的\*InvalidCombination 在内部存储中不一定是 GDL 文件中指定的顺序。

<a href="" id="symptom--spurious-trailing-space-appears-when-a-value-macro-reference-is-replaced-with-its-defined-value-"></a>症状：值宏引用替换为其定义的值时，会出现虚假的尾随空格。  
解决方案：在值宏的定义包含尾随的注释。 将注释移到单独的行。 在大多数上下文中，分析器是其他空格字符存在不区分大小写。

<a href="" id="symptom---surrounding-non-conforming-syntax-with-a--ignoreblock-construct-does-not-hide-the-content-from-the-parser-as-syntax-errors-are-still-generated-"></a>症状：关于不符合要求的语法与\*IgnoreBlock 构造不会隐藏来自分析器的内容，如仍会生成语法错误。  
解决方案：内容\*IgnoreBlock 必须仍符合 GDL。 \*IgnoreBlock 只需将禁止在内部数据树中显示其内容，并防止执行任何非预处理器指令。 若要真正隐藏的内容，请使用预处理器条件语句。 如果碎片是要隐藏本身中包含不应执行的预处理器指令，封闭预处理器条件语句的片段之前更改的预处理器的前缀。

<a href="" id="symptom---features--constructs--and-attributes-that-are-defined-within-files-that-are-designated-with--precompiled-do-not-appear-in-the-xml-snapshot-and-cannot-be-referenced-by-the-host-file-"></a>症状：功能、 构造和使用指定的文件中定义的属性\*预编译不会出现在 XML 快照中，不能引用由主机文件。  
解决方案：这种现象的发生的设计。 您可以存储仅模板和预编译文件中的宏定义。

<a href="" id="symptom---you-cannot-reference-templates--preprocessor-defines--macros--or-other-content-that-is-defined-elsewhere-from-within-files-that-are-designated-with--precompiled--"></a>症状：不能引用模板、 预处理器定义宏或在其他地方定义从使用指定的文件中其他内容\*预编译。   
解决方案：这种现象的发生的设计。 预编译的文件设计为自包含且完全独立的主机文件的上下文。 若要访问模板或另一个文件中定义其他内容，必须将放\#直接在该文件的 Include 指令\#预编译文件。 间接包含通过所包含的内容 (通过使用\#Include) 内\#包含文件 (即，嵌套\#Include 语句) 可访问的预编译的根 (\#预编译的） 文件。 预编译的文件可以包括 (通过使用\#Include) 其他预编译的文件。

<a href="" id="symptom---features-or-options-do-not-appear-in-the-snapshot-in-the-order-that-you-defined-them---or--the-first-option-is-not-assigned-as-the-default-option---"></a>症状：您定义它们的顺序在快照中不显示功能或选项。 或者，作为默认选项未分配第一个选项。   
解决方案：某些选项可能已被定义之前另一部分 GDL 文件中或在包含该功能之前已处理的文件或要查看的选项定义。 处理的第一个选项作为第一个选项，处理的第二个选项作为第二个选项中的快照，依此类推。

<a href="" id="symptom--you-receive-a-warning-message-that-says-that-the-gdl-parser-cannot-find-a-template-that-is-referenced-by-the--elementtype-directive--but-that-template-is-defined--"></a>症状：你收到一条警告消息，指出 GDL 分析器找不到引用的模板\*ElementType 指令，但在该模板定义。   
解决方案：声明为的模板\*类型：数据类型，可以引用\*ElementType 指令。

<a href="" id="symptom--values-of-attributes-that-are-defined-to-be--filtertypename---codepage-string--are-not-converted-to-unicode-properly---"></a>症状：定义为在属性的值\*FilterTypeName:"代码页\_字符串"不正确地转换为 Unicode。   
解决方案：如果\*代码页指令未定义此属性进行分析时，分析器将假定该字符串已为 unicode 格式。 请确保\*代码页定义出现在任何代码页之前\_字符串属性。

<a href="" id="symptom--you-defined-the--requireddelimiter-in-your-array-or-composite-data-type-template-to-be-a-sequence-of-multiple-space-characters-or-tabs--and-the-parser-does-not-seem-to-recognize-the-actual-data-even-though-it-conforms-exactly-to-the-template-definition---"></a>症状：你定义\*RequiredDelimiter 数组或复合数据类型的模板中，若要为一系列多个空格字符或选项卡，并分析程序似乎不能识别的实际数据，即使它与模板定义完全相符。   
解决方案：分析器在内部将单个空格字符转换为空白 （空格或制表符字符） 的任意字符串。 因此选中值后，它将不符合模板定义。 若要避免这种情况下，指定只有一个空格字符\*RequiredDelimiter 或使用非空白字符以\*RequiredDelimiter，并使用空格和制表符字符\*OptionalDelimiter。

<a href="" id="symptom--dom-interface---xpath-query-cannot-find-any-elements-in-the-snapshot---for-example--selectsinglenode---snapshotroot-gdl-attribute----returns-nothing--"></a>症状：DOM 接口：Xpath 查询找不到快照中的任何元素 (例如，selectSingleNode ("/ SnapshotRoot/GDL\_属性") 不返回任何内容)。  
解决方案：Xpath 假定该元素没有命名空间前缀引用为 null 或为空命名空间，不是默认命名空间的名称。 快照定义的默认命名空间，并且大多数元素属于默认命名空间。

若要访问这些元素使用 Xpath，客户端首先必须为显式前缀映射此默认命名空间。 若要以这种方式将默认命名空间映射，使用文档 pbjects setProperty 方法。 需要设置该属性是 SelectionNamespaces。 使用此属性分配一个显式前缀的默认命名空间。 在快照中，默认命名空间是 http://schemas.microsoft.com/2002/print/gdl/1.0因此 setProperty 调用看起来像下面的代码示例。

```cpp
XMLDoc->setProperty(L"SelectionNamespaces", "xmlns:gdl=\"http://schemas.microsoft.com/2002/print/gdl/1.0\"");
```

在前面的示例中的第二个参数是实际变体，但为简单起见，省略了此增加的复杂性。 引用的默认命名空间中的元素时，Xpath 查询必须现在显式引用命名空间前缀 gdl。 然后，查询将变下面的代码示例。

```cpp
selectSingleNode("/gdl:SnapshotRoot/gdl:GDL_ATTRIBUTE")
```

<a href="" id="symptom--the-dom-interface---nodetypedvalue-property-always-returns-values-as-bstr-types--regardless-of-their-xsi-type--"></a>症状：DOM 接口： nodeTypedValue 属性始终返回值为 BSTR 类型，而不考虑其 xsi: type。   
解决方案：通过使用数据类型定义 (DTD) 定义时，MSXML 4.0 的当前实现会识别唯一数据类型。 GDL 分析器使用 XSD，这是当前的 W3C 建议。

<a href="" id="symptom--quoted-strings-that-contain-characters-with-ansi-values-between-0-and-0x19-cause-xml-parsing-errors---except-for-0x0a--0x0d--and-0x09--"></a>症状：带引号的字符串包含 ANSI 值介于 0 到 0x19 之间的字符会导致 XML 分析错误 （除外 0x0a 0x0d 和 0x09）。  
解决方案：此错误是 XML 功能。 此类字符串必须使用 XML 的二进制文件或 binhex 数据格式来表示。 XML 的未来版本可能会接受包含以下字符的字符串。

<a href="" id="symptom--some-xml-instance-data-or-schema-that-are-defined-by-using-the-passthrough-or-xsd-defined-data-types-cause-xml-parser-or-validation-error-messages-when-loaded-into-dom-"></a>症状：某些 XML 实例数据或通过使用传递或 XSD 定义的架构\_定义数据类型会导致 XML 分析器或验证错误消息时加载到 dom。  
解决方案：使用传递或 XSD 创建自己的 XML\_定义数据类型会绕过 GDL 分析器 XML 生成代码并让您面临的复杂性 XML 和 DOM 分析器中的特别之处。 您应该精通使用 XML 来处理这些数据类型之前使用此类问题。

<a href="" id="symptom---the-parser-says--preface-cannot-be-used-with-a-precompiled-file---but-the-root-file-does-not-contain-a--precompiled-directive-"></a>症状：分析器显示"前缀不能用于预编译的文件"，但根文件不包含\#预编译指令。  
解决方案：\#预编译指令可以实际驻留在前缀本身。 分析器无法区分是否 GDL 内容来自前缀或根文件。

 

 




