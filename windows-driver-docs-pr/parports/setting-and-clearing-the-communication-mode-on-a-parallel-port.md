---
title: 设置和清除并行端口上的通信模式
description: 设置和清除并行端口上的通信模式
ms.assetid: a22cdeef-4ae7-49f8-b0b5-a4d68feb4235
keywords:
- 并行端口 WDK、 通信模式
- 通信模式 WDK 的并行端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be3891065f2b0d765be26f4ab3ed90fface720f9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380549"
---
# <a name="setting-and-clearing-the-communication-mode-on-a-parallel-port"></a>设置和清除并行端口上的通信模式





客户端使用以下内置设备控制请求并行端口上设置的通信模式：

[**IOCTL\_INTERNAL\_PARALLEL\_SET\_CHIP\_MODE**](https://msdn.microsoft.com/library/windows/hardware/ff544031)

[**IOCTL\_内部\_并行\_清除\_芯片\_模式**](https://msdn.microsoft.com/library/windows/hardware/ff544017)

内核模式驱动程序还可以使用系统提供[并行设备回调例程](https://msdn.microsoft.com/library/windows/hardware/ff544275)获得[ **IOCTL\_内部\_获取\_并行\_PNP\_INFO** ](https://msdn.microsoft.com/library/windows/hardware/ff543997)请求。 此请求将返回[**并行\_PNP\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff544299)结构，它包括以下指向系统提供的回调：

-   **TrySetChipMode**成员是指向[ *PPARALLEL\_设置\_芯片\_模式*](https://msdn.microsoft.com/library/windows/hardware/ff544542)回调，它设置的操作系统并行端口的模式。

-   **ClearChipMode**成员是指向[ *PPARALLEL\_清除\_芯片\_模式*](https://msdn.microsoft.com/library/windows/hardware/ff544398)回调，这会清除通过重置为 IEEE 1284 兼容性模式的主机芯片组的通信模式的并行端口的运行模式。

然后它可以设置或清除的通信模式，客户端必须首先分配并行端口。

它可以设置新的通信模式之前，客户端必须首先清除的通信模式。 清除的通信模式返回到 IEEE 1284 兼容性模式的主机芯片集确定。

若要确定当前的模式，客户端可以使用 IOCTL\_内部\_获取\_并行\_PNP\_信息请求，返回并行\_PNP\_信息结构，它包含有关当前的通信模式的信息。

 

 




