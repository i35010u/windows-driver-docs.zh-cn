---
title: 筛选器模板数据类型
description: 筛选器模板数据类型
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
ms.openlocfilehash: 28ad37fd09b03460e75e22c8e4c70b964f308900
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836045"
---
# <a name="filter-template-data-type"></a>筛选器模板数据类型


\_分析器筛选器识别筛选器类型类型。 此数据类型的示例包括 GPD 整数类型、GPD 字符串类型和 GPD 符号类型。

\*数据类型：筛选器 \_ 类型将模板与特定的分析器筛选器内置数据类型相关联。 值的语法由分析器筛选器确定。 分析器筛选器会将此值转换为一个或多个本机 XML 数据类型。 生成的特定 XML 数据类型是硬编码的，不能对其进行更改。 值将输出为 \* 数据类型： XML \_ 类型。

以下指令用于完全定义筛选器 \_ 类型数据类型：

-   **\* ElementType** (必需的) 。 数据类型的列表 \* ： xml \_ 类型模板，用于定义此数据类型将转换为并在生成的 XML 中输出的 xml 类型。 所需的 XML 类型随特定筛选器类型的不同而异。 此指令引用的 XML 数据类型必须与分析器筛选器所需的 XML 数据类型匹配。

-   **\* ElementTags** (可选) 。 如果筛选器类型转换为多个 XML 元素，则此指令指定每个 XML 元素的名称。 如果使用此指令，则指定的标记数必须等于每个转换生成的 XML 元素的数目。 如果仅生成一个 XML 元素，则不使用标记。
    **注意**  以后某些筛选器类型可能需要 **\* ElementTags** 指令。

     

-   **\* FilterTypeName** (要求) 特定筛选器实现的数据类型。 默认的分析器筛选器当前支持以下类型：
    -   "HEX \_ 或 \_ INT"： GPD 4 个字节的整数，该整数接受十六进制格式和通配符 (\*) 。 结果转换为十进制数字，并以 XSD **int** 数据类型输出。 对于此数据类型 **\* ，可** 识别可选的 **\* MinValue 和** 模板指令。 如果此类型存在，则分析器将验证提供的值是否在定义的范围内。 可以定义一个限制而不是另一个。
    -   "SYMBOLNAME"： GPD/GDL 符号标记。 标记作为 XSD **字符串** 数据类型输出。 此数据类型可识别可选的 **\* MinLength** 和 **\* MaxLength** 模板指令。 如果此类型存在，则分析器将验证提供的标记的长度是否在定义的范围内。 可以定义一个限制而不是另一个。
    -   "命令 \_ 字符串"： GPD 命令字符串值。 不执行任何字符串解释。 原始值转换为 XSD base64Binary 数据，并将其输出为 XSD。 该值不是作为 XSD **字符串** 数据类型输出的，因为命令字符串可能包含对 XML 字符串不合法的字符。
    -   "NORMAL \_ string"： GPD/GDL 带引号的字符串值。 结果转换为纯8位二进制字符串，并将单词数组输出为 XSD **string** 数据类型。 此数据类型可识别可选的 **\* MinLength** 和 **\* MaxLength** 模板指令。 如果此类型存在，则分析器将验证提供的字符串的长度是否在定义的范围内。 可以定义一个限制而不是另一个。
    -   "代码页 \_ 字符串"： GPD/GDL 带引号的字符串值。 通过使用相应的 **\* 代码** 页条目指定并输出为 XSD **字符串** 数据类型的代码页，将结果转换为16位 Unicode 字符串。 此数据类型可识别可选的 **\* MinLength** 和 **\* MaxLength** 模板指令。 如果此类型存在，则分析器将验证提供的字符串的长度是否在定义的范围内。 可以定义一个限制而不是另一个。 请注意，字符串的长度是在代码页转换后实际生成的 WideChars 的数目。
    -   "默认 \_ 代码页 \_ 字符串"： GPD/GDL 带引号的字符串值。 通过使用 CP \_ ACP 代码页和作为 XSD **字符串** 数据类型的输出，将结果转换为16位 Unicode 字符串。 此数据类型可识别可选的 **\* MinLength** 和 **\* MaxLength** 模板指令。 如果此类型存在，则分析器将验证提供的字符串的长度是否在定义的范围内。 可以定义一个限制而不是另一个。 请注意，字符串的长度是在代码页转换后实际生成的 Unicode 字符数。
    -   "UNICODE \_ 字符串"： GPD/GDL 带引号的字符串值。 此字符串假定为一组 Unicode 字符的二进制表示形式，并且是直接输出为 XSD **字符串** 数据类型。

        每个 Unicode 字符由一对字节表示。 通常将字节表示为十六进制子字符串，以便更轻松地进行编辑。 为了向后兼容，GDL 分析器遵循 GPD 分析器建立的约定，以便对中的最小有效字节显示在最高有效字节的左侧。 与 GPD 分析器不同，此约定与处理器的字节排序无关。 此数据类型可识别可选的 **\* MinLength** 和 **\* MaxLength** 模板指令。 如果此类型存在，则分析器将验证提供的字符串的长度是否在定义的范围内。 可以定义一个限制而不是另一个。 请注意，字符串的长度是实际生成的 Unicode 字符数。

    -   "二进制 \_ 字符串"： GPD/GDL 带引号的字符串值。 假定字符串表示二进制8位数据。 转换为 XSD base64Binary 数据并将其输出为 XSD 数据的结果。 由于 XML 文件中不允许使用 "控制字符"，因此不能使用 XSD "string" 数据类型来表示它们。 因此， \_ 必须使用二进制字符串筛选器将此类字符转换为可由 XML 处理的形式。 \*为此数据类型识别的可选模板指令 MinLength 和 \* MaxLength。 如果此类型存在，则分析器将验证提供的字符串的长度是否在定义的范围内。 可以定义一个限制而不是另一个。 请注意，字符串的长度是 base64 编码数据实际表示的字节数。

