---
title: 定义自定义错误类型
description: 定义自定义错误类型
ms.assetid: 1106b520-8737-421b-bee5-841220862b78
keywords:
- 自定义错误消息 WDK 内核
- 自定义错误类型 WDK 内核
- IO_ERR_XXX 值
- 模板 WDK 错误
- 标头 WDK 错误
- 文件 WDK 错误日志
- 文本文件 WDK 错误日志
- 编译错误消息文件
- LanguageNames 指令
- SeverityNames 指令
- FacilityNames 指令
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e1841930f086c7081e0422de724fce11150b08d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388222"
---
# <a name="defining-custom-error-types"></a>定义自定义错误类型





驱动程序可以指定自己的错误类型和错误消息。 若要定义自定义错误消息，必须首先定义新 IO\_ERR\_*XXX*值指定为**ErrorCode**错误日志条目的成员。 事件查看器使用 IO\_ERR\_*XXX*值来查找驱动程序的错误消息。

若要在您的驱动程序支持自定义错误消息，请执行以下步骤：

1.  创建指定的自定义 IO 消息文本文件\_ERR\_*XXX*值和相应的错误消息。 有关详细信息，请参阅[创建错误消息的文本文件](#ddk-creating-the-error-message-text-file-kg)。

2.  编译错误消息文本文件到资源，并将资源连接到驱动程序映像。 有关详细信息，请参阅[编译错误消息文本文件](#ddk-compiling-the-error-message-text-file-kg)。

3.  将驱动程序映像注册为包含错误消息。 有关详细信息，请参阅[注册为错误消息源](registering-as-a-source-of-error-messages.md)。

### <a href="" id="ddk-creating-the-error-message-text-file-kg"></a>创建错误消息的文本文件

定义的驱动程序的自定义 IO\_ERR\_*XXX*值和匹配的错误消息模板作为消息表资源附加到驱动程序映像。 您可以描述消息文本文件 （其文件扩展名为.mc） 中的驱动程序的消息。

消息文本文件包含两个部分： 标头部分和消息部分。 标头部分可以数字值的符号名称的声明，同时让消息部分指定的 IO\_ERR\_*XXX*值和匹配的错误消息模板。

消息文本文件的示例，请参阅中的 Serlog.mc 文件[串行驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=617962)GitHub 上提供。

### <a name="header-section"></a>标头部分

标头部分必须包含下面这行：

```cpp
MessageIdTypedef=NTSTATUS
```

这可以保证的 IO 类型\_ERR\_*XXX*消息编译器生成的值被声明为 NTSTATUS。

标头部分中显示的其他指令定义用来替代消息部分中的数字值的符号值。

**SeverityNames**并**FacilityNames**指令定义的严重性和设施的 NTSTATUS 值字段的符号值。 指令是窗体<em>关键字</em>**= (** *值* **)**，其中*值*由一个或窗体的多个语句*名称* **=** *值* **:** *标头\_名称*、 通过空格分隔。 *名称*参数是使用指定数字的名称*值*在消息文本文件中，而*标头\_名称*是此值的名称在消息编译器生成的 C 标头文件中声明。 **:** *标头\_名称*子句是可选的。

下面是严重性代码的符号名称的标头声明的示例：

```cpp
SeverityNames = (
  Success       = 0x0:STATUS_SEVERITY_SUCCESS
  Informational = 0x1:STATUS_SEVERITY_INFORMATIONAL
  Warning       = 0x2:STATUS_SEVERITY_WARNING
  Error         = 0x3:STATUS_SEVERITY_ERROR
)
```

**LanguageNames**指令定义的区域设置 Id (LCID) 的符号值。 指令是窗体**LanguageNames = (** *值* **)**，其中*值*包含的窗体的一个或多个语句*语言\_名称* **=** *lcid* **:** *langfile*，由空格分隔。 *语言\_名称*参数是的名称来代替使用*lcid*在消息文本文件中，而*filename*指定唯一的文件名 （不带扩展名）。 当消息编译器从消息文本文件生成资源脚本时，它将存储此语言的字符串资源的所有在名为的文件*langfile*。*bin*。

### <a name="message-section"></a>消息部分

每个消息的定义开头定义的自定义的 IO\_ERR\_*XXX*驱动程序使用来报告错误的此特定类型的值。 IO\_ERR\_*XXX*值由一系列定义*关键字* = *值*对。 可能的关键字和它们的含义如下所示。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>关键字</th>
<th>ReplTest1</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>MessageId</strong></p></td>
<td><p>代码字段的新 IO_ERR_<em>XXX</em>值。</p></td>
</tr>
<tr class="even">
<td><p><strong>Severity</strong></p></td>
<td><p>Severity 字段的新 IO_ERR_<em>XXX</em>值。 指定的值必须是由定义的符号名称之一<strong>SeverityNames</strong>标头指令。</p></td>
</tr>
<tr class="odd">
<td><p><strong>设施</strong></p></td>
<td><p>设施字段的新 IO_ERR_<em>XXX</em>值。 指定的值必须是由定义的符号名称之一<strong>FacilityNames</strong>标头指令。</p></td>
</tr>
<tr class="even">
<td><p><strong>SymbolicName</strong></p></td>
<td><p>符号名称，新 IO_ERR_<em>XXX</em>值。 消息编译器生成包含一个 C 标头文件<strong>#定义</strong>名称声明为相应的 NTSTATUS 值。 指定的错误类型时，驱动程序将使用该名称。</p></td>
</tr>
</tbody>
</table>

 

必须始终为第一个关键字**MessageId**。

消息定义的其余部分包含的错误消息的一个或多个本地化版本。 每个版本的形式：

```cpp
Language=language_name
localized_message
```

*语言\_名称*值，该值必须是一个符号名称由定义**LanguageNames**标头指令指定的消息文本的语言。 本地化的消息文本本身包含 Unicode 字符串。 任何嵌入的窗体的字符串"%*n*"将被视为事件查看器将替换记录错误时的模板。 "%1"字符串"%2"时，驱动程序的设备对象的名称替换为通过"%*n*"替换为驱动程序提供任何插入字符串。

行上唯一一个单个句点终止消息定义。

如果定义自定义错误消息，不应使用插入字符串除非有必要。 插入字符串不能进行本地化，因此，它们应使用的是独立于语言的如数字或文件的名称的字符串。 大多数驱动程序不使用插入字符串。

### <a href="" id="ddk-compiling-the-error-message-text-file-kg"></a>编译错误消息文本文件

使用消息编译器 (mc.exe) 要在消息文本文件编译到资源脚本文件 （它具有一个.rc 文件扩展名）。 格式的命令

```cpp
mc filename.mc
```

使消息编译器生成以下文件：

-   *文件名*.h、 头文件包含声明的每个自定义 IO\_ERR\_*XXX*中的值*filename*。*mc*。

-   *文件名*.rc、 资源脚本。

-   每种语言的消息文本中显示的的第一个文件。 每个文件，存储所有的错误消息字符串资源的一种语言。 每种语言的文件命名为*langfile*。*bin*，其中*langfile*是语言的消息文本文件中指定的值**LanguageNames**指令。

可以在 Microsoft Windows SDK 中找到有关消息编译器的详细信息。

资源编译器将资源脚本转换到的资源文件，您可以将附加到您的驱动程序的映像。 如果使用生成实用程序来构建您的驱动程序，可以确保资源脚本是转换到资源文件并附加到驱动程序映像，只需通过该驱动程序的源变量中包含的资源脚本名称。 资源编译器有关的详细信息，请参阅 Windows SDK 文档。 有关使用生成实用工具构建您的驱动程序的信息，请参阅[构建一个驱动程序](https://docs.microsoft.com/windows-hardware/drivers/develop/building-a-driver)。


 

 




