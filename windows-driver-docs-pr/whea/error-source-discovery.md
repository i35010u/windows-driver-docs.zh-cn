---
title: 错误源发现
description: 错误源发现
ms.assetid: 58b7501d-b51a-436f-ac29-8d03161d0956
keywords:
- Windows 硬件错误体系结构 WDK，错误源发现
- WHEA WDK，错误源发现
- 硬件错误 WDK WHEA，错误源发现
- 错误 WDK WHEA，错误源发现
- 平台特定硬件错误驱动程序插件 WDK WHEA，错误源发现
- PSHED 插件 WDK WHEA，错误源发现
- 错误源发现 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70cd7e1c2cd7fa6865196d83c585d9ac84aa7a46
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844407"
---
# <a name="error-source-discovery"></a>错误源发现


在操作系统的初始化过程中，Windows 内核会在 PSHED 中查询硬件平台实现的所有[错误源](hardware-errors-and-error-sources.md)的列表。 PSHED 返回一个 WHEA\_错误列表，其中列出了描述硬件平台支持的每个错误源的[ **\_源\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_error_source_descriptor)结构。 操作系统使用此信息来启用负责处理来自硬件平台的错误通知的必要低级别硬件错误处理程序（LLHEHs）。

下面是由 PSHED 发现的最小错误源集。

<a href="" id="x86-based-and-x64-based-hardware-platforms"></a>**基于 x86 和基于 x64 的硬件平台**  
-   计算机检查异常（MCE）

-   更正了计算机检查（CMC）

-   不可屏蔽中断（NMI）

-   启动错误

<a href="" id="itanium-based-hardware-platforms"></a>**基于 Itanium 的硬件平台**  
-   计算机检查中止（MCA）

-   更正了计算机检查（CMC）

-   已更正平台错误（CPE）

-   INIT 错误

对于 PCI Express （PCIe）高级错误报告（AER），PCI 总线驱动程序将发现错误源而不是 PSHED。 因此，PSHED 不会将任何 PCIe AER 错误源包含在返回到 Windows 内核的错误源的初始列表中。 相反，PCI 总线驱动程序会将这些错误源报告给操作系统。 向操作系统报告此类错误源时，Windows 内核会调入 PSHED，以允许 PSHED 提供有关错误源的任何其他详细信息。

PSHED 插件还可以参与错误源发现，以修改 PSHED 报告的错误源信息，并报告 PSHED 未发现的其他错误源。 如果实现了参与错误源发现的 PSHED 插件，并向 PSHED 不支持的操作系统报告其他错误源，则 PSHED 插件还必须参与[错误源控制](error-source-control.md)和[错误检索信息](error-information-retrieval.md)以支持这些其他错误源的错误源控制和错误消息检索操作。 有关如何实现参与错误源发现的 PSHED 插件的详细信息，请参阅[参与错误源发现](participating-in-error-source-discovery.md)。

 

 