-   **\* ArrayLabel** (可选) 。 如果指定此指令，则分析器筛选器会将值括在括号内，并在其前面加上指定的数组标签。

要分析的值必须符合为 FilterTypeName 指令指定的特定筛选器类型定义的语法 \* 。 如上所述，分析器筛选器将此值转换为一个或多个 XML 数据类型，如前文所述。 如果转换导致了多个 XML 元素，则每个元素都将使用 ElementTags 指令中指定的名称进行标记 \* 。

发出 XML 快照时，如果 XML 实体存在于字符串筛选器类型的值中，则分析器将自动用适当的 XML 实体来表示它们。 例如， ( # A0) 的 "&" 字符由快照中的 t& 表示。 在使用分析器筛选器定义的数据类型时，无需遵循 XML 语法规则。

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

此模板指定筛选器类型 "HEX \_ " 或 " \_ INT"。 根据为 FilterTypeName 提供的信息 \* ，筛选器会将此数据类型转换为内置 XSD 类型 int。若要确保生成的 XML 保持筛选器的意图，必须在 **\* ElementType** 指令中命名表示 XSD 数据类型 int 的模板。

在下面的示例中，XSD \_ INT 模板命名为。 此模板的定义如下。

```cpp
*Template:  XSD_INT
{
    *Type:  DATATYPE
    *DataType:   XML_TYPE
    *XMLDataType: "int"  
}
```

XSD \_ INT 模板定义本机 XSD 类型 INT，这可确保正确实现分析器筛选器的意图。

\*DataType：筛选器 \_ 类型模板不生成相应的架构。

请考虑以下 GDL 条目。

```cpp
*MaxCopies:   0x1ff
```

并考虑下面的模板 MAXCOPIES。

```cpp
*Template:  MAXCOPIES
{
    *Name:  "*MaxCopies"
    *Type:  ATTRIBUTE
    *ValueType:  INTEGER
}
```

如果前面的模板解释了前面的 GDL 项，则生成的 XML 输出将为。

```cpp
    <GDL_ATTRIBUTE Name="*MaxCopies"  xsi:type="GDLW_int" >511</GDL_ATTRIBUTE> 
```

请注意，分析器筛选器已将 GPD 定义的十六进制格式转换为适用于 XSD 数据类型 **xsd： int** 的十进制格式。另请注意，实际引用的类型是 GDLW int 类型的包装类型 \_ 。

 

 




