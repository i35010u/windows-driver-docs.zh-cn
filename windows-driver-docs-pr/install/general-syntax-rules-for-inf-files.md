---
title: INF 文件常规语法规则
description: INF 文件常规语法规则
ms.assetid: ba11a229-d0d3-4217-bcf8-9aada2f159aa
keywords:
- INF 文件 WDK 设备安装，一般语法规则
- INF 文件 WDK 设备安装，部分
- 部分 WDK INF 文件
- INF 文件 WDK 设备安装，指令
- 指令 WDK INF 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4103e1653d60da15aeb1f613da95e8a5b5a40a4e
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095719"
---
# <a name="general-syntax-rules-for-inf-files"></a>INF 文件常规语法规则





INF 文件是组织到命名部分的文本文件。 有些部分具有系统定义的名称，某些节的名称由 INF 文件的编写器决定。

每节包含特定于部分的条目，这些条目由 [设备安装组件](/previous-versions/ff541277(v=vs.85)) (类安装程序、共同安装程序、setupapi.log) 解释。 某些条目以预定义关键字开头。 这些项称为 " *指令*"。

出于特定目的，某些 INF 文件条目基本上是从一个部分指向另一个部分的指针。 例如， [**INF AddReg 指令**](inf-addreg-directive.md) 标识一个包含指示 Windows 修改注册表的项的部分。 这些项有时包括 (必需的参数或可选的参数) Windows 要在安装过程中进行解释。

其他 INF 文件条目不指向其他部分，而是提供 Windows 在安装过程中使用的信息，例如文件名、注册表值、硬件配置信息、标志等。 例如， [**INF DriverVer 指令**](inf-driverver-directive.md) 提供驱动程序版本信息。

当 Windows 开始安装时，它首先查找 " [**Inf 版本" 部分**](inf-version-section.md) 以验证 inf 文件的有效性，并确定安装文件的位置。 然后，它会通过查找 [**INF 制造商部分**](inf-manufacturer-section.md)来启动安装。 本部分包含对 [**Inf *模型* 部分**](inf-models-section.md)的指令，这反过来提供了根据所安装设备的硬件 ID 提供的各种 [**inf *DDInstall* 部分**](inf-ddinstall-section.md)的指令。

以下语法规则通过使用字符串标记、行格式、继续符和注释来控制 INF 文件的必需内容和可选内容、节名称的格式。

### <a name="case-sensitivity"></a><a href="" id="case-sensitivity"></a> 区分大小写

-   节名称、项和指令不区分大小写。 例如， **版本**、 **版本**和 **版本** 在 INF 文件中的名称规范相同。

### <a name="required-and-optional-contents"></a><a href="" id="required-and-optional-contents"></a> 必需内容和可选内容

- 任何特定 INF 文件中的必需和可选部分、条目和指令集取决于设备/驱动程序或组件的类型 (例如，要安装的应用程序或设备类安装程序 DLL) 。

- 安装任何特定设备及其驱动程序所需的一组部分、特定于节的条目和指令也依赖于相应的类安装程序。 有关系统提供的类安装程序如何处理特定于设备类型的 INF 文件的详细信息，请参阅 WDK 中设备类型的特定文档。

- 在语法定义中，可选项由 *unbolded* 方括号分隔 (\[ ， \]) 。 另一方面 *， (* **\[** ， **\]**) 是包含它们的项的必需元素。 在下面的示例中，需要在**版本**两侧加上括号，而**类** = *类名称*两边的括号表示此项是可选的。

  <pre>
  <b>[</b>Version<b>]</b>

  Signature="signature-name"
  [Class=class-name]
  ...
  </pre>

### <a name="section-names"></a><a href="" id="section-names"></a> 节名称

- 可以按任意顺序指定节。 大多数 INF 文件按特定顺序（按照约定）列出部分，但 Windows 会按名称查找分区，而不是通过 INF 文件中的位置查找。

- INF 文件中的每个部分均以方括号括起来的节名称** \[ \] **开头 () 。 节名称可以是系统定义的，也可以是由 INF 编写的。

  例如， ** \[ 制造商 \] **指定了 "系统指定的**制造商**" 部分的开头，而 " <strong>\[</strong> Std" <strong>\]</strong> 表示特定的 "INF-编写器定义的*模型*" 部分名称。

  在 Windows 2000 和更高版本的 Windows 上，节名的最大长度为255个字符。

  每一节都在新的 **\[** <em>节名</em> **\]** 或文件尾标记的开头处结束。

- 如果 INF 文件中有多个节具有相同的名称，则系统会将其条目和指令合并为一个部分。

