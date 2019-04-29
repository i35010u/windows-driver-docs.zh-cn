---
title: 通过总线驱动程序进行的设备通信
description: 通过总线驱动程序进行的设备通信
ms.assetid: 093e95db-dc3e-467b-9163-e61d793c042e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0670f10de09ebd9d6c9fc13ab0b07163b61cba48
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364576"
---
# <a name="device-communication-through-the-bus-driver"></a>通过总线驱动程序进行的设备通信





WIA 微型驱动程序的主要职责是与设备通信。 当 WIA 应用程序到 WIA 服务的调用时，该请求转发到 WIA 微型驱动程序的接口，通过[IStiUSD](istiusd-com-interface.md)或[IWiaMiniDrv](https://msdn.microsoft.com/library/windows/hardware/ff545027)接口。 在某些情况下，WIA 微型驱动程序必须查询物理设备或在设备上执行一些其他操作。 微型驱动程序的设备通信层负责将从 WIA 服务请求转换为设备可以理解的请求，然后将请求发送总线驱动程序堆栈通过向设备。 同样，如果设备发送其响应备份总线驱动程序堆栈，设备通信层将负责将来自设备的响应转换成 WIA 服务可以理解的响应。

与总线驱动程序堆栈的所有通信都都通过调用[ **CreateFile**](https://msdn.microsoft.com/library/windows/desktop/aa363858)， **ReadFile**， **WriteFile**，和**DeviceIoControl**函数，Microsoft Windows SDK 文档中所述。 有关与总线驱动程序堆栈进行通信的详细信息，请参阅[访问内核模式设备驱动程序仍映像](accessing-kernel-mode-drivers-for-still-image-devices.md)。

 

 




