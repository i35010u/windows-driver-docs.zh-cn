---
title: 错误的信息检索
description: 错误的信息检索
ms.assetid: 4af06727-9660-4bbc-8c9e-a50c8f2d566d
keywords:
- Windows 硬件错误体系结构 WDK、 错误的信息检索
- WHEA WDK、 错误的信息检索
- 硬件错误 WDK WHEA，错误的信息检索
- 错误 WDK WHEA，错误的信息检索
- 特定于平台的硬件错误驱动程序插件 WDK WHEA，错误的信息检索
- PSHED 插件 WDK WHEA 错误信息检索
- 错误的信息检索 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 143d8296c23015bbc52052dcdf88c2d124dd1a06
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524768"
---
# <a name="error-information-retrieval"></a>错误的信息检索


在硬件错误条件的处理期间 PSHED 调用在错误处理过程中的三个单独的点。

-   低级别的硬件错误处理程序 (LLHEH) 调用 PSHED，以便它可以将有关错误条件的任何补充信息添加到硬件错误数据包之前 LLHEH 向操作系统报告错误。

-   Windows 内核调用 PSHED，以便它可以将任何补充错误记录部分添加到描述错误条件的错误记录。

-   对于已更正错误，错误的处理后，将注册到 PSHED 以便它可以清除错误源的错误状态的内核调用 Windows 完成。

PSHED 支持错误情况，报告的标准错误源 PSHED 发现错误的信息检索的操作。 如果参与实现插件 PSHED[错误源发现](error-source-discovery.md)和其他错误源到操作系统 PSHED 不支持，插件 PSHED 必须也参与错误信息的报表检索以支持为这些错误源的错误信息检索操作。 PSHED 插件可以选择性地参与错误信息检索提供的标准错误源报告的错误情况的其他错误信息。

**请注意**   PSHED 插件参与错误信息检索必须也参与[错误源发现](error-source-discovery.md)如果属于以下任一种情况：
-   PSHED 插件提供了到特定的错误源报告的硬件错误数据包的其他错误信息。 在这种情况下，插件 PSHED 必须修改中包含的值**MaxRawDataLength**的成员[ **WHEA\_错误\_源\_描述符** ](https://msdn.microsoft.com/library/windows/hardware/ff560505)错误源发现的其他错误信息期间该错误源的结构。

-   PSHED 插件提供其他错误的错误记录到记录部分有硬件错误报告受特定错误的来源。 在这种情况下，插件 PSHED 必须修改中包含的值**MaxSectionsPerRecord** WHEA 成员\_错误\_源\_描述符结构的该错误源错误源发现，以便获得更多错误记录部分。

 

有关如何实现插件参与 PSHED 错误信息检索方面的详细信息，请参阅[参与中错误的信息检索](participating-in-error-information-retrieval.md)。

 

 




