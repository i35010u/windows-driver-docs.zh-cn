---
title: 使用传感器类扩展来处理事件
description: 传感器类扩展处理传感器驱动程序和传感器 API 之间的事件链接。
ms.assetid: A49489EF-1721-4F12-9793-6FBA76BA7976
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 795e5e55a545dc6fd42fc0979c79aeb86cb57e74
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326177"
---
# <a name="using-the-sensor-class-extension-to-handle-events"></a>使用传感器类扩展来处理事件

> [!IMPORTANT] 
> 已弃用此文档和 Windows 8.1 的地理位置驱动程序示例。

传感器类扩展处理传感器驱动程序和传感器 API 之间的事件链接。

传感器应用程序检索模拟的传感器的数据字段通过注册从驱动程序; 接收事件通知或者，通过调用要检索的数据字段的属性。 示例驱动程序同时支持。

如果应用程序注册为数据更新事件，该驱动程序将引发这些事件，每次从传感器到达该数据。 这些事件通知的频率与当前报告间隔属性相对应。

引发事件时，驱动程序模拟来自传感器的"新"数据，除了示例驱动程序也会引发传感器已准备好开始发送数据时发生的事件。 此事件被称为状态更改事件。

支持的示例驱动程序的状态对应于在中找到的常数**SensorState**枚举：

| 事件状态常量 | 重要性                                                   |
|----------------------|----------------------------------------------------------------|
| 传感器\_状态\_准备就绪 | 指示传感器已连接并且准备好发送数据。 |

 

如前文所述，传感器类扩展处理的示例驱动程序和传感器 API 之间的事件链接。 该驱动程序调用每次**ISensorClassExtension::PostStateChange**方法，则类扩展会将通知转发到 API。 示例驱动程序调用此方法内的**CSensorManager::SetState**。 当驱动程序调用**ISensorClassExtension::PostEvent**方法，并提供数据更新事件，此类扩展的属性键会将通知转发到传感器 API。 示例驱动程序调用此方法内的**CSensorManager::PostDataEvent**。

两个传感器管理器方法::**SetState**和::**PostDataEvent**中的事件的示例驱动程序的线程过程调用**CSensorManager::\_SensorEventThreadProc**。 在单独的线程过程以防止事件活动阻止驱动程序 （如回调函数） 中的同步过程中保留的事件处理程序。

## <a name="related-topics"></a>相关主题
[传感器地理位置驱动程序示例](sensors-geolocation-driver-sample.md)  



