---
title: 错误信息检索
description: 错误信息检索
ms.assetid: 4af06727-9660-4bbc-8c9e-a50c8f2d566d
keywords:
- Windows 硬件错误体系结构 WDK，错误信息检索
- WHEA WDK，错误信息检索
- 硬件错误 WDK WHEA，错误信息检索
- 错误 WDK WHEA，错误信息检索
- 平台特定硬件错误驱动程序插件 WDK WHEA、错误信息检索
- PSHED 插件 WDK WHEA，错误信息检索
- 错误信息检索 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7db8bf1551c2e771dbd1f126b4921beed3e2045
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844790"
---
# <a name="error-information-retrieval"></a>错误信息检索


在处理硬件错误情况时，会在错误处理过程中的三个不同点调用 PSHED。

-   低级别硬件错误处理程序（LLHEH）调用到 PSHED，以便它可以将有关错误情况的任何补充信息添加到硬件错误数据包，然后 LLHEH 将错误报告给操作系统。

-   Windows 内核调入 PSHED，以便可以将任何补充错误记录部分添加到描述错误情况的错误记录。

-   对于更正后的错误，Windows 内核会调入 PSHED，以便在处理完错误后清除错误源的错误状态寄存器。

对于由 PSHED 发现的标准错误源报告的错误条件，PSHED 支持错误信息检索操作。 如果实现了参与[错误源发现](error-source-discovery.md)的 PSHED 插件，并向 PSHED 不支持的操作系统报告其他错误源，则 PSHED 插件还必须参与错误消息检索，以支持这些错误源的错误信息检索操作。 PSHED 插件还可以选择参与错误信息检索，以便为标准错误源报告的错误条件提供额外的错误信息。

  **请注意**，如果满足以下任一条件，则参与错误信息检索的 PSHED 插件还必须参与[错误源发现](error-source-discovery.md)：
-   PSHED 插件向特定错误源报告的硬件错误数据包提供额外的错误信息。 在这种情况下，PSHED 插件必须修改 WHEA\_错误的**MaxRawDataLength**成员中包含的值，以便在错误源发现期间为该错误源[ **\_源\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_error_source_descriptor)结构，以考虑额外的错误信息。

-   对于特定错误源报告的硬件错误，PSHED 插件为错误记录提供其他错误记录部分。 在这种情况下，PSHED 插件必须修改 WHEA\_错误的**MaxSectionsPerRecord**成员中包含的值，以便在错误源发现期间为其他错误记录分区\_源\_描述符结构。

 

有关如何实现参与错误信息检索的 PSHED 插件的详细信息，请参阅[参与错误信息检索](participating-in-error-information-retrieval.md)。

 

 




