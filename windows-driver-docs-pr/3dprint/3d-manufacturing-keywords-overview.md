---
title: 3D 制造关键字概述
description: 打印架构3D 制造关键字可识别设备功能的可能设置或设备配置的所选设置。
ms.assetid: D78EB9E6-584A-419C-B320-8962CDCC966E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8ba8df870c36290f2aa8db00c3afe869c746cbb
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652789"
---
# <a name="3d-manufacturing-keywords-overview"></a>3D 制造关键字概述


打印架构3D 制造关键字可识别3D 制造设备功能的可能设置或特定设备配置的所选设置。 这些关键字分别以定义完善的方式描述了特定概念，以最大程度地说明用于3D 制造的打印架构文档的创建者和使用者之间的设置通信。

制造者和使用者应该使用打印架构3D 制造关键字，以便为私有关键字扩展中的类似功能定义关键字。 关键字通过**name**属性标识单个打印架构框架元素。 为特定关键字指定的名称应具有关键字表示的设置或特征。

出现在 PrintCapabilities 或 PrintTicket 文档中的关键字实例应符合本文1.6 部分中定义的作用域前缀规则。 有关范围前缀的详细信息，请参阅第5.4 节中的 "范围前缀"。

## <a name="11-xml-namespaces"></a>1.1. XML 命名空间


用于3D 制造的打印架构关键字的命名空间 URI 为：

```xml
https://schemas.microsoft.com/3dmanufacturing/2013/01/pskeywords3d
```

在此规范中，命名空间前缀**psk3d：** 用于表示从3d 制造命名空间的打印架构关键字中提取的元素、属性和属性值。 发生器必须使用与相关打印架构命名空间的命名空间声明关联的命名空间前缀来生成每个带前缀的元素、属性或属性值。 使用者必须针对命名空间声明解析命名空间前缀，以确保限定名称是从正确的命名空间中提取的。 使用者不得依赖于命名空间前缀**psk3d：** 正确地声明并与用于3d 制造命名空间的打印架构关键字关联。 单个发生器可以为三维制造命名空间前缀使用不同的打印架构关键字，或将此命名空间声明为默认命名空间，并省略从此命名空间绘制的元素、属性和属性值的命名空间前缀。 但是，不建议将此关键字命名空间分配给默认命名空间。

在此规范中，命名空间前缀**vnd.apple.mpegurl：** 仅用于表示从供应商定义的命名空间提取的私有关键字扩展属性值。 供应商应为其定义的任何命名空间定义其自己的唯一命名空间前缀。 供应商不应为其命名空间定义**vnd.apple.mpegurl：** 命名空间前缀。 制造者不应生成使用**vnd.apple.mpegurl：** 命名空间的打印架构文档。

此外，在此规范中，命名空间前缀 xsd：用于表示从 XML 架构命名空间提取的元素和属性，命名空间前缀**xsi：** 用于表示从 Xml 架构实例命名空间中提取的元素和属性。 XML 内容不能包含从 "xml" 或 "xsi" 命名空间中提取的元素或属性，除非这些元素或此规范中的其他要求或打印架构规范明确允许这些元素或属性。

若要在打印架构框架的上下文中使用，请参阅第1.2 节 "打印架构中的 XML 使用情况"。

## <a name="12-3d-manufacturing-keywords-versioning"></a>1.2. 3D 制造关键字版本控制


此规范可能会以新关键字定期更新。 为了确保向前和向后兼容性，将为每组新的关键字提供一个唯一的命名空间。 一旦为生产用途释放了关键字集，就不会修改或扩展在特定命名空间中定义的关键字。 有关详细信息，请参阅1.3.2 中的 "关键字版本控制"。

## <a name="13-common-keyword-terminology"></a>1.3. 常见关键字术语


本节中的术语提供了一个基本框架和词汇，用于描述此规范的其余部分中的特定3D 制造关键字。

### <a name="131-model"></a>1.3.1. 型号

此规范中的*模型*是指通过3d 制造流程创建的对象，作为单个作业。 它可能包括单个对象、多个同源对象、多个异类对象、完全包含在另一个对象中的对象或互锁和不可分割*程序集中*的多个对象。

### <a name="132-coordinate-space"></a>1.3.2. 坐标空间

3D 制造打印架构关键字基于右旋坐标空间，模型坐标出现在正值 XYZ space 中。 制造者和使用者必须定义坐标空间的源并将其映射到打印输出字段的左下角，其中 x 轴增加到输出字段的右侧，y 轴增加到输出字段的背面，z 轴增加到输出字段的顶部。

制造者和使用者必须将坐标空间的单位分辨率用作1微米。 在对3D 制造关键字应用打印架构之前，必须将模型转换为此坐标空间。

![坐标空间](images/coordinate-space.png)

### <a name="133-relative-directions-and-measurement"></a>1.3.3. 相对方向和测量

