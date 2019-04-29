---
title: 编写 ControllerControl 例程
description: 编写 ControllerControl 例程
ms.assetid: 9330e0ff-c4bb-4aa6-985e-ef89791f74df
keywords:
- 控制器对象 WDK 内核，编写 ControllerControl 例程
- ControllerControl 例程编写
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcec280f64accb304c28a3b0eee798b30f99d235
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355997"
---
# <a name="writing-controllercontrol-routines"></a>编写 ControllerControl 例程





使用控制器对象的驱动程序必须提供[ *ControllerControl* ](https://msdn.microsoft.com/library/windows/hardware/ff542049)例程，以启动 I/O 操作。

必须同步的操作，通过物理控制器，例如"AT"磁盘控制器、 到类似的设备的最低级别的设备驱动程序可以具有*ControllerControl*例程。

当驱动程序调用[ **IoAllocateController**](https://msdn.microsoft.com/library/windows/hardware/ff548224)，将其*ControllerControl*如果硬件由控制器对象可立即运行时例程对于 I/O 操作。 否则为*ControllerControl*例程会排队，直到该控制器是免费的。

**请注意**  WDM 驱动程序不能使用控制器对象和*ControllerControl*例程。

 

 

 




