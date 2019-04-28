---
title: 生成和发送 BRB
description: 生成和发送 BRB
ms.assetid: 53a692e7-9c71-4dca-9331-32ac97b94179
keywords:
- 蓝牙 WDK、 蓝牙请求块
- BRBs WDK
- 蓝牙 WDK，请求块
- 发送 BRBs
- 返回值 WDK 蓝牙
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03c883b19f878fd37a636282eb1d512eb98c3972
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328248"
---
# <a name="building-and-sending-a-brb"></a>生成和发送 BRB


以下过程概述了为了生成并发送蓝牙请求块 (BRB) 配置文件驱动程序遵循的一般过程。 BRB 是描述要执行的蓝牙操作数据的块。

### <a name="span-idtobuildandsendabrbspanspan-idtobuildandsendabrbspanto-build-and-send-a-brb"></a><span id="to_build_and_send_a_brb"></span><span id="TO_BUILD_AND_SEND_A_BRB"></span>若要生成并发送 BRB

1.  分配 IRP。 有关如何使用 Irp 的详细信息，请参阅[处理 Irp](https://msdn.microsoft.com/library/windows/hardware/ff546847)。

2.  分配 BRB。 若要分配 BRBs，调用[ **BthAllocateBrb** ](https://msdn.microsoft.com/library/windows/hardware/ff536634)按配置文件驱动程序用于将导出的蓝牙驱动程序堆栈的函数。 若要获取的指针*BthAllocateBrb*函数中，请参阅[蓝牙接口查询](querying-for-bluetooth-interfaces.md)。

3.  初始化 BRB 参数。 每个 BRB 使用相应的结构。 设置根据预期用途结构的成员。 BRBs 和其相应结构的列表，请参阅[使用蓝牙驱动程序堆栈](using-the-bluetooth-driver-stack.md)。

4.  初始化 IRP 的参数。 设置**MajorFunction** IRP 到 IRP 的成员\_MJ\_内部\_设备\_控件。 设置**Parameters.DeviceIoControl.IoControlCode**成员添加到 IOCTL\_内部\_同时为\_提交\_BRB。 设置**Parameters.Others.Argument1**成员以指向 BRB。

5.  将驱动程序堆栈的下层 IRP 传递。 调用[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)以将 IRP 发送到下一步低驱动程序。

下面的伪代码示例演示如何设置要处理的蓝牙驱动程序堆栈 L2CAP Ping BRB。

**请注意**  以提高可读性，下面的伪代码示例并不演示错误处理。

 

```cpp
#include <bthddi.h>

// Code for obtaining the BthInterface pointer

// Define a custom pool tag to identify your profile driver's dynamic memory allocations.
// You should change this tag to easily identify your driver's allocations from other drivers.
#define PROFILE_DRIVER_POOL_TAG '_htB'

PIRP Irp;
Irp = IoAllocateIrp( DeviceExtension->ParentDeviceObject->StackSize, FALSE );

PBRB_L2CA_PING BrbPing; // Define storage for a L2CAP Ping BRB

// Allocate the Ping BRB
BrbPing = BthInterface->BthAllocateBrb( BRB_L2CA_PING, PROFILE_DRIVER_POOL_TAG );

// Set up the next IRP stack location
PIO_STACK_LOCATION NextIrpStack;
NextIrpStack = IoGetNextIrpStackLocation( Irp );
NextIrpStack->MajorFunction = IRP_MJ_INTERNAL_DEVICE_CONTROL;
NextIrpStack->Parameters.DeviceIoControl.IoControlCode = IOCTL_INTERNAL_BTH_SUBMIT_BRB;
NextIrpStack->Parameters.Others.Argument1 = BrbPing;

// Pass the IRP down the driver stack
NTSTATUS Status;
Status = IoCallDriver( DeviceExtension->NextLowerDriver, Irp );
```

 

 





