---
title: 一般性的指导原则的 INF 文件
description: 一般性的指导原则的 INF 文件
ms.assetid: a0394708-46ed-47f8-a629-0c7d3088df3b
keywords:
- INF 文件 WDK 设备安装，一般指导原则
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 415f8bf9c0e61553a36ddf2095893b84896fc9a5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548283"
---
# <a name="general-guidelines-for-inf-files"></a>一般性的指导原则的 INF 文件





INF 文件具有许多常见的部分，并遵循单一的语法规则集。 但是，它们也是为作为支持的 Microsoft Windows 设备的各种不同的。 当您编写的 INF 文件时，请参阅以下信息源：

-   本部分和[INF 文件的部分和指令](inf-file-sections-and-directives.md)参考资料。

-   你的设备类的文档。

    例如，如果你的设备是打印机，请参阅[安装和配置打印机驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff551648)。

-   WDK 的 INF 文件的工具。

    有关详细信息，请参阅[INF 文件的工具](https://msdn.microsoft.com/library/windows/hardware/ff552956)。 这些工具包括在\\WDK 的 Tools 子目录。

-   示例 INF 文件和类似的设备的 INF 文件。

    WDK 包括的示例驱动程序的 INF 文件。 浏览示例驱动程序，以查看是否有设备 INF 文件类似于你的设备。

您可以创建或使用在其中您可以控制的换行插入任何文本编辑器来修改 INF 文件。 如果你 INF 包含非 ASCII 字符，将文件另存 Unicode 文件。

INF 文件附带 Windows 7 和更早的操作系统必须具有的文件名称<em>xxxxxxxx</em>**.inf**，其中"*xxxxxxxx*"不超过 8 个字符。 从操作系统是单独发售的 INF 文件的名称不局限于八个字符。

从 Windows 8 开始，INF 文件的名称不受限制为八个字符，而不考虑如果或不提供与操作系统。

不要随意修改你的 INF 文件的时间戳作为版本控制机制。 版本控制的 INF 文件应基于中指定的日期和版本号[ **INF 版本部分**](inf-version-section.md)。

 

 





