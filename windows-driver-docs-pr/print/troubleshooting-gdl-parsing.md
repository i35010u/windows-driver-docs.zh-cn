---
title: 排查 GDL 分析问题
description: 排查 GDL 分析问题
ms.assetid: 8c678a2f-b15b-4693-9bed-0edec06b3485
keywords:
- GDL WDK，分析器
- 分析器 WDK GDL，排除分析故障
- 分析 GDL 数据 WDK
- GDL 分析 WDK 疑难解答
- GDL WDK，分析错误
- GDL WDK，错误
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 141bda331dc507d7e0c94b7cbc98b616bdfcbe0d
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652955"
---
# <a name="troubleshooting-gdl-parsing"></a>排查 GDL 分析问题

以下信息介绍了在分析 GDL 文件时可能会遇到的意外行为。

<a href="" id="symptom--you-include-the-schema-file--but-the-parser-emits-an-error-message-that-says---no--root--template-found--gdl-entries-will-not-be--templatized--and-ignores-the-schema---"></a>症状：包含架构文件，但分析器发出一条错误消息，指出找不到 "根" 模板，GDL 条目将不模板化 "并忽略架构。   
解决方案：检查是否定义了根模板。 如果定义了此类模板，请确保 \#包括： gdl 指令位于任何实例数据之前。 否则，分析器将忽略此架构。

<a href="" id="symptom--you-define-an-attribute-multiples-times-in-the-gdl-file--and-i-see-it-appear-in-the-xml-snapshot-only-once---"></a>症状：在 GDL 文件中定义属性倍数，并将其只显示在 XML 快照一次。   
解决方案：必须为 XML 快照中多次出现的任何属性定义模板。 您必须定义 \*累加指令。 否则，将只显示最新的定义。

<a href="" id="symptom---the-parser-complains-that---production-defined-in-template----template-name---is-not-satisfied-by-actual-construct-----and-it-appears-that-the-number-of-occurrences-of-each-member-is-within-the-bounds-that-the-production-defines-"></a>症状：分析投诉原因中定义的 "\[模板中定义的生产" 不满足实际的构造。\]"，则会显示每个成员出现的次数在生产定义的边界内。  
解决方案：首先，请使用 GDL 分析器的-i 选项检查绑定到每个 GDL 项的模板。 绑定可能未按预期方式发生。 如果绑定似乎已工作，请记住，生产是通过在生产中命名的模板的实例，以及从命名模板派生的任何模板的任何实例满足的。 因此，如果生产指定只能存在特定模板的一个实例，并且实际数据文件包含从该模板派生的模板的两个实例，则将违反该生产。 即使派生模板重新定义 \*Name 指令，也会跟踪模板继承。

<a href="" id="symptom--you-receive-a-warning-message-that-references-an--invalidcombination-that-does-not-exist-in-the-gdl-file-that-is-being-parsed-"></a>症状：你收到一条警告消息，该消息引用了不存在于正在分析的 GDL 文件中的 \*InvalidCombination。  
解决方案： GDL 分析器在内部将 \*约束指令转换为 \*的 InvalidCombination 指令。 因此，在转换后检测到错误时，消息将 \*约束称为 \*InvalidCombination。 此外，\*InvalidCombination 的每个元素在内部存储的顺序并不一定是 GDL 文件中指定的顺序。

<a href="" id="symptom--spurious-trailing-space-appears-when-a-value-macro-reference-is-replaced-with-its-defined-value-"></a>症状：当值宏引用替换为其定义的值时，将出现虚假尾随空格。  
解决方案：值宏定义包含尾随注释。 将注释移动到单独的行。 在大多数情况下，分析器不区分附加的空白字符。

