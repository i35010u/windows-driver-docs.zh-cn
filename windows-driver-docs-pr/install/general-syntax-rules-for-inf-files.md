---
title: INF 文件常规语法规则
description: INF 文件常规语法规则
ms.assetid: ba11a229-d0d3-4217-bcf8-9aada2f159aa
keywords:
- INF 文件 WDK 设备安装，常规语法规则
- INF 文件 WDK 设备安装，部分
- 部分 WDK INF 文件
- INF 文件 WDK 设备安装，指令
- 指令 WDK INF 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d8214ecb9d35997fc7da45cf0314ba9b2c03bd9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392518"
---
# <a name="general-syntax-rules-for-inf-files"></a>INF 文件常规语法规则





INF 文件是文本文件划分为命名的部分。 某些部分提供的系统定义的名称和某些部分具有由的 INF 文件编写器的名称。

每个部分包含特定于部分的条目，将解释这些[设备安装组件](https://msdn.microsoft.com/library/windows/hardware/ff541277)（类安装程序，共同安装程序安装程序 Api）。 某些条目开始使用预定义的关键字。 这些项称为*指令*。

某些 INF 文件条目基本上都是指针从一部分到另一个，针对特定用途。 例如， [ **INF AddReg 指令**](inf-addreg-directive.md)标识节，其中包含指示 Windows 修改注册表项。 这些条目有时包含 Windows 来解释在安装过程中的其他参数 （必需或可选）。

其他 INF 文件条目执行不指向其他部分中，但提供信息，Windows 使用在安装期间，例如文件名、 注册表值、 硬件配置信息标志，等等。 例如， [ **INF DriverVer 指令**](inf-driverver-directive.md)提供驱动程序版本信息。

当 Windows 开始安装时，它首先会查找[ **INF 版本部分**](inf-version-section.md)验证其有效性的 INF 文件并确定安装文件的位置。 随后，它通过查找开始安装[ **INF 制造商部分**](inf-manufacturer-section.md)。 本部分包含对指令[ **INF*模型*各节**](inf-models-section.md)，进而提供指令，从而导致各种[ **INF *DDInstall*各节**](inf-ddinstall-section.md)，根据所安装的设备的硬件 ID。

下面的语法规则控制 INF 文件，通过使用字符串标记和行格式、 继续符和注释的部分名称的格式的必需和可选的内容。

### <a href="" id="case-sensitivity"></a> 区分大小写

-   节名称、 条目和指令不区分大小写。 例如，**版本**，**版本**，并**版本**都是有效的部分名称规范 INF 文件中的。

### <a href="" id="required-and-optional-contents"></a> 必需和可选的内容

- 必需和可选部分、 项和任何特定的 INF 文件中的指令集取决于类型的设备/驱动程序或组件 （如应用程序或设备类安装程序 DLL） 安装。

- 部分、 特定于部分的条目，以及安装任何特定设备，其驱动程序所需的指令集还取决于在某种程度上相应类安装程序。 详细了解如何系统提供的类中的安装程序处理特定于设备的类型 INF 文件，请参阅 WDK 中的设备类型特定文档。

- 语法定义中可选条目由分隔*unbolded*方括号 (\[，\])。 但是，*粗体*方括号 (**\[**， **\]**) 是它们包含的项的必需的元素。 在下面的示例中，用方括号括起**版本**是必需的而用方括号括起**类**=*类名*指示此项是可选。

  <pre>
  <b>[</b>Version<b>]</b>

  Signature="signature-name"
  [Class=class-name]
  ...
  </pre>

### <a href="" id="section-names"></a> 节名称

- 可以按任意顺序指定部分。 大多数 INF 文件列表中特定的顺序，部分按照约定，但 Windows 找到部分通过名称而不是 INF 文件中的位置。

- INF 文件中的每个部分开头的节的名称用方括号括起来 (**\[ \]**)。 节名称可以是系统定义或 INF 编写器定义。

  例如， **\[制造商\]** 指定起始位置的系统命名**制造商**部分中，而<strong>\[</strong>Std.Mfg<strong>\]</strong>表示特定 INF 编写器定义*模型*节名称。

  节名称具有最大长度为 255 个字符，在 Windows 2000 和更高版本的 Windows。

  每个部分结束时开始的新**\[**<em>节名称</em>**\]** 或文件尾标记处。

- 如果 INF 文件中的多个部分具有相同的名称，系统将合并其条目和指令到单个部分。

- 除非为括在双引号字符 (**"**)，INF 编写器定义的部分名称必须是唯一-到--INF 不带引号的显式可见的字符，不包括与特定于 INF 的某些字符字符串含义。 具体而言，不带引号的部分名称引用的部分条目或指令不能有前导或尾部空格、 换行符、 回车符或任何不可见控件字符，且它不应包含选项卡。 此外，它不能包含任一大括号 (**\[ \]**) 字符，单个 %(**%**) 字符，以分号 (**;**)或任何内部双引号括起来 (**"**) 字符，而且不能有一个反斜杠 (**\\**) 作为其最后一个字符。

  例如，Std.Mfg 和 Std_Mfg 是唯一且有效的部分名称时引用的 INF 文件条目或指令，但 Std;（使用其内部的分号） 的制造业无效，除非它包含由双引号引起来 (**"**)。

  INF 编写器定义的部分名称指定为 **"**<em>带引号的字符串</em>**"** 重写大部分已根据几个字符中前面所述的限制引用的节名称。 此类分隔的部分名称可以包含除右括号的几乎任何显式或隐式可见字符 (**\]**)，只要 INF 文件中的相应部分匹配这 **"**<em>带引号的字符串</em>**"** 完全。

  例如， **"**;标准制造业 **"** INF 文件中的相应部分声明与相对于其空间和分号字符作为两个双引号内的名称完全匹配时有效的部分名称引用**\[**;;标准制造业**\]**。

### <a href="" id="using-string-tokens"></a> 使用字符串令牌

- 可以表示多个值中的 INF 文件，其中包括 INF 编写器定义的节名称，如字符串标记的窗体**%** <em>strkey</em> **%**. 在 INF**字符串**INF 文件，每个字符串密钥部分必须包含一系列显式可见的字符的字符串值与相关联。 如有必要，安装程序代码将 Unicode 转换为字符串值。

  有关如何定义详细信息**%** <em>strkey</em> **%** 令牌及其各自的值，请参阅说明[ **INF 字符串部分**](inf-strings-section.md)。

### <a href="" id="line-format--continuation--and-comments"></a> 行的格式、 继续符和注释

- 每个条目和一个部分中的指令返回或换行字符结尾。 因此，使用创建的 INF 文件的文本编辑器必须插入一些任意的编辑器确定的字符数后返回或换行字符。

- 反斜杠字符 (**\\**) 可以用作项或指令中显式行 continuator。 但是，路径规范中还使用反斜杠字符。 若要确保未错误将出现在路径规范的反斜杠字符解释为行 continuator，请使用以下策略：

  -   对于一个指令跨越两行，其中之一是包含一个反斜杠的项，使用引号来分隔包含反斜杠的项。

      ```cpp
      CopyFiles = "SomeDirectory\"\
      ,SomeFile
      ```

  -   避免在以下示例所示的方式中使用反斜杠字符。 Windows 将忽略第一个反斜杠，并且将解释为行 continuator 另一个反斜杠。

      ```cpp
      CopyFiles = SomeDirectory\\
      ,SomeFile
      ```

  -   下面的语法有效，等效于`CopyFiles = "SomeDirectory\",SomeFile ; comment`。

      ```cpp
      CopyFiles = "SomeDirectory\"\ ; comment 
      ,SomeFile
      ```
      由于文本后忽略分号，`CopyFiles = "SomeDirectory\" ; comment ,SomeFile`不起作用。

- 以分号开头的注释 (**;**) 字符。 当分析和解释的 INF 文件，系统将假定以下已安装过程无关：
  - 除非分号将显示在分号后在同一行上的任何字符 **"**<em>带引号的字符串</em>**"** 或者**%**<em>strkey</em> **%** 令牌
  - 不包含除换行符或返回字符外的任何内容的任何空的行

- 用逗号分隔每节条目和指令中提供的值。

  INF 文件条目或指令可以省略可选值，一个列表中间值但逗号必须保留。 INF 文件可以省略尾随逗号。

  例如，考虑的语法**SourceDisksFiles**部分条目：

  <em>filename</em>**=**<em>diskid</em>\[**,**\[*subdir*\]\[**,**<em>size</em>\]\]

  省略的条目*subdir*但提供的值*大小*值必须指定这两个值的逗号分隔符，如下面的示例中所示：

  <em>filename</em>**=**<em>diskid</em>**,,**<em>size</em>

  省略了两个可选值的 INF 文件中的项可以具有以下格式：

  <em>filename</em>**=**<em>diskid</em>
- 若要包括一个百分号 （%）节条目和指令中提供的值中的字符，用另一个百分比字符转义百分比。

  例如，请考虑在此语句 *[添加的注册表-部分]* 部分：

  *HKR,,EventMessageFile,0x00020000,"%%SystemRoot%%\System32\IoLogMsg.dll"*

  注册表值将设置以下值：

  *%SystemRoot%\System32\IoLogMsg.dll*
- 若要在节条目和指令中提供的值中包含双引号 （"） 字符，转义具有另一个双引号字符的双引号字符。  请注意，该字符串必须位于 **"**<em>带引号的字符串</em>**"**。  

  例如，请考虑在此语句 *[添加的注册表-部分]* 部分：

  *HKR、 示例、"显示""示例""字符串"*

  注册表值将设置以下值：

  *显示"示例"字符串*

### <a href="" id="inf-size-limits"></a> INF 大小限制

-   以字符为单位的 INF 文件字段，字符串替换并包括终止 NULL 字符之前的最大长度为 4096。

-   字符串替换后以字符为单位的 INF 文件字符串的最大长度为 4096，其中包括终止 NULL 字符。

-   但是，请注意该 and 插即用 (PnP) 可能会施加更为严格的限制的某些 INF 文件字段，它会识别或使用，例如设备描述、 驱动程序提供程序和设备制造商。









