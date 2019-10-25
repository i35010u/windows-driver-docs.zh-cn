---
title: Windows 7 的 WHEA 更改
description: Windows 7 的 WHEA 更改
ms.assetid: d92c2be0-732b-4fcd-b517-5cb9eccf962b
keywords:
- Windows 硬件错误体系结构 WDK，Windows 7 更改
- WHEA WDK，Windows 7 更改
- Windows 7 WDK WHEA
- Windows 7 WDK WHEA，WHEA 更改
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 57e38c7bbed34a379b6d1d42acbb64ce178c8f9d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843282"
---
# <a name="whea-changes-for-windows-7"></a>Windows 7 的 WHEA 更改


从 Windows 7 开始，对 Windows 硬件错误体系结构（WHEA）进行了以下更改：

-   在 windows 7 和更高版本的 Windows 中，会使用一种新的错误记录格式（[**WHEA\_错误\_数据包\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_error_packet_v2)）来报告硬件错误。 以前的错误记录格式（[WHEA\_错误\_数据包](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff560465(v=vs.85))）已重命名为[**WHEA\_错误\_数据包\_V1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_error_packet_v1)，仅用于报告 Windows Server 2008 和 windows Vista SP1 中的硬件错误。

    从 Windows 7 Windows 驱动程序工具包（WDK）开始，WHEA\_错误\_数据包是一个宏，该宏根据生成目标引用 WHEA\_错误\_数据包\_V1 或 WHEA\_\_的数据包\_V2 结构。

    有关此更改的详细信息，请参阅[WHEA\_ERROR\_PACKET](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff560465(v=vs.85))。

-   Windows 7 Windows 驱动程序工具包（WDK）中已重命名了各种 Windows 硬件错误体系结构（WHEA）数据类型。 有关这些更改的详细信息，请参阅[重命名的 WHEA 数据类型](renamed-whea-data-types.md)。

-   对于错误纠正代码（ECC）内存，WHEA 支持预测性故障分析（PFA）。 通过 PFA，WHEA 可以监视一个或多个已遇到以前错误的 ECC 内存页。 如果发生太多错误，WHEA 会尝试将内存页面置于脱机状态。

    [特定于平台的硬件错误驱动程序（PSHED）插件](platform-specific-hardware-error-driver-plug-ins2.md)可以通过在 ECC 内存上执行 PFA，来扩展 WHEA 的 PFA 支持。 通过这种方式，插件必须决定何时将内存页面置于脱机状态。

-   已定义其他 WHEA 错误特定硬件错误。 有关这些错误的详细信息，请参阅[WHEA 硬件错误事件（Windows Server 2008、Windows VISTA SP1 及更高版本）](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff560537(v=vs.85))。

 

 




