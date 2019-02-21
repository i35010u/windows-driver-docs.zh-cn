---
title: 与智能卡驱动程序库的交互
description: 与智能卡驱动程序库的交互
ms.assetid: 44cf41f4-bbff-4193-afad-6d4106ce50c3
keywords:
- Ioctl WDK 智能卡
- 供应商提供的驱动程序 WDK 的智能卡，IOCTL 请求管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f95c29dc67c6215d43effa346b96ec29dbe6f36
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533921"
---
# <a name="interaction-with-the-smart-card-driver-library"></a>与智能卡驱动程序库的交互


## <span id="_ntovr_interaction_with_the_smart_card_driver_library"></span><span id="_NTOVR_INTERACTION_WITH_THE_SMART_CARD_DRIVER_LIBRARY"></span>


下图显示了读卡器驱动程序交互的方式与智能卡驱动程序库来处理它从资源管理器收到的 IOCTL 请求：

![说明如何使用智能卡驱动程序库来处理 ioctl 请求交互读卡器驱动程序的关系图 ](images/memnum3.png)

下面的编号，与上图中的数字相对应。 从数字 1 开始，该图显示的步骤 （以及系统提供的驱动程序库中） 完成读卡器驱动程序必须处理 IOCTL 请求：

1.  读卡器驱动程序将传递到所有 IOCTL 请求[ **SmartcardDeviceControl (WDM)** ](https://msdn.microsoft.com/library/windows/hardware/ff548939)驱动程序库例程。

2.  如果读卡器驱动程序将传递给参数[ **SmartcardDeviceControl** ](https://msdn.microsoft.com/library/windows/hardware/ff548939)不正确， **SmartcardDeviceControl**返回一条错误消息。 **SmartcardDeviceControl**返回，而不完成 IOCTL 请求。 在这种情况下，读卡器驱动程序必须完成 IOCTL 请求。

3.  如果参数有效， [ **SmartcardDeviceControl** ](https://msdn.microsoft.com/library/windows/hardware/ff548939)如果它能够处理 IOCTL 请求。

4.  [**SmartcardDeviceControl** ](https://msdn.microsoft.com/library/windows/hardware/ff548939)检查读卡器驱动程序是否正在处理的 IOCTL 请求定义的回调例程。 如果回调存在，则**SmartcardDeviceControl**调用它。

5.  回调例程调用所有驱动程序完成处理 IOCTL 请求所需的库例程。

6.  在处理 IOCTL 请求之后, 回调例程将返回到[ **SmartcardDeviceControl**](https://msdn.microsoft.com/library/windows/hardware/ff548939)。

7.  [**SmartcardDeviceControl** ](https://msdn.microsoft.com/library/windows/hardware/ff548939)完成执行 IOCTL IRP。

8.  [**SmartcardDeviceControl** ](https://msdn.microsoft.com/library/windows/hardware/ff548939)将控制权返回给读卡器驱动程序调度例程。

智能卡库同步到读卡器驱动程序的访问。 没有两个回调函数将调用一次。 但是，必须以异步方式处理的事件处理卡插入和删除。

 

 





