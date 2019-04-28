---
title: WHEA 如何在 ECC 内存上执行 PFA
description: WHEA 如何在 ECC 内存上执行 PFA
ms.assetid: def94688-9ca6-4146-8d5b-4c3550d3d272
keywords:
- 预计故障分析 (PFA) WDK WHEA，错误更正代码内存
- PFA WDK WHEA，错误更正代码内存
- 错误更正代码内存 WDK WHEA
- 错误更正代码内存 WDK WHEA，预计故障分析
- 低级别的硬件错误处理程序 WDK WHEA
- LLHEH WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd43fbbff691133978503716618368cbabed8a7a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340810"
---
# <a name="how-whea-performs-pfa-on-ecc-memory"></a>WHEA 如何在 ECC 内存上执行 PFA


从 Windows 7 开始，Windows 硬件错误体系结构 (WHEA) 支持错误更正代码 (ECC) 内存用于预测故障分析 (PFA)。

WHEA 执行 PFA ECC 内存页上，仅当满足以下条件：

-   注册表值**MemPfaDisable**不设置为 1。

-   一个[特定于平台的硬件错误驱动程序 (PSHED) 插件](platform-specific-hardware-error-driver-plug-ins2.md)以前未设置**PlatformPfaControl**位[ **WHEA\_错误\_数据包\_标志**](https://msdn.microsoft.com/library/windows/hardware/ff560472)的成员[WHEA\_错误\_数据包](https://msdn.microsoft.com/library/windows/hardware/ff560465)结构为 1。 该插件前提它执行 PFA 设置此位。 有关如何 PFA 执行此插件的详细信息，请参阅[PFA 由 PSHED 插件](pfa-performed-by-a-pshed-plug-in.md)。

ECC 内存出错时的内存页面上，WHEA PFA 页上执行 ECC 内存通过执行以下步骤：

1.  如果当前未监视 WHEA ECC 内存页，WHEA 将页面添加到其监视数据库，并清除错误计数和计时周期计数来添加新项。

    **请注意**WHEA 将停止监视 ECC 内存页时其计时周期计数超过**MemPfaTimeout**注册表值。 在此情况下，WHEA 从其监视数据库中删除该条目。



2.  WHEA 递增 ECC 内存页的错误计数。

3.  如果错误计数超过**MemPfaThreshold**注册表值，WHEA 首次调用的系统内存管理器以使脱机 ECC 内存页。

    **请注意**调用时系统内存管理器，则 ECC 内存页将使脱机实际上不能保证。




WHEA 然后添加内存页中的系统存储到引导配置数据 (BCD)。 这可以防止在下次系统重新启动后会使用内存页。

**请注意**WHEA 会使硬件组件，例如 ECC 内存页脱机如果注册表值**DisableOffline**设置为非零值。 此外，WHEA 会 ECC 内存页到 BCD 存储如果添加的注册表值**MemPersistOffline**设置为 0。




WHEA 为 PFA 注册表值的详细信息，请参阅[WHEA 策略设置](whea-pfa-registry-settings.md)。

有关系统内存管理器的详细信息，请参阅[内存管理](https://go.microsoft.com/fwlink/p/?linkid=140723)Windows SDK 文档中。








