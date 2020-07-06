---
Description: 处理即插即用和电源管理事件
title: 处理即插即用和电源管理事件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dbf0bb8787f271f3618d9e919822569e6b52b8ac
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85967874"
---
# <a name="handling-plug-and-play-and-power-management-events"></a>处理即插即用和电源管理事件


当发生即插即用（PnP）或电源管理（PM）事件时，用户模式驱动程序框架（UMDF）调用 CDevice 类中的一个或多个方法来处理事件。 （CDevice 类*在文件中定义。）* 可在三个接口中找到事件处理程序： **IPnpCallback**、 **IPnpCallbackHardware**和**IPnpCallbackSelfManagedIo**。

在 WpdHelloWorldDriver 示例中，大多数 PnP 和 PM 事件处理程序要么不返回任何值，要么返回 \_ "OK"。 有两个例外： **IPnpCallbackHardware：： OnPrepareHardware**和**IPnpCallbackHardware：： OnReleaseHardware**。 下表描述了每种方法。

IPnpCallbackHardware：： OnPrepareHardware * * * *：调用**WpdBaseDriver：： Initialize**方法。 初始化 WPD 类扩展并更新设备友好名称。

IPnPCallbackHardware：： OnReleaseHardware * * * *：调用**WpdBaseDriver：：** 伪类方法，并取消 WPD 类扩展。


 

有关每个接口及其方法的说明，请参阅[UMDF 文档](https://go.microsoft.com/fwlink/p/?linkid=153678)。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





