---
title: 将 AFM 文件转换为 NTF 文件
description: 将 AFM 文件转换为 NTF 文件
keywords:
- 微型驱动程序 WDK Pscript，转换 AFM 文件
- CONTOSO.NTF 文件
- contoso.ntf 文件
- afm 文件
- AFM 文件
- 将 AFM 文件转换为 CONTOSO.NTF 文件
- Adobe 字体指标 WDK Pscript
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8f51af6b6b81354fac19e5f1a3a9d5e9256648d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797513"
---
# <a name="converting-afm-files-to-ntf-files"></a>将 AFM 文件转换为 NTF 文件





对于 Windows 2000 和更高版本， (*AFM*) 文件必须转换为 contoso.ntf 文件。 使用 Windows 驱动程序开发工具包 (的 DDK) 提供了一个用于执行此转换的命令行工具，该工具名为 makentf.exe。

若要转换一个或多个文件的一个或多个文件，请使用以下命令语法：

**makentf** {**-win32** | **-win64**} * * * * * \[ **-v** \]  ****  \[ **o** \]  ****  <em>contoso.ntf \_</em>**contoso.ntf** *AFM \_* FileName

其中， *Contoso.ntf \_ FileName* 是要生成的 contoso.ntf 文件的名称，而 *AFM \_ 文件名* 是要转换的一个或多个 afm 文件的集合。

支持以下命令行选项：

<a href="" id="-win32"></a>**-win32**  
为 Win32 驱动程序创建 CONTOSO.NTF 文件。 如果指定此命令行选项，则不能指定 **-win64** 。

<a href="" id="-win64"></a>**-win64**  
为 Win64 驱动程序创建 CONTOSO.NTF 文件。 如果指定此命令行选项，则无法指定 **-win32** 。

<a href="" id="-v"></a>**-v**  
“详细”： 此选项将创建一个命令输出流，其中包含所生成的 CONTOSO.NTF 文件结构的文本显示。

<a href="" id="-o"></a>**-o**  
省略标准西方字形集。 默认情况下，在生成 contoso.ntf 文件时，Makentf.exe 包括标准西方标志符号集。 如果要创建多个 contoso.ntf 文件，只需在其中一个文件中包含西方标志符号集，前提是所有文件将一起使用。 例如，假设要创建一个 contoso.ntf 文件，其中包含罗马字字体指标和另一个包含日语字体度量值的文件。 您可以使用以下命令：

```cpp
makentf -win32 roman.ntf roman1.afm roman2.afm roman3.afm
makentf -win32 -o jpn.ntf jpn1.afm jpn2.afm jpn3.afm
```

如果将这些文件一起使用，则将始终从 contoso.ntf 获取西方标志符号集信息，因此不需要复制 jpn 中的信息，也不需要占用额外的空间。 另一方面，如果 jpn 将单独使用，则不能指定 **-o** 。

还支持第二个命令语法，如下所示：

**makentf** *filename*

其中 *filename* 是用于接收输出文本的文件的名称。 此语法会导致 Makentf.exe 创建一个文件，该文件包含 Makentf.exe 已知的每个代码页的 PostScript 标志符号名称和 Unicode 值的列表。

其他文件 PSFamily 与 WDK 一起提供，并且必须驻留在包含 Makentf.exe 的同一目录中。 这是一个文本文件，它为每个字体的显示和家族名称提供 Makentf.exe。

在转换标准的 afm 文件之前，必须添加一行，如下所示：

```cpp
Comment UniqueID IDnumber
```

其中， *IDnumber* 表示字体的唯一标识符，由字体供应商发出。

当处理东亚字体的 afm 文件时，Makentf.txt 需要一些附加的 .map 文件和 .ps 文件，这些文件必须与 **-o** 和 PSFamily 的目录驻留在同一目录中。 在 WDK (中提供的附加 .map 和 .ps 文件与 PSFamily) ，这是创建从 Unicode 代码到该字体的 CID 的映射表所必需的。 有关详细信息，请参阅 [将东亚 AFM 文件转换为 Contoso.ntf 文件](converting-east-asian-afm-files-to-ntf-files.md)。

将转换为 contoso.ntf 文件的一个文件将包含 **FontBBox2** 关键字。 此关键字的参数类似于 **FontBBox** 的参数 (参阅 adobe Systems，inc. ) 中的 *Adobe Font 指标文件格式规范*，但 **FontBBox2** 参数说明了在特定字符集中使用的标志符号的边界框 (如为90毫秒) ，而 **FontBBox** 参数说明了该文件中所述的所有字符的联合的边界框。 如果找不到 **FontBBox2** ，则将为 **FontBBox** 指定值。

 

 




