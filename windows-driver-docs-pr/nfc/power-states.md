---
title: 电源状态
description: NFC 类扩展驱动程序用作设备的电源策略所有者，因此它在其设备初始化例程期间调用 WdfDeviceInitSetPowerPolicyOwnership (TRUE) 。
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79703611b7afcbb31dd3272775bd3f22f7fcf191
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812757"
---
# <a name="power-states"></a>电源状态


NFC 类扩展驱动程序用作设备的电源策略所有者，因此它在其设备初始化例程期间调用 [**WdfDeviceInitSetPowerPolicyOwnership**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyownership) (TRUE) 。

NFC CX 驱动程序支持设备电源状态 D0 和 D3。 下图显示了两个电源状态之间的转换。 处于空闲状态的设备处于 D3 电源状态，其中的 NFCC 没有电源。 当收音机模式处于活动状态，并且任何模块（如 NFP） (活动发布或来自 NFP DDI) 的订阅时，SE (模拟模式下的活动安全元素（来自 NFCSE DDI) 或智能卡处于活动状态），状态转换为 D0。 在此转换过程中，将更新设备的轮询状态，以满足所有活动模块的要求。

![电源状态](images/powerstate.png)

而且，UMDF 的内置空闲检测逻辑用于对设备进行电源管理。 在初始化期间，会为 WdfDevice 分配其 S0 空闲设置，如下所示：

```cpp
WdfDeviceAssignS0IdleSettings(
    IdleCannotWakeFromS0,
    PowerDeviceD3,
    IdleTimeout,
    IdleAllowUserControl,
    WdfUseDefault
);
```

IdleTimeout 默认值为1秒。 此设置可通过 [**NFC \_ CX \_ 客户端 \_ 配置**](/windows-hardware/drivers/ddi/nfccx/ns-nfccx-_nfc_cx_client_config)中的 *PowerIdleTimeout* 参数进行配置。 下图显示了使用 WDF 空闲检测方法时隐含的各种电源转换。

客户端驱动程序可以选择将其作为堆栈的电源策略所有者，通过 [**NFC \_ CX \_ 客户端 \_ 配置**](/windows-hardware/drivers/ddi/nfccx/ns-nfccx-_nfc_cx_client_config)结构的 **IsPowerPolicyOwner** 成员。 这对于需要配置附加设备电源状态的传输（例如 USB）可能会很有用。

![电源管理操作](images/powermanagementoperations.png)

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](/windows-hardware/drivers/ddi/index)  
[ (CX) 参考的 NFC 类扩展](/windows-hardware/drivers/ddi/index)
