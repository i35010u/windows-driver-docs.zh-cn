---
title: 实现 IPowerNotify
description: 实现 IPowerNotify
ms.assetid: 8bd8b4c8-1961-41ea-ba98-41e3a732ed37
keywords:
- IPowerNotify 接口
- 通知 WDK 音频
- 电源状态更改通知 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45ed70a8f114449dd85434021ef7351a39dd6fd5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333444"
---
# <a name="implementing-ipowernotify"></a>实现 IPowerNotify


## <span id="implementing_ipowernotify"></span><span id="IMPLEMENTING_IPOWERNOTIFY"></span>


如果您的驱动程序微型端口对象 (请参阅[音频微型端口对象接口](https://msdn.microsoft.com/library/windows/hardware/ff536207)) 或流式传输对象 (请参阅[音频 Stream 对象接口](https://msdn.microsoft.com/library/windows/hardware/ff536217)) 需要了解的有关电源状态更改，它们可以支持[IPowerNotify](https://msdn.microsoft.com/library/windows/hardware/ff536947)接口在其**QueryInterface**方法和从 PortCls 系统驱动程序每次电源更改发生时接收通知。

当电源状态更改时，调用 PortCls [ **IPowerNotify::PowerChangeNotify** ](https://msdn.microsoft.com/library/windows/hardware/ff536949)方法以分别通知的微型端口和流的每个对象支持的**IPowerNotify**接口。 期间**PowerChangeNotify**调用，微型端口对象应缓存的新设备电源状态。 期间**CAdapterCommon::Init**调用 (有关示例，请参阅在 Microsoft Windows 驱动程序工具包中 Msvad 示例适配器实现\[WDK\])，微型端口驱动程序应设置其缓存的电源状态为初始值 PowerDeviceD0。

然后再调用**PowerChangeState**能耗更低，PortCls 调用到**IPowerNotify::PowerChangeNotify**以便微型端口驱动程序有机会保存任何必要的设备上下文。 此上下文可能包括体现了当前筛选器拓扑和 mixer 行设置，例如硬件寄存器值。 在调用**PowerChangeState**开启 PortCls 调用**PowerChangeNotify**以便微型端口驱动程序可以还原已保存的上下文。

PortCls 时关闭，暂停之前调用的所有活动音频数据流**PowerChangeNotify**。 当启动过程中，调用 PortCls **PowerChangeNotify**重新启动任何暂停音频数据流之前。

微型端口驱动程序微型端口和流对象的类可以继承自**IPowerNotify**接口，并支持在此接口及其**NonDelegatingQueryInterface**方法。 可以使用 IMP\_IPowerNotify 定义与标头文件添加的函数声明的 Portcls.h **PowerChangeNotify**向类定义您的驱动程序微型端口和流对象的方法。

 

 




