---
title: 使用传感器类扩展来处理事件
description: 传感器类扩展处理传感器驱动程序和传感器 API 之间的事件链接。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cac89bb5f2fb84420ad10a02005292dec9872f8e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825991"
---
# <a name="using-the-sensor-class-extension-to-handle-events"></a>使用传感器类扩展来处理事件

> [!IMPORTANT] 
> 此文档和 Windows 8.1 的地理位置驱动程序示例已弃用。

传感器类扩展处理传感器驱动程序和传感器 API 之间的事件链接。

传感器应用程序通过注册接收来自驱动程序的事件通知来检索模拟传感器的数据字段;或者，通过调用属性来检索数据字段。 示例驱动程序同时支持这两者。

如果某个应用程序注册了数据更新事件，则每次该数据到达传感器时，驱动程序就会引发这些事件。 这些事件通知的频率与当前报表间隔属性相对应。

除了在驱动程序模拟从传感器传入的 "新" 数据时引发事件外，当传感器准备好开始发送数据时，示例驱动程序还会引发事件。 此事件称为 "状态更改事件"。

示例驱动程序支持的状态对应于在 **SensorState** 枚举中找到的常数：

| Event-State 常量 | 含义                                                   |
|----------------------|----------------------------------------------------------------|
| 传感器 \_ 状态 \_ 就绪 | 指示传感器已连接并且已准备好发送数据。 |

 

如前文所述，传感器类扩展处理示例驱动程序和传感器 API 之间的事件链接。 每当驱动程序调用 **ISensorClassExtension：:P oststatechange** 方法时，类扩展就会将通知转发到该 API。 示例驱动程序在 **CSensorManager：： SetState** 中调用此方法。 当驱动程序调用 **ISensorClassExtension：:P ostevent** 方法并为数据更新事件提供属性键时，类扩展会将通知转发到传感器 API。 示例驱动程序在 CSensorManager 中调用此方法 **：:P ostdataevent**。

在事件 **CSensorManager：： \_ SensorEventThreadProc** 的示例驱动程序的线程过程中，将调用两个传感器管理器方法：：**SetState** 和：：**PostDataEvent** 。 事件处理程序保留在单独的线程过程中，以防止事件活动阻止驱动程序中的同步过程 (如) 回调函数。

## <a name="related-topics"></a>相关主题
[传感器地理位置驱动程序示例](sensors-geolocation-driver-sample.md)  



