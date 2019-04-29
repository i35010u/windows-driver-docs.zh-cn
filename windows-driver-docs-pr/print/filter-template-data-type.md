---
title: 筛选器模板数据类型
description: 筛选器模板数据类型
ms.assetid: cfbe8f39-9a8d-4e6b-91d8-f25926057e7b
keywords:
- 模板 WDK GDL，数据类型
- 数据类型 WDK GDL，基元
- FILTER_TYPE 数据类型 WDK GDL
- ArrayLabel 指令 WDK GDL
- ElementType 指令 WDK GDL
- FilterTypeName 指令 WDK GDL
- ElementTags 指令 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfcf70817849a163e2810f04e60c4b0395619612
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363242"
---
# <a name="filter-template-data-type"></a>筛选器模板数据类型


筛选器\_分析器筛选器识别类型类型。 此数据类型的示例包括 GPD 整数类型、 GPD 字符串类型和 GPD 符号类型。

\*数据类型：筛选器\_类型将模板与特定分析器筛选器内置数据类型相关联。 值的语法取决于分析器筛选器。 分析器筛选器会将一个或多个本机 XML 数据类型转换的此值。 特定生成的 XML 数据类型是硬编码，不能更改它。 将输出值，就好像\*数据类型：XML\_TYPE.

以下指令用于完全定义的筛选器\_数据类型：

-   **\*ElementType** （必需）。 一系列\*数据类型：XML\_将转换为类型定义的 XML 类型的这种数据类型的模板，并将其输出中生成的 XML。 是必需的 XML 类型特定筛选器类型而异。 此指令引用的 XML 数据类型必须匹配分析器筛选器需要的 XML 数据类型。

-   **\*ElementTags** （可选）。 如果筛选器类型转换为多个 XML 元素，此指令指定每个 XML 元素的名称。 如果使用此指令时，指定的标记数必须等于每个转换生成的 XML 元素的数目。 如果仅生成一个 XML 元素，则不使用标记。
    **请注意**    **\*ElementTags**指令可能需要一些将来的筛选器类型。

     

-   **\*FilterTypeName** （必需） 的特定筛选器实现的数据类型。 默认分析器筛选器当前支持以下类型：
    -   "HEX\_OR\_INT":接受的十六进制格式和通配符的 GPD 4 字节整数 (\*)。 结果转换为十进制数字，并输出为 XSD **int**数据类型。 可选 **\*MinValue**并 **\*MaxValue**模板指令被识别为此数据类型。 如果存在此类型，则分析器将验证提供的值处于内定义的范围。 而无需其他可以定义一个限制。
    -   "SYMBOLNAME":GPD/GDL 符号标记。 令牌的输出作为 XSD**字符串**数据类型。 可选 **\*MinLength**并 **\*MaxLength**模板指令被识别为此数据类型。 如果存在此类型，则分析器将验证提供的令牌的长度位于内定义的范围。 而无需其他可以定义一个限制。
    -   "命令\_字符串":GPD 命令字符串值。 执行字符串的解释。 转换为原始值并将其输出为 XSD base64Binary 数据。 值不是输出作为 XSD**字符串**数据类型，因为命令字符串可能包含不合法的 XML 字符串的字符。
    -   "正常\_字符串":GPD/GDL 带引号的字符串值。 结果转换为纯的 8 位二进制字符串中，将作为 XSD 单词输出的数组**字符串**数据类型。 可选 **\*MinLength**并 **\*MaxLength**模板指令被识别为此数据类型。 如果存在此类型，则分析器将验证所提供的字符串长度是否在定义的范围内。 而无需其他可以定义一个限制。
    -   "代码页\_字符串":GPD/GDL 带引号的字符串值。 结果通过使用代码页转换为 16 位 Unicode 字符串的相应**\*代码页**项指定和输出作为 XSD**字符串**数据类型。 可选 **\*MinLength**并 **\*MaxLength**模板指令被识别为此数据类型。 如果存在此类型，则分析器将验证所提供的字符串长度是否在定义的范围内。 而无需其他可以定义一个限制。 请注意，字符串的长度的实际生成的代码页转换后的 WideChars 数。
    -   "默认\_代码页\_字符串":GPD/GDL 带引号的字符串值。 将结果转换为 16 位 Unicode 字符串使用 CP\_ACP 代码页和输出作为 XSD**字符串**数据类型。 可选 **\*MinLength**并 **\*MaxLength**模板指令被识别为此数据类型。 如果存在此类型，则分析器将验证所提供的字符串长度是否在定义的范围内。 而无需其他可以定义一个限制。 请注意，字符串的长度的实际生成的代码页转换后的 Unicode 字符数。
    -   "UNICODE\_字符串":GPD/GDL 带引号的字符串值。 字符串被假定为的二进制表示形式的一系列 Unicode 字符并将输出直接作为 XSD**字符串**数据类型。

        每个 Unicode 字符表示由一对字节。 字节通常表示为十六进制的子字符串以使编辑更容易。 为了向后兼容，GDL 分析器遵循 GPD 分析器建立，约定，以便对中的最低有效字节显示在最高有效字节的左侧。 与不同 GPD 分析器中，此约定是独立于处理器的字节顺序。 可选 **\*MinLength**并 **\*MaxLength**模板指令被识别为此数据类型。 如果存在此类型，则分析器将验证所提供的字符串长度是否在定义的范围内。 而无需其他可以定义一个限制。 请注意，字符串的长度的实际产生的 Unicode 字符数。

    -   "二进制\_字符串":GPD/GDL 带引号的字符串值。 假定该字符串来表示 8 位的二进制数据。 转换为和输出作为 XSD base64Binary 数据中的结果。 由于控制字符不允许使用的 XML 文件，它们不能表示使用 XSD 'string' 数据类型。 因此二进制\_字符串筛选器必须用于将此类字符转换为可处理 xml 的窗体。 可选模板指令\*MinLength 和\*MaxLength 识别此数据类型。 如果存在此类型，则分析器将验证所提供的字符串长度是否在定义的范围内。 而无需其他可以定义一个限制。 请注意，字符串的长度的实际表示 base64 编码数据的字节数。

