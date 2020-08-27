---
description: 处理即插即用和电源管理事件
title: 处理即插即用和电源管理事件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 394e19669008f36592fba1ed572e7036a627c35a
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88968792"
---
# <a name="handling-plug-and-play-and-power-management-events"></a>处理即插即用和电源管理事件


如果即插即用 (PnP) 或电源管理 (PM) 事件发生，则用户模式驱动程序框架 (UMDF) 调用 CDevice 类中的一个或多个方法来处理事件。  (CDevice 类*在文件 IPnpCallback*中定义。 ) 事件处理程序可在以下三个接口中找到： **IPnpCallback**、 **IPnpCallbackHardware**和**IPnpCallbackSelfManagedIo**。

在 WpdHelloWorldDriver 示例中，大多数 PnP 和 PM 事件处理程序要么不返回任何值，要么返回 \_ "OK"。 有两个例外： **IPnpCallbackHardware：： OnPrepareHardware**和 **IPnpCallbackHardware：： OnReleaseHardware**。 下表描述了每种方法。

IPnpCallbackHardware：： OnPrepareHardware * * * *：调用 **WpdBaseDriver：： Initialize** 方法。 初始化 WPD 类扩展并更新设备友好名称。

IPnPCallbackHardware：： OnReleaseHardware * * * *：调用 **WpdBaseDriver：：** 伪类方法，并取消 WPD 类扩展。


 

有关每个接口及其方法的说明，请参阅 [UMDF 文档](https://go.microsoft.com/fwlink/p/?linkid=153678)。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