此规范中的相对方向定义如下。 "*顶部*" 一词是指坐标空间中具有最大可打印 Z 值的 XY 平面。 "*下*" 一词是指坐标空间的可打印的最小 XY 平面，定义为 Z 值为0的 XY 平面。 这通常与打印平台表面重合。 术语 "*左*" 指的是坐标空间的最小可打印 YZ 平面，定义为 X 值为0的 YZ 平面。 术语 "*右*" 指的是坐标空间的 YZ 平面，最大可打印 X 值。 术语 "*前*" 是指坐标空间的最小可打印 XZ 平面，定义为 Y 值为0的 XZ 平面。 术语 "*后退*" 指坐标空间的 XZ 平面，其最大可打印 Y 值。

这些字词还适用于模型，在这种情况下，它们是在转换为在此规范中定义的坐标空间时相对于模型的边界框定义的。

制造者和使用者必须相对于此规范中定义的坐标空间来解释相对坐标。

## <a name="14-interpreting-keyword-descriptions"></a>1.4. 解读关键字说明


使用几个标准表中的一种来指定打印架构3D 制造关键字。 其中每个表的内容和要求的格式与打印架构规范第5.2 节中的格式相同。

## <a name="15-keyword-usage-in-print-schema-documents"></a>1.5. 打印架构文档中的关键字用法


打印架构3D 制造关键字不得用于此规范未显式描述的任何上下文中。

**Name**属性值包含 private 关键字 extension 的元素可以是 Print Schema Framework 允许的任何元素的子元素。

任何打印架构3D 制造关键字可能会显示为用 private 关键字扩展标识的元素的值的子元素的字符数据内容，前提是该字符数据引用了由打印架构3D 制造标识的原始元素在同一打印架构文档中的其他位置正确使用的关键字。

## <a name="16-scoping-prefixes"></a>1.6. 范围前缀


范围前缀是追加到关键字开头的文本标签，用于描述关键字的预期范围。 使用范围前缀，可以严格地将特定易懂的上下文 ascribing 为关键字。 3D 制造关键字应具有 "Job3D" 作用域前缀。 文档和页范围前缀不得用于3D 制造打印架构文档中。 有关详细信息，请参阅第5.4 节 "打印架构规范的" 范围前缀 "。

## <a name="17-resource-identifiers"></a>1.7. 资源标识符


资源标识符可用于打印架构3D 制造关键字，但必须遵循打印架构规范的第5.5 节 "资源标识符" 中的要求。

## <a name="18-parameter-types"></a>1.8。 参数类型


打印架构3D 制造关键字集的参数遵循与打印架构关键字集相同的参数要求。 请参阅第5.6 节中的 "参数类型"。

### <a name="181-materialmapparamtype"></a>1.8.1. MaterialMapParamType

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>“儿童”</th>
<th>xsi:type</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>属性 psf： DataType</td>
<td>xsd： QName</td>
<td>参数的类型为 materialMap，必须为 psk3d： MaterialMap。</td>
</tr>
<tr class="even">
<td>属性 psf： MaxLength</td>
<td>xsd:integer</td>
<td><p>指定可将此参数初始化为的字符串的最大长度。</p>
<p>值不应大于特定关键字的预期值。 打印架构定义的参数不得指定超过65535个字符的值。 该值必须是正整数或0。 该值必须大于或等于 psf： MinLength 的值。</p></td>
</tr>
<tr class="odd">
<td>属性 psf： MinLength</td>
<td>xsd:integer</td>
<td><p>指定可将此参数初始化为的字符串的最小长度。</p>
<p>该值必须是正整数或0。</p></td>
</tr>
<tr class="even">
<td>属性 psf：必需</td>
<td>xsd： QName</td>
<td>指定何时必须初始化参数。 有关此属性的说明和要求，请参阅§2.1.3.1.1，"参数 psf：必需属性"。</td>
</tr>
<tr class="odd">
<td>属性 psf： Unittype.pixel 度量</td>
<td>xsd:string</td>
<td>该值必须为 MaterialMapUnitType。</td>
</tr>
<tr class="even">
<td>属性 psk3d： Job3DMaterialSelected</td>
<td>xsd： QName</td>
<td>此值表示此参数对应的 Job3DMaterial。</td>
</tr>
</tbody>
</table>

 

## <a name="19-common-properties"></a>1.9。 通用属性


此规范使用与打印架构关键字相同的公共属性，这些关键字在第5.7 节 "通用属性" 中定义。

指定 xsd： decimal 类型的属性值必须可表示为 IEEE 754 单精度浮点值。

## <a name="110-parameter-unit-types"></a>1.10。 参数单位类型


除了在第2.1.3.1.2 中指定的参数单位类型外，还可以通过此规范添加以下单元类型： "参数 psf： Unittype.pixel 度量属性"。

| 单位类型   | xsi:type    | 描述                                                                                                                                                  |
|-------------|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 数量    | xsd:integer | 参数值的内容表示计数或其他数量。                                                                             |
| 温度 | xsd:decimal | 参数值的内容表示温度，以摄氏温度表示。 此参数必须始终舍入到最接近的百度。 |
| materialMap | xsd:string  | 参数值的内容必须表示为以分号分隔的 materialids 列表。                                                  |

 

 

 




