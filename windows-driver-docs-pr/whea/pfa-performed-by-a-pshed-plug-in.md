---
title: 由 PSHED 插件执行的 PFA
description: 由 PSHED 插件执行的 PFA
ms.assetid: e9876c86-b059-406f-a01a-7670ab294098
keywords:
- 预测性故障分析 (PFA) WDK WHEA、PSHED 插件
- PFA WDK WHEA，PSHED 插件
- 平台特定的硬件错误驱动程序 (PSHED) WDK WHEA
- 平台特定硬件错误驱动程序 (PSHED) WDK WHEA、预测性故障分析
- PSHED 插件-WHEA
- PSHED 插件 WDK WHEA、预测性故障分析
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b00f4c8eaf41fbfa555bb09f7cba53ae9f9f50eb
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209477"
---
# <a name="pfa-performed-by-a-pshed-plug-in"></a>由 PSHED 插件执行的 PFA


[ (PSHED) 插件的特定于平台的硬件错误驱动程序](platform-specific-hardware-error-driver-plug-ins2.md)可以对 ECC 内存 (PFA) 执行预测性故障分析。 出现这种情况时，插件和非 WHEA 必须监视 ECC 内存页。 如果该插件确定 ECC 内存页超出了错误阈值，则会将此状态指示为 WHEA。 然后，WHEA 将尝试使 "内存页" 脱机。

**注意**  如果 PSHED 插件执行 PFA 并使用注册表存储其配置设置（例如错误阈值和监视超时），则它不应依赖于或使用 [WHEA 策略设置](whea-pfa-registry-settings.md)中所述的 WHEA PFA 配置设置。



出现 ECC 内存错误时，WHEA 和插件执行以下步骤：

1.   (*LLHEH*) 的*低级硬件错误处理程序*将收到有关内存错误情况的通知。

2.  LLHEH 检索来自错误源的内存错误的相关信息，并使用错误数据来完成硬件错误数据包。 此数据包的格式为 [WHEA \_ 错误 \_ 数据包](/previous-versions/windows/hardware/drivers/ff560465(v=vs.85)) 结构。

3.  LLHEH 调用 PSHED 来检索任何特定于平台的硬件错误信息。 如果已安装并注册了 PSHED 插件来检索有关错误的信息，则 PSHED 将调入 PSHED 插件，以便插件可以修改返回到 LLHEH 的错误的相关信息。

4.  LLHEH 调用 Windows 操作系统内核并向其传递错误数据包。

5.  Windows 内核创建 [错误记录](error-records.md) ，并向其添加从 LLHEH 收到的错误数据包中的信息。 此外，Windows 内核还添加了有关错误的其他信息，如错误源、错误的严重性以及错误记录发生的次数。

6.  Windows 内核调入 PSHED，以允许 PSHED 向错误记录中添加部分。

7.  如果安装了 PSHED 插件并注册了以检索错误信息，则 PSHED 将调入 PSHED 插件，以便它可以修改错误记录中的信息。

8.  如果 PSHED 插件正在 ECC 内存页上执行 PFA，则必须执行以下操作：

    -   设置[WHEA \_ 错误 \_ 数据包](/previous-versions/windows/hardware/drivers/ff560465(v=vs.85))结构的[**WHEA \_ 错误 \_ 数据包 \_ 标志**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_error_packet_flags)成员中的**PlatformPfaControl**位。 如果设置了此位，WHEA 不再负责该内存页上的 PFA。
    -   如果该插件确定遇到错误的 ECC 内存页应脱机，请设置[**WHEA \_ 错误 \_ 数据包 \_ 标志**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_error_packet_flags)成员中的**PlatformDirectedOffline**位。 如果设置了此位，WHEA 将尝试使 "内存页" 脱机。

    否则，PSHED 插件必须清除[WHEA \_ 错误 \_ 数据包](/previous-versions/windows/hardware/drivers/ff560465(v=vs.85))结构的[**WHEA \_ 错误 \_ 数据包 \_ 标志**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_error_packet_flags)成员中的**PlatformPfaControl**和**PlatformDirectedOffline**位。

    **注意**  如果清除 **PlatformPfaControl** 位，WHEA 将执行 PFA （如果配置为执行此操作），并确定遇到错误的 ECC 内存页是否应脱机。 有关此过程的详细信息，请参阅 [WHEA 执行的 PFA](pfa-performed-by-whea.md)。



9.  如果 ECC 内存页应脱机，WHEA 将首先调用系统内存管理器以执行此操作。

    **注意**  调用系统内存管理器后，不能保证 ECC 内存页将实际脱机。




然后，WHEA 将内存页添加到系统上的引导配置数据 (BCD) 存储区中。 这会阻止在下一次系统重新启动后使用内存页。

**注意**  如果注册表值 **DisableOffline** 设置为非零值，则 WHEA 将不采用 ECC 内存页等硬件组件。 此外，如果注册表值 **MemPersistOffline** 设置为0，则 WHEA 不会将内存页添加到 BCD 存储区中。 有关注册表值的详细信息，请参阅 [WHEA 策略设置](whea-pfa-registry-settings.md)。



有关系统内存管理器的详细信息，请参阅 Windows SDK 文档中的 [内存管理](https://go.microsoft.com/fwlink/p/?linkid=140723) 。


10. Windows 内核生成 ETW 事件，并在系统事件日志中记录错误消息。