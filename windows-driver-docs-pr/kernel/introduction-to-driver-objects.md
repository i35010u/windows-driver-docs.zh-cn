---
title: 驱动程序对象简介
description: 驱动程序对象简介
ms.assetid: 497ee2dc-671d-408e-b228-16dc24532375
keywords:
- 驱动对象 WDK 内核
- 标准驱动程序例程 WDK 内核，驱动程序对象
- 驱动程序例程 WDK 内核，驱动程序对象
- 例程的 WDK 内核，驱动程序对象
- 对象 WDK 驱动程序对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5736566d6b407690ceea71b2d7d78a92cff7bc2c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838630"
---
# <a name="introduction-to-driver-objects"></a>驱动程序对象简介


## <a href="" id="ddk-introduction-to-driver-objects-kg"></a>


I/o 管理器为每个已安装和加载的驱动程序创建一个*驱动程序对象*。 驱动程序对象是使用[**驱动\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_driver_object)结构来定义的。

当 i/o 管理器调用驱动程序的[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程时，它将提供驱动程序的驱动程序对象的地址。 驱动程序对象包含多个驱动程序标准例程的入口点的存储区。 驱动程序负责填写这些入口点。

## <a href="" id="driver-object-illustration"></a>


下图说明了一个驱动程序对象，其中包含最低级别和更高级别的驱动程序可以或必须具有的系统定义标准例程集。

名称旁边带有星号的每个标准例程接收 i/o 请求数据包（IRP）作为输入。 每个标准例程还会接收指向 i/o 请求的目标设备对象的指针。

![阐释驱动程序对象的关系图](images/24drvobj.png)

I/o 管理器定义驱动程序对象类型并使用驱动程序对象来注册和跟踪有关已加载映像的驱动程序的信息。 请注意，驱动程序对象中的调度入口点（ **DDDispatch * * * Xxx*到**DDDispatch * **Yyy*）对应于传递到**的 i/o 堆栈位置的主要函数代码（IRP\_MJ\_* Xxx * * *）Irp.

I/o 管理器首先将每个 IRP 路由到驱动程序提供的调度例程。 最低级别驱动程序的调度例程通常会调用 i/o 支持例程（[**IoStartPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartpacket)）将具有有效参数的每个 IRP 排队（或传递）到驱动程序的[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)例程。 *StartIo*例程在特定设备上启动请求的 i/o 操作。 较高级别的驱动程序通常不具有*StartIo*例程，但也可以。

 

 