<a href="" id="symptom---surrounding-non-conforming-syntax-with-a--ignoreblock-construct-does-not-hide-the-content-from-the-parser-as-syntax-errors-are-still-generated-"></a>症状：使用 \*IgnoreBlock 构造的非一致性语法不会隐藏分析器中的内容，因为仍会生成语法错误。  
解决方案： \*IgnoreBlock 的内容仍必须符合 GDL。 \*IgnoreBlock 只会阻止其内容显示在内部数据树中，并阻止执行任何非预处理器指令。 若要真正隐藏某些内容，请使用预处理器条件。 如果隐藏的片段本身包含不应执行的预处理器指令，则在将片段与预处理器条件括起来之前，请更改预处理器前缀。

<a href="" id="symptom---features--constructs--and-attributes-that-are-defined-within-files-that-are-designated-with--precompiled-do-not-appear-in-the-xml-snapshot-and-cannot-be-referenced-by-the-host-file-"></a>症状：在使用 \*预编译指定的文件中定义的功能、构造和属性不会显示在 XML 快照中，也不能由主机文件引用。  
解决方案：此症状按设计发生。 只能在预编译文件中存储模板和宏定义。

<a href="" id="symptom---you-cannot-reference-templates--preprocessor-defines--macros--or-other-content-that-is-defined-elsewhere-from-within-files-that-are-designated-with--precompiled--"></a>症状：无法从用 \*预编译指定的文件中引用模板、预处理器定义、宏或其他内容。   
解决方案：此症状按设计发生。 预编译文件设计为自包含且完全独立于主机文件的上下文。 若要访问在另一个文件中定义的模板或其他内容，你必须将 \#Include 指令命名为直接在 \#预编译文件中命名该文件。 在 \#包含文件（即，嵌套 \#包含语句）内包含的内容（通过使用 \#包含）间接包含的内容将可由根预编译（\#预编译）文件访问。 预编译的文件可以包含（通过使用 \#包括）其他预编译文件。

<a href="" id="symptom---features-or-options-do-not-appear-in-the-snapshot-in-the-order-that-you-defined-them---or--the-first-option-is-not-assigned-as-the-default-option---"></a>症状：功能或选项不会按照您定义的顺序出现在快照中。 或者，未将第一个选项指定为默认选项。   
解决方案：之前可能已在 GDL 文件的另一部分或在所查看的功能或选项定义之前处理的包含文件中定义了某些选项。 处理的第一个选项是第一个选项，处理的第二个选项成为快照中的第二个选项，依此类推。

<a href="" id="symptom--you-receive-a-warning-message-that-says-that-the-gdl-parser-cannot-find-a-template-that-is-referenced-by-the--elementtype-directive--but-that-template-is-defined--"></a>症状：你会收到一条警告消息，指出 GDL 分析器找不到由 \*ElementType 指令引用的模板，但该模板已定义。   
解决方案： \*ElementType 指令只能引用声明为 \*类型： DATATYPE 的模板。

<a href="" id="symptom--values-of-attributes-that-are-defined-to-be--filtertypename---codepage-string--are-not-converted-to-unicode-properly---"></a>症状：定义为 \*FilterTypeName "代码页\_字符串" 的属性值不会正确地转换为 Unicode。   
解决方案：如果在分析此属性时未定义 \*代码页指令，则分析器将假定该字符串已采用 Unicode。 请确保 \*代码页定义显示在任何代码页\_字符串特性之前。

<a href="" id="symptom--you-defined-the--requireddelimiter-in-your-array-or-composite-data-type-template-to-be-a-sequence-of-multiple-space-characters-or-tabs--and-the-parser-does-not-seem-to-recognize-the-actual-data-even-though-it-conforms-exactly-to-the-template-definition---"></a>症状：你将数组或复合数据类型模板中的 \*RequiredDelimiter 定义为多个空格字符或制表符的序列，而分析器似乎不会识别实际数据，即使它完全符合模板定义。   
解决方案：分析器将任意空白（空格或制表符）任意字符串转换为单个空格字符。 因此，在检查值时，它将不满足模板定义。 若要避免这种情况，请仅为 \*RequiredDelimiter 指定一个空格字符，或对 \*RequiredDelimiter 使用非空白字符，并为 \*OptionalDelimiter 使用空格和制表符。

