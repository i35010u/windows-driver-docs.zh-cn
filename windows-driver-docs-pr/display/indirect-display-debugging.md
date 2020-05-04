---
title: 调试间接显示驱动程序
description: 介绍间接显示的调试技术
ms.assetid: a343812d-03d0-4a95-9c36-7e6b5a404088
ms.date: 04/22/2020
ms.localizationpriority: medium
ms.openlocfilehash: 1cb1feb250ae96882d5d77bc2327707c837296e2
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "82107410"
---
# <a name="debugging-indirect-displays"></a>调试间接显示

间接显示驱动程序是 UMDF 驱动程序，因此，UMDF 调试文档是一个很好的起点，[这里](https://docs.microsoft.com/windows-hardware/drivers/wdf/determining-why-the-umdf-driver-fails-to-load-or-the-umdf-device-fails)是该部分中某个页面的示例。  此页将提供间接显示特定的调试信息。

## <a name="span-idregistry_controlspanspan-idregistry_controlspanspan-idregistry_controlspanregistry-control"></a><span id="Registry_Control"></span><span id="registry_control"></span><span id="REGISTRY_CONTROL"></span>注册表控件

IddCx 具有一些可用于帮助调试间接显示驱动程序的注册表设置。  所有注册表值都位于**HKLM\System\CurrentControlSet\Control\GraphicsDrivers**注册表项下。


| 值名称               | 详细信息 |
|--------------------------|---------|
| TerminateIndirectOnStall | 如果此值为零，则将禁用终止该驱动程序的监视程序（如果它未在10秒内提供可用帧）。  任何其他值都将使监视程序处于启用状态。 |
| IddCxDebugCtrl           | 启用 IddCx 的不同调试方面的位域，请参阅下表 |

**注意**如果使用 "TerminateIndirectOnStall" 注册表值禁用监视程序，则会失败。

### <a name="iddcxdebugctrl-values"></a>IddCxDebugCtrl 值

| IddCxDebugCtrl 中的位 | 含义  |
|:---------------------:|----------|
| 0x0001 | 当 IddCx 检测到错误时中断到调试器 |
| 0x0002 | 加载 IddCx 时中断调试器 |
| 0x0004 | 在卸载 IddCx 时中断到调试器 |
| 0x0008 | 调用 IddCx DriverEntry 时中断调试器 |
| 0x0010 | 在调用驱动程序绑定时中断到调试器 |
| 0x0020 | 在调用驱动程序启动时中断到调试器 |
| 0x0040 | 调用驱动程序绑定时中断调试器 |
| 0x0080 | 禁用 DDI 监视程序，在 DDI 调用中终止驱动程序的时间过长 |
| 0x0100 | 未使用 |
| 0x0200 | 启用调试覆盖，如下所示 |
| 0x0400 | 覆盖帧中超出脏 rect 的彩色 alpha 框，需要设置0x0200 |
| 0x0800 | 将 pref 统计信息覆盖到帧中需要设置0x0200 |

**注意**对于任何用于处理驱动程序创建的 Direct3D 设备并传递给 IddCxSwapChainSetDevice （）的覆盖函数，都必须使用 D3D11_CREATE_DEVICE_BGRA_SUPPORT 标志来创建。
