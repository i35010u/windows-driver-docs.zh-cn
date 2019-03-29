---
title: 使用磁带类驱动程序
description: 使用磁带类驱动程序
ms.assetid: 72ed3fd9-d46f-400e-9816-f9f48b5a85c0
keywords:
- 磁带驱动程序 WDK 存储有关磁带驱动程序
- 存储磁带驱动程序 WDK，有关磁带驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a992634d000b1b152ce14649d3ba75da51053dc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569027"
---
# <a name="using-the-tape-class-driver"></a>使用磁带类驱动程序


## <span id="ddk_using_the_tape_class_driver_kg"></span><span id="DDK_USING_THE_TAPE_CLASS_DRIVER_KG"></span>


系统提供磁带类驱动程序实现独立于设备的、 特定于操作系统的磁带支持，并将导出特定于设备的磁带 miniclass 驱动程序的支持例程。

磁带类驱动程序：

-   初始化使用 miniclass 驱动程序提供特定于设备的信息的磁带 miniclass 驱动程序**DriverEntry**例程，包括分配并初始化 miniclass 驱动程序的操作系统资源和其支持的即插即用管理器从一个开始请求创建一个设备对象 (FDO) 来表示设备并将其附加到设备堆栈和启动设备的设备。

-   将导出内存分配和初始化例程。

-   拆分转移请求时可以根据最大传输大小内的 HBA。

-   处理 IRP\_MJ\_创建、 IRP\_MJ\_读取、 IRP\_MJ\_编写、 IRP\_MJ\_PNP 和 IRP\_MJ\_电源请求.

-   执行与设备无关的 IRP 预处理\_MJ\_设备\_控制请求并分派给磁带 miniclass 驱动程序中的相应特定于设备的例程。

-   分配 Srb 并将其发送到基础存储端口驱动程序后磁带 miniclass 驱动程序已填写 CDB 和任何其他适用于请求的 SRB 成员。

-   Windows NT 状态代码和磁带状态代码之间进行转换，提供了独立于设备的特定于磁带的错误处理，并且调用 miniclass 驱动程序的特定于设备的错误处理例程的磁带。

-   将驱动程序的上下文区域分配的磁带 miniclass 驱动程序 （minitape 扩展和扩展的命令）。

请参阅[磁带类驱动程序例程](https://msdn.microsoft.com/library/windows/hardware/ff567959)有关的说明 **TapeClass * * * Xxx*磁带 miniclass 驱动程序可以调用的例程。

 

 




