---
title: INF 文件常规指南
description: INF 文件常规指南
ms.assetid: a0394708-46ed-47f8-a629-0c7d3088df3b
keywords:
- INF 文件 WDK 设备安装，一般指导原则
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 788d55c9f1a0c810da0d0952cdf56d9f6fe40f51
ms.sourcegitcommit: a5cbd86f3019a54ba6425999b651d6ef8bd29937
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57693058"
---
# <a name="general-guidelines-for-inf-files"></a>INF 文件常规指南




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

## <a name="best-practices-for-naming-and-versioning-your-inf-file"></a>命名的最佳实践和版本控制您的 INF 文件

- 可使用 Inf 冲突的可能性减少来自其他供应商的方式，应命名为 INF 名称。  例如，INF 名称可以在其中，作为前缀或后缀，包括你的公司名称的缩写词。
- 如果您有两个不同变量的不同方面，如品牌字符串、 设置等的相同驱动程序包，两个驱动程序包，应具有唯一的名称。
- 每次更新 INF 或任何 INF 文件的引用，应更新的日期和 INF 中的版本。
 





