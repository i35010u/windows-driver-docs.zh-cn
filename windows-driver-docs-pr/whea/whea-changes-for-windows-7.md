---
title: Windows 7 的 WHEA 更改
description: Windows 7 的 WHEA 更改
ms.assetid: d92c2be0-732b-4fcd-b517-5cb9eccf962b
keywords:
- Windows 硬件错误体系结构 WDK，Windows 7： 更改
- WHEA WDK，Windows 7： 更改
- Windows 7 WDK WHEA
- Windows 7 WDK WHEA，WHEA 更改
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b556a934f98db12869340f06d83ae0b46621abc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387144"
---
# <a name="whea-changes-for-windows-7"></a>Windows 7 的 WHEA 更改


从 Windows 7 开始，以下进行了更改到 Windows 硬件错误体系结构 (WHEA):

-   新的错误记录格式 ([**WHEA\_错误\_数据包\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_error_packet_v2)) 用于报告在 Windows 7 和更高版本的 Windows 硬件错误。 以前的错误记录格式 ([WHEA\_错误\_数据包](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff560465(v=vs.85))) 已重命名为[ **WHEA\_错误\_数据包\_V1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_error_packet_v1)，，仅用于报告在 Windows Server 2008 和 Windows Vista SP1 中的硬件错误。

    开始使用 Windows 7 Windows Driver Kit (WDK)，WHEA\_错误\_数据包是一个宏，具体取决于生成目标，引用任一 WHEA\_错误\_数据包\_V1 或 WHEA\_错误\_数据包\_V2 结构。

    有关此更改的详细信息，请参阅[WHEA\_错误\_数据包](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff560465(v=vs.85))。

-   各种 Windows 硬件错误体系结构 (WHEA) 数据类型具有已重命名在 Windows 7 Windows Driver Kit (WDK)。 有关这些更改的详细信息，请参阅[重命名 WHEA 数据类型](renamed-whea-data-types.md)。

-   WHEA 错误更正代码 (ECC) 内存支持预测故障分析 (PFA)。 通过 PFA，WHEA 可以监视遇到以前的错误的一个或多个 ECC 内存页。 当发生了太多错误时，WHEA 会尝试将内存页放进入脱机状态。

    一个[特定于平台的硬件错误驱动程序 (PSHED) 插件](platform-specific-hardware-error-driver-plug-ins2.md)可以扩展 WHEA 的 PFA 支持通过对 ECC 内存执行 PFA 本身。 这种方式，该插件必须决定何时将内存页放进入脱机状态。

-   WHEA 错误特定于硬件的其他错误已定义。 有关这些错误的详细信息，请参阅[WHEA 硬件错误事件 （Windows Server 2008、 Windows Vista SP1 和更高版本）](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff560537(v=vs.85))。

 

 




