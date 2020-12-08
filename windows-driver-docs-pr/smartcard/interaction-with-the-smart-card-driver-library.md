---
title: 与智能卡驱动程序库的交互
description: 与智能卡驱动程序库的交互
keywords:
- IOCTLs WDK 智能卡
- 供应商提供的驱动程序 WDK 智能卡，IOCTL 请求管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb041709b3c25bc254fc8a0e2c3179de590771fa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804929"
---
# <a name="interaction-with-the-smart-card-driver-library"></a>与智能卡驱动程序库的交互


## <span id="_ntovr_interaction_with_the_smart_card_driver_library"></span><span id="_NTOVR_INTERACTION_WITH_THE_SMART_CARD_DRIVER_LIBRARY"></span>


下图显示了读取器驱动程序如何与智能卡驱动程序库交互，以便处理从资源管理器接收的 IOCTL 请求：

![说明读取器驱动程序如何与智能卡驱动程序库交互以处理 ioctl 请求的关系图 ](images/memnum3.png)

以下数字与上图中的数字相对应。 从数字1开始，该图显示了读取器驱动程序必须 (与系统提供的驱动程序库一起完成的步骤，) 才能处理 IOCTL 请求：

1.  读取器驱动程序将所有 IOCTL 请求传递到 [**SmartcardDeviceControl (WDM)**](/previous-versions/ff548939(v=vs.85)) 驱动程序库例程。

2.  如果读取器驱动程序传递到 [**SmartcardDeviceControl**](/previous-versions/ff548939(v=vs.85)) 的参数不正确，则 **SmartcardDeviceControl** 返回并返回错误消息。 **SmartcardDeviceControl** 返回，但不完成 IOCTL 请求。 在这种情况下，读取器驱动程序必须完成 IOCTL 请求。

3.  如果参数有效， [**SmartcardDeviceControl**](/previous-versions/ff548939(v=vs.85)) 将处理 IOCTL 请求（如果可能）。

4.  [**SmartcardDeviceControl**](/previous-versions/ff548939(v=vs.85)) 检查读取器驱动程序是否具有为其正在处理的 IOCTL 请求定义的回调例程。 如果回调存在， **SmartcardDeviceControl** 将调用该回调。

5.  回调例程调用完成 IOCTL 请求处理所需的所有驱动程序库例程。

6.  处理 IOCTL 请求后，回调例程返回到 [**SmartcardDeviceControl**](/previous-versions/ff548939(v=vs.85))。

7.  [**SmartcardDeviceControl**](/previous-versions/ff548939(v=vs.85)) 完成携带 IOCTL 的 IRP。

8.  [**SmartcardDeviceControl**](/previous-versions/ff548939(v=vs.85)) 向读取器-驱动程序调度例程返回控制权。

智能卡库同步对读取器驱动程序的访问。 同时不会调用两个回调函数。 但是，必须异步处理卡片插入和移除的事件处理。

 

