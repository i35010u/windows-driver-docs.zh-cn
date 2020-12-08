---
title: 定义自定义错误类型
description: 定义自定义错误类型
keywords:
- 自定义错误消息 WDK 内核
- 自定义错误类型 WDK 内核
- IO_ERR_XXX 值
- 模板 WDK 错误
- 标头 WDK 错误
- 文件 WDK 错误日志
- 文本文件 WDK 错误日志
- 编译错误消息文件
- Languagenames.xml 指令
- SeverityNames 指令
- FacilityNames 指令
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab7446553b8642480b8ac242954addcf5c27b822
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824031"
---
# <a name="defining-custom-error-types"></a>定义自定义错误类型





驱动程序可以指定其自己的错误类型和错误消息。 若要定义自定义错误消息，必须首先定义一个新的 IO \_ ERR \_ *XXX* 值，以指定为错误日志条目的 **ErrorCode** 成员。 事件查看器使用 IO \_ ERR \_ *XXX* 值查找驱动程序的错误消息。

若要支持驱动程序中的自定义错误消息，请执行以下步骤：

1.  创建一个消息文本文件，该文件指定自定义 IO \_ ERR \_ *XXX* 值和相应的错误消息。 有关详细信息，请参阅 [创建错误消息文本文件](#ddk-creating-the-error-message-text-file-kg)。

2.  将错误消息文本文件编译为资源，并将资源附加到驱动程序映像。 有关详细信息，请参阅 [编译错误消息文本文件](#ddk-compiling-the-error-message-text-file-kg)。

3.  注册包含错误消息的驱动程序映像。 有关详细信息，请参阅 [注册为错误消息源](registering-as-a-source-of-error-messages.md)。

### <a name="creating-the-error-message-text-file"></a><a href="" id="ddk-creating-the-error-message-text-file-kg"></a>创建错误消息文本文件

驱动程序自定义 IO \_ ERR \_ *XXX* 值和匹配错误消息模板的定义作为消息表资源附加到驱动程序映像。 可以在消息文本文件中描述驱动程序的消息 (文件扩展名为 mc) 。

消息文本文件由两部分组成：标头部分和消息部分。 标头部分允许为数值声明符号名称，而 message 节则指定 IO \_ ERR \_ *XXX* 值和匹配的错误消息模板。

有关消息文本文件的示例，请参阅 GitHub 上提供的 [串行驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=617962) 中的 Serlog.mc 文件。

### <a name="header-section"></a>标题部分

标头部分必须包含以下行：

```cpp
MessageIdTypedef=NTSTATUS
```

这可确保 \_ 消息编译器生成的 IO ERR \_ *XXX* 值的类型被声明为 NTSTATUS。

标头部分中显示的其他指令定义用于替换 message 节中的数值的符号值。

**SeverityNames** 和 **FacilityNames** 指令定义了 NTSTATUS 值的 "严重级别" 和 "工具" 字段的符号值。 指令的形式为 <em>关键字</em>**= (** *值* **)**，其中 *值* 由一个或多个窗体 *名称* 值的语句组成 **=** *value* **：** *标头 \_ 名称*，由空格分隔。 *Name* 参数是在消息文本文件中 *指定数值时* 使用的名称，而 *标头 \_ 名称* 是在消息编译器生成的 C 头文件中声明的此值的名称。 **：** *Header \_ name* 子句是可选的。

下面是严重性代码的符号名称标头声明的示例：

```cpp
SeverityNames = (
  Success       = 0x0:STATUS_SEVERITY_SUCCESS
  Informational = 0x1:STATUS_SEVERITY_INFORMATIONAL
  Warning       = 0x2:STATUS_SEVERITY_WARNING
  Error         = 0x3:STATUS_SEVERITY_ERROR
)
```

**Languagenames.xml** 指令定义 (LCID) 的区域设置 id 的符号值。 指令的格式为 **languagenames.xml = (** *值* **)**，其中的 *值* 由一个或多 *个格式 \_ 为* langfile 的语句 **=** *lcid* **:** *langfile*（由空格分隔）组成。 *Language \_ name* 参数是用于替代消息文本文件中的 *lcid* 的名称，而 *文件名* 指定唯一的文件名 (不包含扩展名) 。 当消息编译器从消息文本文件生成资源脚本时，它将此语言的所有字符串资源都存储在名为 *langfile* 的文件中。*bin*。

### <a name="message-section"></a>消息部分

每个消息定义都以自定义 IO ERR XXX 值的定义开始， \_ \_ *XXX* 驱动程序使用该值报告此特定类型的错误。 IO \_ ERR \_ *XXX* 值由一系列 *关键字*  =  *值* 对定义。 可能的关键字及其含义如下所示。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>关键字</th>
<th>“值”</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>MessageId</strong></p></td>
<td><p>新 IO_ERR_<em>XXX</em> 值的代码字段。</p></td>
</tr>
<tr class="even">
<td><p><strong>严重性</strong></p></td>
<td><p>新 IO_ERR_<em>XXX</em> 值的严重性字段。 指定的值必须是 <strong>SeverityNames</strong> 标头指令定义的符号名称之一。</p></td>
</tr>
<tr class="odd">
<td><p><strong>设施</strong></p></td>
<td><p>新 IO_ERR_<em>XXX</em> 值的设施字段。 指定的值必须是 <strong>FacilityNames</strong> 标头指令定义的符号名称之一。</p></td>
</tr>
<tr class="even">
<td><p><strong>SymbolicName</strong></p></td>
<td><p>新 IO_ERR_<em>XXX</em> 值的符号名称。 消息编译器将生成一个 C 头文件，其中包含名称的<strong> # 定义</strong>声明作为对应的 NTSTATUS 值。 驱动程序在指定错误类型时使用该名称。</p></td>
</tr>
</tbody>
</table>

 

第一个关键字必须始终为 **MessageId**。

消息定义的其余部分包含错误消息的一个或多个本地化版本。 每个版本的格式为：

```cpp
Language=language_name
localized_message
```

*Language \_ name* 值必须是 **languagenames.xml** 标头指令定义的符号名称之一，指定消息文本的语言。 本地化消息文本本身包含 Unicode 字符串。 格式为 "%*n*" 的任何嵌入式字符串都将被视为在记录错误时事件查看器将替换的模板。 "%1" 字符串替换为驱动程序的设备对象的名称，而 "%2" 通过 "%*n*" 替换为驱动程序提供的任何插入字符串。

消息定义在一行上单独由一个句点结束。

如果定义自定义错误消息，则除非需要，否则不应使用插入字符串。 不能对插入字符串进行本地化，因此应将其用于与语言无关的字符串，例如数字或文件名。 大多数驱动程序不使用插入字符串。

### <a name="compiling-the-error-message-text-file"></a><a href="" id="ddk-compiling-the-error-message-text-file-kg"></a>编译错误消息文本文件

使用消息编译器 ( # A0) 将消息文本文件编译到 (文件) 扩展名为 .rc 的资源脚本文件中。 窗体的命令

```cpp
mc filename.mc
```

导致消息编译器生成以下文件：

-   *filename*.h，其中包含 filename 中每个自定义 IO \_ ERR \_ *XXX* 值 *filename* 的声明的头文件。*mc*。

-   *filename*.rc，资源脚本。

-   消息文本文件中显示的每种语言都有一个文件。 其中每个文件都存储一种语言的所有错误消息字符串资源。 每种语言的文件都命名为 *langfile*。*bin*，其中 *langfile* 是在消息文本文件的 **languagenames.xml** 指令中为语言指定的值。

有关消息编译器的详细信息，请参阅 Microsoft Windows SDK。

资源编译器将资源脚本转换为可附加到驱动程序映像的资源文件。 如果使用生成实用程序来构建驱动程序，则可以通过将资源脚本的名称包含在驱动程序的源变量中，确保资源脚本转换为资源文件并附加到驱动程序映像。 有关资源编译器的详细信息，请参阅 Windows SDK 文档。 有关使用生成实用程序构建驱动程序的信息，请参阅 [构建驱动程序](../develop/building-a-driver.md)。


 

