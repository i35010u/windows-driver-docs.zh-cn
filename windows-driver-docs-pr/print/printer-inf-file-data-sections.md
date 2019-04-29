---
title: 打印机 INF 文件的 Data 节
description: 打印机 INF 文件的 Data 节
ms.assetid: d060716c-7c26-41a8-afbc-6fe83829d46a
keywords:
- INF 文件 WDK 打印，数据部分
- 数据部分 WDK 打印机
- 以前的名称的数据部分 WDK 打印机
- 部分 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94320614a29d8ee17c58969f89205e9454793123
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380163"
---
# <a name="printer-inf-file-data-sections"></a>打印机 INF 文件的 Data 节





默认 Windows 2000 及更高版本的打印机类安装程序中，Ntprint.dll，允许打印机 INF 文件包含的数据部分。 使用以下格式指定数据部分：

**DataSection**= *SectionName*

其中*SectionName*是 INF 文件部分名称。

用于数据部分指定的集[打印机 INF 文件条目](printer-inf-file-entries.md)共有多台打印机。 通过将分组常见列表中的项下的命名的节，然后引用与该部分**DataSection**语句中为每个打印机使用的条目，条目列表必须是包含一次 INF 文件中。

Microsoft 的打印机 INF 文件，Ntprint.inf，定义以下数据部分：

-   \[PSCRIPT\_DATA\]

    将分配到的值**DriverFile**， **ConfigFile**，并**HelpFile** Microsoft PostScript 打印机驱动程序的条目。

-   \[UNIDRV\_DATA\]

    将分配到的值**DriverFile**， **ConfigFile**，并**HelpFile** Microsoft 通用打印机驱动程序的条目。

-   \[UNIDRV\_BIDI\_DATA\]

    将分配到的值**DriverFile**， **ConfigFile**， **HelpFile**，以及**LanguageMonitor** Microsoft 通用的条目打印机驱动程序，用于双向打印机。

应该从供应商提供 INF 文件中引用这些数据部分。 有关示例，请参阅[安装 Unidrv 微型驱动程序](installing-a-unidrv-minidriver.md)并[安装 Pscript 微型驱动程序](installing-a-pscript-minidriver.md)。

**请注意**   IHV 打印机 INF 文件，或者**需要**条目或**Include**指 Ntprint.inf 的条目不能包含任何 INF 相同的数据部分名称在 Ntprint.inf 中存在的节名称。 命名供应商提供的打印机 INF 文件中的数据部分之前, 搜索 %windir%/inf/Ntprint.inf 以确保部分名称已不是 （的任何类型） 在 Ntprint.inf 中的部分名称。

 

### <a href="" id="ddk--previous-names-section-gg"></a>"先前名称"部分

Windows 2000 及更高版本的打印机类安装程序会识别一个名为"先前名称"的特殊数据部分。 这些部分之一被允许在每个 INF 文件。 节中的项标识为其打印机名称是不同 Windows 2000 和 Windows 95/98/me 比更高版本的驱动程序 通过指定此类名称的差异，对于 Windows 95/98/我的客户端连接到 Windows 2000 和更高版本的服务器支持点和打印。

在本部分中的每个条目的格式为：

"*Windows 2000 或更高版本的打印机名称*"="*Windows 95/98/我的打印机名称*"

以下是示例条目：

```cpp
[Previous Names]
"HP Color LaserJet" = "HP Color LaserJet (MS)"
"HP DeskJet 1200C" = "HP DeskJet 1200C (MS)"
"HP DeskJet 310" = "HP DeskJet 310 Printer"
```

 

 




