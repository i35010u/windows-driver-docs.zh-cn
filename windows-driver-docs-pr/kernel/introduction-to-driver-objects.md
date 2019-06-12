---
title: 驱动程序对象简介
description: 驱动程序对象简介
ms.assetid: 497ee2dc-671d-408e-b228-16dc24532375
keywords:
- 驱动程序 WDK 内核对象
- 标准驱动程序例程 WDK 内核，驱动程序对象
- 驱动程序例程 WDK 内核，驱动程序对象
- 例程 WDK 内核，驱动程序对象
- 对象 WDK 驱动程序对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc774035d74293006a46c5f1abdb910391abaa56
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341024"
---
# <a name="introduction-to-driver-objects"></a>驱动程序对象简介


## <a href="" id="ddk-introduction-to-driver-objects-kg"></a>


I/O 管理器创建*驱动程序对象*每个驱动程序已安装并加载。 使用定义驱动程序对象[**驱动程序\_对象**](https://msdn.microsoft.com/library/windows/hardware/ff544174)结构。

当 I/O 管理器调用的驱动程序[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程，则它会提供驱动程序的驱动程序对象的地址。 驱动程序对象包含对多个驱动程序的标准例程的入口点的存储。 该驱动程序负责填写这些入口点。

## <a href="" id="driver-object-illustration"></a>


下图说明了具有的系统定义的标准例程的最低级别和更高级别的驱动程序可以或必须具有组的驱动程序对象。

每个标准例程使用其名称旁边的星号作为输入接收的 I/O 请求数据包 (IRP)。 每个标准例程还会收到指向 I/O 请求的目标设备对象的指针。

![说明驱动程序对象的关系图](images/24drvobj.png)

I/O 管理器定义的驱动程序对象类型，并使用驱动程序对象来注册并跟踪有关加载的映像的驱动程序的信息。 请注意，调度入口点 ( **DDDispatch * * * Xxx*通过**DDDispatch * **Yyy*) 中的驱动程序对象相对应的主要功能代码 (** IRP\_MJ\_* XXX * * *) 在 I/O 堆栈位置的 Irp 传递。

I/O 管理器首先将每个 IRP 传送给驱动程序所提供的调度例程。 最低级别驱动程序的调度例程通常调用 I/O 支持例程 ([**IoStartPacket**](https://msdn.microsoft.com/library/windows/hardware/ff550370)) 来排队 （或传递） 具有有效的参数，驱动程序的每个 IRP [ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)例程。 *StartIo*例程启动特定设备上请求的 I/O 操作。 更高级别的驱动程序通常不具有*StartIo*例程，但它们可以。

 

 




