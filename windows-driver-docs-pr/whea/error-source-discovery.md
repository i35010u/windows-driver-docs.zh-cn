---
title: 错误源发现
description: 错误源发现
ms.assetid: 58b7501d-b51a-436f-ac29-8d03161d0956
keywords:
- Windows 硬件错误体系结构 WDK、 错误源发现
- WHEA WDK、 错误源发现
- 硬件错误 WDK WHEA，错误源发现
- WDK WHEA，错误源发现的错误
- 特定于平台的硬件错误驱动程序插件 WDK WHEA，错误源发现
- PSHED 插件 WDK WHEA 错误源发现
- 错误源发现 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e3bc3c4e90efb599b74768a0df920c874141239
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340871"
---
# <a name="error-source-discovery"></a>错误源发现


在初始化期间的操作系统，Windows 内核查询有关的所有列表 PSHED[错误源](hardware-errors-and-error-sources.md)实现的硬件平台。 PSHED 返回一系列[ **WHEA\_错误\_源\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff560505)描述了每个硬件平台支持的错误源的结构. 操作系统使用此信息来启用负责处理从硬件平台的错误通知的必要低级别的硬件错误处理程序 (LLHEHs)。

下面是发现的 PSHED 错误源的最小集。

<a href="" id="x86-based-and-x64-based-hardware-platforms"></a>**基于 x86 和基于 x64 的硬件平台**  
-   计算机检查异常 (MCE)

-   更正计算机检查 (CMC)

-   不可屏蔽的中断 (NMI)

-   启动错误

<a href="" id="itanium-based-hardware-platforms"></a>**基于 Itanium 的硬件平台**  
-   计算机检查中止 (MCA)

-   更正计算机检查 (CMC)

-   已更正的平台错误 (CPE)

-   初始化错误

PCI Express (PCIe) 高级错误报告 (AER)，为 PCI 总线驱动程序发现而不是 PSHED 的错误源。 因此，PSHED 不包括在它返回到 Windows 内核的错误源的初始列表中的任何 PCIe AER 错误源。 相反，PCI 总线驱动程序向操作系统报告这些错误源。 当此类错误源会报告给操作系统到 PSHED Windows 内核调用，以允许 PSHED 提供有关错误源的任何其他详细信息。

PSHED 插件还可以参与错误源发现修改 PSHED 报告的错误源信息并报告未由 PSHED 的其他错误源。 如果 PSHED 插件实现它参与了错误源发现并报告其他错误源到 PSHED 不支持的操作系统，插件 PSHED 必须也参与[错误源控制](error-source-control.md)并[错误的信息检索](error-information-retrieval.md)以支持错误源控件和这些额外的错误源的错误的信息检索操作。 有关如何参与 PSHED 插件实现中发现错误源的详细信息，请参阅[参与错误源发现](participating-in-error-source-discovery.md)。

 

 




