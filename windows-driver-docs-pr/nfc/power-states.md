---
title: 电源状态
description: NFC 类扩展驱动程序充当设备的电源策略所有者，因此它在其设备初始化例程期间调用 WdfDeviceInitSetPowerPolicyOwnership(TRUE)。
ms.assetid: 12433344-9C33-415B-BA14-4BD4C7E838CC
keywords:
- NFC
- 附近通信
- 近程
- 邻近附近
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7870bf343ed2870f3330124c5a4721727690426c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533318"
---
# <a name="power-states"></a>电源状态


NFC 类扩展驱动程序充当设备的电源策略所有者这样它便可以调用[ **WdfDeviceInitSetPowerPolicyOwnership**](https://msdn.microsoft.com/library/windows/hardware/ff546776)(TRUE) 其设备初始化例程期间。

NFC CX 驱动程序支持设备的电源状态 D0 和 D3。 下面的状态关系图显示两个电源状态之间转换。 在空闲状态上的设备处于 NFCC 不具有 power D3 电源状态。 如果单选模式处于活动状态并且任何模块，如 NFP （活动发布或订阅从 NFP DDI）、 SE （从 NFCSE DDI 仿真模式中安全的活动元素） 或智能卡处于活动状态，状态将转换为 D0。 在此转换，设备的轮询状态更新以满足要求，所有活动的模块。

![电源状态](images/powerstate.png)

此外，UMDF 的内置空闲检测逻辑用于支持设备管理器。 在初始化期间，WdfDevice 分配其 S0 空闲设置，如下所示：

```cpp
WdfDeviceAssignS0IdleSettings(
    IdleCannotWakeFromS0,
    PowerDeviceD3,
    IdleTimeout,
    IdleAllowUserControl,
    WdfUseDefault
);
```

IdleTimeout 默认为 1 秒。 此设置是可通过配置*PowerIdleTimeout*中的参数[ **NFC\_CX\_客户端\_配置**](https://msdn.microsoft.com/library/windows/hardware/dn905540)。 下面的状态关系图说明了隐含 WDF 空闲检测方法使用的各种 power 转换。

客户端驱动程序可以选择是通过堆栈的电源策略所有者**IsPowerPolicyOwner**的成员[ **NFC\_CX\_客户端\_配置**](https://msdn.microsoft.com/library/windows/hardware/dn905540)结构。 这可能是用于传输如 USB 必须在其中配置其他设备的电源状态。

![电源管理操作](images/powermanagementoperations.png)

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[NFC 类扩展 (CX) 引用](https://msdn.microsoft.com/library/windows/hardware/dn905536)  

