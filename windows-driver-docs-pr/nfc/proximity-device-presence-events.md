---
title: 邻近感应设备存在事件
description: 邻近感应设备存在事件
ms.assetid: 8E0E44D5-E6DD-4385-988E-EFDAA75C6D59
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f86f1908453b4019c46ec0716aa950afb03693b4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386515"
---
# <a name="proximity-device-presence-events"></a>邻近感应设备存在事件


NFP 提供程序使客户端接收的事件，只要 NFP 提供程序检测到的到达或离开近程设备 （触发操作的窗口）。 每当 NFP 提供程序检测到邻近，这意味着提供程序目前可以与一个或多个近程设备通信的提供程序需要发出*DeviceArrived*事件。 当 NFP 提供程序不再能够与任何近程设备通信时，需要发出*DeviceDeparted*事件。

NFP 提供程序还需要确保正确的已发布的消息才会传输一次设备位于邻近内时跟踪近程设备存在。 这些事件应基于相同指标。 对于恰好是能够同时与多个近程设备进行通信的 NFP 提供程序，存在事件应为所有存在的聚合。 如果提供程序支持 0 到 N 同时近程设备，仅根据从 0 到 1 和 1 到 0 当前近程设备转换提供事件。 请注意，NFC 不支持此。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[邻近 DDI 引用附近](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  

