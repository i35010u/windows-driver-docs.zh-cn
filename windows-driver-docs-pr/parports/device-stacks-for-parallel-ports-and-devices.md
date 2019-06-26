---
title: 并行端口和设备的设备堆栈
description: 并行端口和设备的设备堆栈
ms.assetid: 80222ed9-f900-4d97-b459-2d8ca780e1d1
keywords:
- 系统提供并行驱动程序 WDK，设备堆栈
- 设备堆栈 WDK 并行驱动程序
- 并行设备 WDK，设备堆栈
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ec93a7c51fef316270e256b381e2ec20916ee4a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376965"
---
# <a name="device-stacks-for-parallel-ports-and-devices"></a>并行端口和设备的设备堆栈





本部分介绍由系统提供并行和驱动程序的并行端口连接到并行端口的设备创建设备堆栈。

下图显示了系统提供的并行驱动程序的并行端口和并行端口连接的设备创建设备堆栈的类型。

![说明并行端口和设备的 windows 设备和驱动程序堆栈的关系图](images/parport4.png)

供应商提供的函数的并行连接到并行端口的设备的驱动程序是可选的。 系统提供的并行驱动程序提供广泛支持用于直接控制并行设备为原始的设备，以及用于控制设备的父并行端口。

有关如何运行的并行端口和与并行端口连接的设备的详细信息，请参阅：

[并行设备接口、 内部名称和符号链接](parallel-device-interfaces--internal-names--and-symbolic-links.md)

[IOCTL 和并行端口和设备的回调支持](ioctl-and-callback-support-for-parallel-ports-and-devices.md)

[运行并行端口](operating-a-parallel-port.md)

[运行并行设备附加到并行端口](operating-a-parallel-device-attached-to-a-parallel-port.md)

[系统提供并行的驱动程序的客户端接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

 

 




