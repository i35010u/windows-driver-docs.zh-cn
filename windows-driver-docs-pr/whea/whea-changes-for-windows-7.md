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
ms.openlocfilehash: f3fa60e7cc3fb01bde27994886b390a89813e478
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216306"
---
# <a name="whea-changes-for-windows-7"></a>Windows 7 的 WHEA 更改


从 Windows 7 开始，对 Windows 硬件错误体系结构进行了以下更改 (WHEA) ：

-   新的错误记录格式 ([**WHEA \_ 错误 \_ 数据包 \_ V2**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_error_packet_v2)) 用于在 windows 7 及更高版本的 windows 中报告硬件错误。 以前的错误记录格式 ([WHEA \_ 错误 \_ 数据包](/previous-versions/windows/hardware/drivers/ff560465(v=vs.85))) 已重命名为 [**WHEA \_ 错误 \_ 数据包 \_ V1**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_error_packet_v1)，仅用于在 windows Server 2008 和 windows Vista SP1 中报告硬件错误。

    从 Windows 7 Windows 驱动程序工具包开始 (WDK) ，WHEA \_ 错误 \_ 数据包是一个宏，根据生成目标，引用 WHEA \_ 错误 \_ 数据包 \_ V1 或 WHEA \_ 错误 \_ 数据包 \_ V2 结构。

    有关此更改的详细信息，请参阅 [WHEA \_ 错误 \_ 数据包](/previous-versions/windows/hardware/drivers/ff560465(v=vs.85))。

-   Windows 7 Windows 驱动程序工具包 (WDK) 中 (WHEA) 数据类型的各种 Windows 硬件错误体系结构已重命名。 有关这些更改的详细信息，请参阅 [重命名的 WHEA 数据类型](renamed-whea-data-types.md)。

-   WHEA 支持预测性故障分析 (PFA) ，) 内存 (ECC 错误更正代码。 通过 PFA，WHEA 可以监视一个或多个已遇到以前错误的 ECC 内存页。 如果发生太多错误，WHEA 会尝试将内存页面置于脱机状态。

    [ (PSHED) 插件的特定于平台的硬件错误驱动程序](platform-specific-hardware-error-driver-plug-ins2.md)可以通过在 ECC 内存上执行 PFA，来扩展 WHEA 的 PFA 支持。 通过这种方式，插件必须决定何时将内存页面置于脱机状态。

-   已定义其他 WHEA 错误特定硬件错误。 有关这些错误的详细信息，请参阅 [WHEA 硬件错误事件 (Windows Server 2008、Windows VISTA SP1 和更高版本) ](/previous-versions/windows/hardware/drivers/ff560537(v=vs.85))。

 

