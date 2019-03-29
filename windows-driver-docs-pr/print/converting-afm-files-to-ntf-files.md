---
title: 将 AFM 文件转换为 NTF 文件
description: 将 AFM 文件转换为 NTF 文件
ms.assetid: 5c6c8843-c1b8-4cbd-81db-8a54cc377020
keywords:
- 微型驱动程序 WDK Pscript，转换 AFM 文件
- NTF 文件
- .ntf 文件
- .afm 文件
- AFM 文件
- 将 AFM 文件转换为 NTF 文件
- Adobe 字体指标 WDK Pscript
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85f56bc39fdb6c712edb85abd0a97a54c0dbe48d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566010"
---
# <a name="converting-afm-files-to-ntf-files"></a>将 AFM 文件转换为 NTF 文件





为 Windows 2000 和更高版本、 Adobe 字体规格 (*AFM*) 文件必须转换为.ntf 文件。 用于执行此转换中，名为 makentf.exe，命令行工具提供与 Windows 驱动程序开发工具包 (DDK)。

若要将一个或多个.afm 文件的转换，使用以下命令语法：

**makentf** {**-win32**|**-win64**} **** \[**-v**\] **** \[**-o**\] **** <em>NTF\_FileName</em>**.ntf** *AFM\_FileNames*

其中*NTF\_文件名*是要生成，.ntf 文件的名称和*AFM\_文件名*是一组要转换的一个或多个 AFM 文件。

支持以下命令行选项：

<a href="" id="-win32"></a>**-win32**  
创建 Win32 驱动程序的 NTF 文件。 如果指定此命令行选项，则 **-win64**不能指定。

<a href="" id="-win64"></a>**-win64**  
创建用于 Win64 驱动程序的 NTF 文件。 如果指定此命令行选项，则 **-win32**不能指定。

<a href="" id="-v"></a>**-v**  
详细。 此选项创建包含 NTF 文件结构正在生成的文本显示的命令输出流。

<a href="" id="-o"></a>**-o**  
忽略标准西方标志符号集。 默认情况下，Makentf.exe 生成.ntf 文件时包括标准西方标志符号集。 如果要创建多个.ntf 文件，则只需包括西欧的标志符号设置中的文件之一，只要将一起使用的所有文件。 例如，假设要创建一个.ntf 文件，其中包含 Roman 字体规格和另一个同时包含日语字体规格。 你可以使用以下命令：

```cpp
makentf -win32 roman.ntf roman1.afm roman2.afm roman3.afm
makentf -win32 -o jpn.ntf jpn1.afm jpn2.afm jpn3.afm
```

如果同时使用了这些文件，西方标志符号集信息将始终从获取 roman.ntf，以便复制 jpn.ntf 中的信息，则不需要并会消耗额外空间。 另一方面，如果将单独，使用 jpn.ntf **-o**不能指定。

第二个命令语法也支持，按如下所示：

**makentf** *filename*

其中*文件名*是要接收输出的文本的文件的名称。 此语法会导致 Makentf.exe 若要创建包含 PostScript 标志符号名称和已知的 Makentf.exe 每个代码页的 Unicode 值的列表的文件。

一个额外的文件，PSFamily.dat，WDK 提供，并且必须位于包含 Makentf.exe 的相同目录。 这是向 Makentf.exe 提供的显示和每个字体系列名称的文本文件。

转换标准.afm 文件之前，必须添加类似于以下内容的行：

```cpp
Comment UniqueID IDnumber
```

其中*id 编号*表示字体的唯一标识符，颁发的字体供应商。

Makentf.txt 时它正在处理东亚字体.afm 文件时，需要进行一些其他.map 和.ps 文件，必须所在的同一目录中驻留 **-o**和 PSFamily.dat。 其他.map 和.ps 文件中 （以及 PSFamily.dat) WDK 提供了，是必需的映射表从创建 Unicode 代码至 CID 的字体。 有关详细信息，请参阅[转换东亚 AFM 文件转换为 NTF 文件](converting-east-asian-afm-files-to-ntf-files.md)。

将转换为.ntf 文件.afm 文件可以包含**FontBBox2**关键字。 此关键字的参数是类似于**FontBBox** (请参阅*Adobe 字体指标文件格式规范*，从 Adobe Systems，Inc.)，只不过**FontBBox2**参数描述的特定字符 （如 90 毫秒），设置中使用的标志符号的边界框时**FontBBox**参数描述.afm 文件中所述的所有字符的边界框的联合。 如果**FontBBox2**未找到，为指定的值**FontBBox**用于边界框。

 

 




