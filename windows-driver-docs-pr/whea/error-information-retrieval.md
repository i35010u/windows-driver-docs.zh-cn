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
ms.openlocfilehash: 5d3bb268c4cce76642f7d89d891415403c7684f2
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213081"
---
# <a name="error-information-retrieval"></a>错误信息检索


在处理硬件错误情况时，会在错误处理过程中的三个不同点调用 PSHED。

-   低级别硬件错误处理程序 (LLHEH) 调用到 PSHED，以便在 LLHEH 向操作系统报告错误之前，将有关错误情况的任何补充信息添加到硬件错误数据包。

-   Windows 内核调入 PSHED，以便可以将任何补充错误记录部分添加到描述错误情况的错误记录。

-   对于更正后的错误，Windows 内核会调入 PSHED，以便在处理完错误后清除错误源的错误状态寄存器。

对于由 PSHED 发现的标准错误源报告的错误条件，PSHED 支持错误信息检索操作。 如果实现了参与 [错误源发现](error-source-discovery.md) 的 PSHED 插件，并向 PSHED 不支持的操作系统报告其他错误源，则 PSHED 插件还必须参与错误消息检索，以支持这些错误源的错误信息检索操作。 PSHED 插件还可以选择参与错误信息检索，以便为标准错误源报告的错误条件提供额外的错误信息。

**注意**   如果满足以下任一条件，则参与错误信息检索的 PSHED 插件还必须参与[错误源发现](error-source-discovery.md)：
-   PSHED 插件向特定错误源报告的硬件错误数据包提供额外的错误信息。 在这种情况下，PSHED 插件必须修改错误源的[**WHEA \_ 错误 \_ 源 \_ 描述符**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_error_source_descriptor)结构的**MaxRawDataLength**成员中包含的值，以考虑其他错误信息。

-   对于特定错误源报告的硬件错误，PSHED 插件为错误记录提供其他错误记录部分。 在这种情况下，PSHED 插件必须修改错误源的 WHEA 错误源描述符结构的 **MaxSectionsPerRecord** 成员中包含的值， \_ \_ \_ 以考虑其他错误记录部分。

 

有关如何实现参与错误信息检索的 PSHED 插件的详细信息，请参阅 [参与错误信息检索](participating-in-error-information-retrieval.md)。

 