<a href="" id="symptom--dom-interface---xpath-query-cannot-find-any-elements-in-the-snapshot---for-example--selectsinglenode---snapshotroot-gdl-attribute----returns-nothing--"></a>症状： DOM 接口： Xpath 查询在快照中找不到任何元素（例如，selectSingleNode （"/SnapshotRoot/GDL\_属性"）不返回任何内容）。  
解决方案： Xpath 假定不带命名空间前缀的元素名称引用 null 或空命名空间，而不是默认命名空间。 快照定义默认命名空间，大多数元素属于默认命名空间。

若要使用 Xpath 访问这些元素，客户端必须首先将此默认命名空间映射到显式前缀。 若要以这种方式映射默认命名空间，请使用 document pbjects setProperty 方法。 需要设置的属性为 SelectionNamespaces。 使用此属性可为默认命名空间分配显式前缀。 在快照中[https://schemas.microsoft.com/2002/print/gdl/1.0](https://schemas.microsoft.com/2002/print/gdl/1.0)默认命名空间，因此，对 setProperty 的调用可能类似于下面的代码示例。

```cpp
XMLDoc->setProperty(L"SelectionNamespaces", "xmlns:gdl=\"https://schemas.microsoft.com/2002/print/gdl/1.0\"");
```

上面示例中的第二个参数实际上是一个变体，但为了简单起见，省略了这一增加的复杂性。 Xpath 查询现在必须显式引用命名空间前缀 gdl，并引用默认命名空间中的元素。 然后，该查询将成为下面的代码示例。

```cpp
selectSingleNode("/gdl:SnapshotRoot/gdl:GDL_ATTRIBUTE")
```

<a href="" id="symptom--the-dom-interface---nodetypedvalue-property-always-returns-values-as-bstr-types--regardless-of-their-xsi-type--"></a>症状： DOM 接口： nodeTypedValue 属性始终将值作为 BSTR 类型返回，而不考虑其 xsi： type。   
解决方案： MSXML 4.0 的当前实现仅识别使用数据类型定义（DTD）定义的数据类型。 GDL 分析器使用 XSD，这是当前的 W3C 建议。

<a href="" id="symptom--quoted-strings-that-contain-characters-with-ansi-values-between-0-and-0x19-cause-xml-parsing-errors---except-for-0x0a--0x0d--and-0x09--"></a>症状：包含 ANSI 值介于0和0x19 之间的字符的带引号的字符串将导致 XML 分析错误（0x0a、0x0d 和0x09 除外）。  
解决方案：此错误是一个 XML 功能。 此类字符串必须使用 XML 的 binary 或 binhex 数据格式表示。 未来版本的 XML 可能接受包含这些字符的字符串。

<a href="" id="symptom--some-xml-instance-data-or-schema-that-are-defined-by-using-the-passthrough-or-xsd-defined-data-types-cause-xml-parser-or-validation-error-messages-when-loaded-into-dom-"></a>症状：在加载到 DOM 时，使用传递或 XSD\_定义的数据类型定义的某些 XML 实例数据或架构会导致 XML 分析器或验证错误消息。  
解决方案：通过使用直通或 XSD\_定义的数据类型来创建自己的 XML，绕过 GDL 分析器 XML 生成代码，并向你展示了 DOM 分析器中的 XML 和其他内容的复杂性。 在使用这些数据类型之前，您应当精通 XML 来处理此类问题。

<a href="" id="symptom---the-parser-says--preface-cannot-be-used-with-a-precompiled-file---but-the-root-file-does-not-contain-a--precompiled-directive-"></a>症状：分析器显示 "前言无法用于预编译文件"，但根文件不包含 \#预编译指令。  
解决方案： \#预编译指令实际上可能位于前言本身。 分析器无法区分 GDL 内容是否来自前言或根文件。
