---
title: WHEA 如何在 ECC 内存上执行 PFA
description: WHEA 如何在 ECC 内存上执行 PFA
ms.assetid: def94688-9ca6-4146-8d5b-4c3550d3d272
keywords:
- 预测性故障分析（PFA） WDK WHEA，纠错代码内存
- PFA WDK WHEA，纠错代码内存
- 错误更正代码内存 WDK WHEA
- 错误更正代码内存 WDK WHEA、预测性故障分析
- 低级别硬件错误处理程序 WDK WHEA
- LLHEH WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4d9cbed229c7dd2f2e677d2c24b4f5b90777983
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844402"
---
# <a name="how-whea-performs-pfa-on-ecc-memory"></a>WHEA 如何在 ECC 内存上执行 PFA


从 Windows 7 开始，Windows 硬件错误体系结构（WHEA）支持针对错误纠正代码（ECC）内存的预测性故障分析（PFA）。

仅当满足以下条件时，WHEA 才会在 ECC 内存页面上执行 PFA：

-   注册表值**MemPfaDisable**未设置为1。

-   [特定于平台的硬件错误驱动程序（PSHED）插件](platform-specific-hardware-error-driver-plug-ins2.md)以前未在 WHEA\_错误中设置**PLATFORMPFACONTROL**位[ **\_数据包\_标志**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_error_packet_flags)成员[WHEA\_错误\_数据包](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff560465(v=vs.85))结构为1。 此插件在执行 PFA 时将设置此位。 有关此插件如何执行 PFA 的详细信息，请参阅[PFA 通过 PSHED 插件执行](pfa-performed-by-a-pshed-plug-in.md)的操作。

当内存页上发生 ECC 内存错误时，WHEA 通过执行以下步骤在 ECC 内存页上执行 PFA：

1.  如果 WHEA 当前未监视 ECC 内存页，则 WHEA 会将该页添加到其监视数据库，并清除新项的错误计数和滴答计数。

    **注意** 当 ECC 内存页的滴答计数超过**MemPfaTimeout**注册表值时，WHEA 将停止对该页的监视。 发生这种情况时，WHEA 将从其监视数据库中删除该项。



2.  WHEA 递增 ECC 内存页的错误计数。

3.  如果错误计数超过**MemPfaThreshold**注册表值，WHEA 将首先调用系统内存管理器使 ECC 内存页脱机。

    **注意** 调用系统内存管理器后，不能保证 ECC 内存页将实际脱机。




然后，WHEA 将内存页添加到系统存储中的引导配置数据（BCD）中。 这会阻止在下一次系统重新启动后使用内存页。

**注意** 如果注册表值**DisableOffline**设置为非零值，则 WHEA 将不采用 ECC 内存页等硬件组件。 此外，如果注册表值**MemPersistOffline**设置为0，则 WHEA 不会将 ECC 内存页添加到 BCD 存储区。




有关 WHEA 的 PFA 注册表值的详细信息，请参阅[WHEA 策略设置](whea-pfa-registry-settings.md)。

有关系统内存管理器的详细信息，请参阅 Windows SDK 文档中的[内存管理](https://go.microsoft.com/fwlink/p/?linkid=140723)。