- 除非它括在双引号中 (**"**) ，否则 inf 写入方定义的部分名称必须是显式可见字符的唯一的、不带引号的字符串，其中不包括特定于 inf 的含义的特定字符。 特别是，节条目或指令引用的未加引号的节名称不能包含前导空格或尾随空格、换行符、回车符或任何不可见的控制字符，也不应包含制表符。 此外，它不能包含任何一个方括号 (** \[ \] **) 字符、单个百分号 (**%**) 字符、分号 (、) 或 **;** 任何内部双引号 (**"**) 个字符，且不能将反斜杠 (**\\**) 为最后一个字符。

  例如，在由 INF 文件条目或指令引用时，Std 和 Std_Mfg 是唯一且有效的节名称，但 Std 为;使用内部分号) 制造 (无效，除非它由双引号括起来 (**"**) 。

  将由 INF 编写器定义的节名称指定为 **"**<em>带引号的字符串</em>**"** 会覆盖以前在引用的节名称中的字符上描述的大多数限制。 此类分隔部分名称可以包含几乎所有显式或隐式可见的字符， **\]** 只要 INF 文件中的相应部分与此 **"**<em>带引号的字符串</em>**"** 匹配，就 () 。

  例如， **"**;;如果 INF 文件中的相应部分声明与双引号内的名称完全匹配，并且其空格和分号字符与相同，则 Std 制造 **"** 是有效的节名称引用 **\[** ;标准制造 **\]** 。

### <a name="using-string-tokens"></a><a href="" id="using-string-tokens"></a> 使用字符串标记

- INF 文件中的许多值（包括 INF 写入方定义的部分名称）可表示为 strkey 形式的字符串密钥标记 **%** <em>strkey</em> **%** 。 在 INF 文件的 "INF **字符串** " 部分中，每个字符串键必须与一个字符串值相关联，该字符串值由一个显式可见字符序列组成。 如有必要，安装代码会将字符串值转换为 Unicode。

  有关如何定义 **%** <em>strkey</em> **%** 令牌及其各自值的详细信息，请参阅[**INF 字符串部分**](inf-strings-section.md)的说明。

### <a name="line-format-continuation-and-comments"></a><a href="" id="line-format--continuation--and-comments"></a> 线条格式、继续符和注释

- 节中的每个条目和指令都以返回或换行字符结尾。 因此，用于创建 INF 文件的文本编辑器不得在任何由编辑器确定的字符后插入返回或换行字符。

- 反斜杠字符 (**\\**) 可用作输入或指令中的 continuator。 但在路径规范中也使用了反斜杠字符。 若要确保路径规范中出现的反斜杠字符未被错误解释为行 continuator，请使用以下策略：

  -   对于跨两行的指令，其中一个是包含反斜杠的条目，请使用引号分隔包含反斜杠的条目。

      ```cpp
      CopyFiles = "SomeDirectory\"\
      ,SomeFile
      ```

  -   避免按以下示例中所示的方式使用反斜杠字符。 Windows 将忽略第一个反斜杠，并将第二个反斜杠解释为行 continuator。

      ```cpp
      CopyFiles = SomeDirectory\\
      ,SomeFile
      ```

  -   下面的语法有效并且等效于 `CopyFiles = "SomeDirectory\",SomeFile ; comment` 。

      ```cpp
      CopyFiles = "SomeDirectory\"\ ; comment 
      ,SomeFile
      ```
      由于忽略分号后的文本，因此 `CopyFiles = "SomeDirectory\" ; comment ,SomeFile` 不起作用。

- 注释以分号开始 (**;**) 字符。 在分析和解释 INF 文件时，系统假定以下内容没有与安装过程相关的关系：
  - 在同一行的分号后面的任何字符，除非分号出现在 **"**<em>带引号的字符串</em>**"** 或 **%** <em>strkey</em> **%** 标记中
  - 除换行符或回车符之外的任何空行

- 逗号分隔节条目和指令中提供的值。

  INF 文件条目或指令可以省略值列表中间的可选值，但必须保留逗号。 INF 文件可以省略尾随逗号。

  例如，请考虑 **SourceDisksFiles** 节项的语法：

  <em>filename</em> **=**<em>diskid</em> \[**,**\[*subdir* \] subdir \[**、**<em>大小</em>\]\]

  省略 *subdir* 值但提供 *大小* 值的项必须为这两个值指定逗号分隔符，如以下示例中所示：

  <em>filename</em> **=**<em>diskid</em>**、，**<em>size</em>

  INF 文件中省略两个可选值的条目可以采用以下格式：

  <em>filename</em> **=**<em>diskid</em>
- 若要在节条目和指令中提供的值中包含百分比 (% ) 字符，请使用另一个百分号字符对百分号字符进行转义。

  例如，请考虑 *[add-registry 节]* 部分中的以下语句：

  *HKR、、EventMessageFile、0x00020000、"%% SystemRoot%% \System32\IoLogMsg.dll"*

  注册表值将设置为以下值：

  *% SystemRoot% \System32\IoLogMsg.dll*
- 若要在部分条目和指令中提供的值中包含双引号 ( ") 字符，请使用另一个双引号字符来转义双引号字符。  请注意，该字符串必须位于 **"**<em>带引号的字符串</em>**"** 中。  

  例如，请考虑 *[add-registry 节]* 部分中的以下语句：

  *HKR，，Example，，"显示一个" 示例 "" string "*

  注册表值将设置为以下值：

  *显示 "示例" 字符串*

### <a name="inf-size-limits"></a><a href="" id="inf-size-limits"></a> INF 大小限制

-   在字符串替换和包含终止 NULL 字符之前，"INF 文件" 字段的最大长度（以字符为字符）为4096。

-   字符串替换后，INF 文件字符串的最大长度（以字符为4096）包含一个终止 NULL 字符。

-   但请注意，即插即用 (PnP) 可能会对它识别或使用的某些 INF 文件字段施加更严格的限制，例如设备说明、驱动程序提供程序和设备制造商。