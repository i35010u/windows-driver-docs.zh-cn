---
title: 由 PSHED 插件执行的 PFA
description: 由 PSHED 插件执行的 PFA
ms.assetid: e9876c86-b059-406f-a01a-7670ab294098
keywords:
- 预计故障分析 (PFA) WDK WHEA，PSHED 插件
- PFA WDK WHEA，PSHED 插件
- 特定于平台的硬件错误驱动程序 (PSHED) WDK WHEA
- 特定于平台的硬件错误驱动程序 (PSHED) WDK WHEA，预计故障分析
- PSHED 插件 WDK WHEA
- PSHED 插件 WDK WHEA，预计故障分析
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c7c32ed8ba9ddbae690702177aabd298a106f8f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387158"
---
# <a name="pfa-performed-by-a-pshed-plug-in"></a>由 PSHED 插件执行的 PFA


一个[特定于平台的硬件错误驱动程序 (PSHED) 插件](platform-specific-hardware-error-driver-plug-ins2.md)可以对 ECC 内存执行预测故障分析 (PFA)。 在这种情况，该插件和不 WHEA 必须监视 ECC 内存页。 如果该插件确定 ECC 内存页已超出错误阈值，它表示 WHEA 到此状态。 WHEA 然后尝试使内存页处于脱机状态。

**请注意**PSHED 插件执行 PFA，并使用注册表来存储其配置设置，例如错误阈值和监视超时，如果它不应依赖于或使用 WHEA PFA 配置设置中所述[WHEA策略设置](whea-pfa-registry-settings.md)。



ECC 内存错误时，WHEA 和插件将执行以下步骤：

1.  *低级别的硬件错误处理程序*(*LLHEH*) 通知的内存错误条件是否存在。

2.  LLHEH 从错误源中检索有关内存错误的信息，并使用错误数据完成硬件错误数据包。 此数据包的格式设置为[WHEA\_错误\_数据包](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff560465(v=vs.85))结构。

3.  若要检索特定于平台的硬件错误的任何信息 PSHED LLHEH 调用。 如果 PSHED 插件中安装并注册要检索有关错误的信息，PSHED 将调入 PSHED 插件，以便该插件可以修改返回给 LLHEH 错误有关的信息。

4.  LLHEH 调用 Windows 操作系统内核，并将其传递错误数据包。

5.  创建 Windows 内核[错误记录](error-records.md)并向其添加信息从 LLHEH 从接收到的错误数据包。 此外，Windows 内核添加有关错误的其他信息，例如错误源、 错误和多少次的严重级别的错误记录到发生了错误。

6.  Windows 内核调用 PSHED 允许 PSHED 将部分添加到的错误记录。

7.  如果 PSHED 插件安装并注册，无法检索错误信息，PSHED 将调入 PSHED 插件，以便它可以修改的错误记录中的信息。

8.  如果插件 PSHED ECC 内存页上执行的 PFA，它必须执行以下操作：

    -   设置**PlatformPfaControl**位[ **WHEA\_错误\_数据包\_标志**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_error_packet_flags)隶属[WHEA\_错误\_数据包](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff560465(v=vs.85))结构。 如果设置此位，WHEA 不再负责 PFA 内存该页上。
    -   如果该插件确定，遇到了错误的 ECC 内存页面应使其脱机，则设置**PlatformDirectedOffline**位[ **WHEA\_错误\_数据包\_标志**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_error_packet_flags)成员。 如果设置此位，WHEA 会尝试使内存页脱机。

    否则，必须清除插件 PSHED **PlatformPfaControl**并**PlatformDirectedOffline**中的位[ **WHEA\_错误\_数据包\_标志**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_error_packet_flags)的成员[WHEA\_错误\_数据包](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff560465(v=vs.85))结构。

    **请注意**如果**PlatformPfaControl**位将清，WHEA 执行 PFA，如果配置为执行此操作，并且将确定是否遇到了错误的 ECC 内存页面应使其脱机。 有关此过程的详细信息，请参阅[PFA 由 WHEA](pfa-performed-by-whea.md)。



9.  如果 ECC 内存页应使脱机，WHEA 首先调用系统内存管理器来执行此操作。

    **请注意**调用时系统内存管理器，则 ECC 内存页将使脱机实际上不能保证。




WHEA 然后将内存页添加到系统上的启动配置数据 (BCD) 存储。 这可以防止在下次系统重新启动后会使用内存页。

**请注意**WHEA 会使硬件组件，例如 ECC 内存页脱机如果注册表值**DisableOffline**设置为非零值。 此外，WHEA 将内存页到 BCD 存储如果添加的注册表值**MemPersistOffline**设置为 0。 有关注册表值的详细信息，请参阅[WHEA 策略设置](whea-pfa-registry-settings.md)。



有关系统内存管理器的详细信息，请参阅[内存管理](https://go.microsoft.com/fwlink/p/?linkid=140723)Windows SDK 文档中。


10. Windows 内核会生成一个 ETW 事件和系统事件日志中记录错误的信息。








