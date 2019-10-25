---
title: 电源状态
description: NFC 类扩展驱动程序用作设备的电源策略所有者，因此它在其设备初始化例程期间调用 WdfDeviceInitSetPowerPolicyOwnership （TRUE）。
ms.assetid: 12433344-9C33-415B-BA14-4BD4C7E838CC
keywords:
- NFC
- 近场通信
- proximity
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c1ad8e01cd57727a295f4937d180436d6f1a70c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834040"
---
# <a name="power-states"></a>电源状态


NFC 类扩展驱动程序用作设备的电源策略所有者，因此它在其设备初始化例程期间调用[**WdfDeviceInitSetPowerPolicyOwnership**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyownership)（TRUE）。

NFC CX 驱动程序支持设备电源状态 D0 和 D3。 下图显示了两个电源状态之间的转换。 处于空闲状态的设备处于 D3 电源状态，其中的 NFCC 没有电源。 当收音机模式处于活动状态，并且任何模块（如 NFP 的活动发布或来自 NFP DDI 的订阅）、SE （模拟模式下的活动安全元素 NFCSE DDI）或智能卡处于活动状态时，状态将转换为 D0。 在此转换过程中，将更新设备的轮询状态，以满足所有活动模块的要求。

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

IdleTimeout 默认值为1秒。 此设置可通过[**NFC\_CX\_客户端\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/ns-nfccx-_nfc_cx_client_config)中的*PowerIdleTimeout*参数进行配置。 下图显示了使用 WDF 空闲检测方法时隐含的各种电源转换。

客户端驱动程序可以选择通过[**NFC\_CX\_客户端\_配置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/ns-nfccx-_nfc_cx_client_config)结构的**IsPowerPolicyOwner**成员来成为堆栈的电源策略所有者。 这对于需要配置附加设备电源状态的传输（例如 USB）可能会很有用。

![电源管理操作](images/powermanagementoperations.png)

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口（DDI）概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[NFC 类扩展（CX）参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

