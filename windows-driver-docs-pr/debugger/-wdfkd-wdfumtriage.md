---
title: wdfkd_wdfumtriage
description: Wdfkd_wdfumtriage 扩展将显示在系统上，包括设备对象、 加载驱动程序和类扩展，即插即用设备堆栈 UMDF 设备调度 Irp 的信息。
ms.assetid: E25DAE56-E42A-4A56-B36F-8B0B1D826524
keywords:
- wdfkd_wdfumtriage Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd_wdfumtriage
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 36146a80a288aabc380f7d9afa757fa0f335d191
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534891"
---
# <a name="wdfkdwdfumtriage"></a>!wdfkd\_wdfumtriage


**！ Wdfkd\_wdfumtriage**扩展系统，其中包括相应主机进程、 加载驱动程序和类扩展，即插即用设备堆栈、 即插即用设备的设备对象上显示所有 UMDF 设备有关的信息节点已发送 Irp 和如果相关的问题状态。

```dbgcmd
!wdfkd.wdfumtriage
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Wdfkd.dll

## <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>框架


UMDF 2

## <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息


有关详细信息，请参阅[内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

可以在内核模式调试会话中使用此命令。

下面是输出的示例 **！ wdfkd\_wdfumtriage**。

![从驱动程序对象列表输出 ！ wdfkd.wdfumtriage](images/wdfumtriage2.png)

 

 