-   **\*ArrayLabel** （可选）。 如果指定此指令，则分析器筛选器需要括在圆括号，以指定的数组标签值。

要分析的值必须符合特定筛选器类型定义的语法\*FilterTypeName 指令指定。 分析器筛选器将转换并输出到一个或多个 XML 数据类型，前面指定的此值。 如果在多个 XML 元素的转换结果，将通过使用中指定的名称标记每个元素\*ElementTags 指令。

当 XML 快照，则生成分析器如果字符串筛选器类型的值中已存在这些自动可表示与相应的 XML 实体的特殊字符。 例如，& 号字符 (&) 由 t 和快照中表示。 不需要使用分析器筛选器定义的数据类型时遵循 XML 语法规则。

请考虑以下模板。

```cpp
*Template:  INTEGER
{
    *Type:  DATATYPE
    *DataType:   FILTER_TYPE
    *ElementType:  XSD_INT
    *FilterTypeName: "HEX_OR_INT"
}
```

此模板指定的筛选器类型"十六进制\_或\_INT"。 根据为提供的信息\*FilterTypeName，筛选器会将转换此数据类型为 int 内置 XSD 类型。若要确保生成的 XML，维护筛选器的目的，必须命名表示在 XSD 数据类型为 int 的模板 **\*ElementType**指令。

在下面的示例中，XSD\_INT 模板被命名为。 此模板定义，如下所示。

```cpp
*Template:  XSD_INT
{
    *Type:  DATATYPE
    *DataType:   XML_TYPE
    *XMLDataType: "int"  
}
```

XSD\_INT 模板定义本机 XSD 类型为 int，这可确保将正确实现分析器筛选器的意图。

\*数据类型：筛选器\_类型模板不会生成相应的架构。

请考虑以下 GDL 条目。

```cpp
*MaxCopies:   0x1ff
```

并考虑以下模板 MAXCOPIES。

```cpp
*Template:  MAXCOPIES
{
    *Name:  "*MaxCopies"
    *Type:  ATTRIBUTE
    *ValueType:  INTEGER
}
```

如果早期 GDL 条目解释由前面的模板中，将生成的 XML 输出。

```cpp
    <GDL_ATTRIBUTE Name="*MaxCopies"  xsi:type="GDLW_int" >511</GDL_ATTRIBUTE> 
```

请注意，分析器筛选器具有到适合的 XSD 数据类型的小数格式转换 GPD 定义十六进制格式**xsd: int**。还要注意，实际上引用的类型是包装的类型 GDLW\_int。

 

 




