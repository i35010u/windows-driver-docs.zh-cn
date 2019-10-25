---
title: 并行端口和设备的设备堆栈
description: 并行端口和设备的设备堆栈
ms.assetid: 80222ed9-f900-4d97-b459-2d8ca780e1d1
keywords:
- 系统提供的并行驱动程序 WDK，设备堆栈
- 设备堆栈 WDK 并行驱动程序
- 并行设备 WDK，设备堆栈
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c07e3f97d17a71bce511c9fbcc2fb890d7deef4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831486"
---
# <a name="device-stacks-for-parallel-ports-and-devices"></a>并行端口和设备的设备堆栈





本部分介绍系统为并行端口和设备附加到并行端口的系统提供的并行驱动程序创建的设备堆栈。

下图显示了系统为并行端口和连接到并行端口的设备创建的并行驱动程序的设备堆栈类型。

![阐释并行端口和设备的 windows 设备和驱动程序堆栈的示意图](images/parport4.png)

附加到并行端口的供应商提供的并行设备的函数驱动程序是可选的。 系统提供的并行驱动程序广泛支持直接将并行设备控制为原始设备，并提供控制设备的父并行端口的支持。

有关如何操作连接到并行端口的并行端口和设备的详细信息，请参阅：

[并行设备接口、内部名称和符号链接](parallel-device-interfaces--internal-names--and-symbolic-links.md)

[并行端口和设备的 IOCTL 和回调支持](ioctl-and-callback-support-for-parallel-ports-and-devices.md)

[操作并行端口](operating-a-parallel-port.md)

[操作连接到并行端口的并行设备](operating-a-parallel-device-attached-to-a-parallel-port.md)

[系统提供的并行驱动程序的客户端接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

 

 




