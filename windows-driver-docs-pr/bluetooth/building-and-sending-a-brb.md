---
title: 生成和发送 BRB
description: 生成和发送 BRB
ms.assetid: 53a692e7-9c71-4dca-9331-32ac97b94179
keywords:
- 蓝牙 WDK，蓝牙请求块
- BRBs WDK
- 蓝牙 WDK，请求块
- 发送 BRBs
- 返回值 WDK 蓝牙
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8adcba3e4028c18947d84eb7f586906493164da6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833874"
---
# <a name="building-and-sending-a-brb"></a>生成和发送 BRB


下面的过程概述了配置文件驱动程序用于构建和发送蓝牙请求块（BRB）的一般过程。 BRB 是描述要执行的蓝牙操作的数据块。

### <a name="span-idto_build_and_send_a_brbspanspan-idto_build_and_send_a_brbspanto-build-and-send-a-brb"></a><span id="to_build_and_send_a_brb"></span><span id="TO_BUILD_AND_SEND_A_BRB"></span>生成并发送 BRB

1.  分配 IRP。 有关如何使用 Irp 的详细信息，请参阅[处理 irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-irps)。

2.  分配 BRB。 若要分配 BRBs，请调用蓝牙驱动程序堆栈导出以供配置文件驱动程序使用的[**BthAllocateBrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnbth_allocate_brb)函数。 若要获取指向*BthAllocateBrb*函数的指针，请参阅[查询蓝牙接口](querying-for-bluetooth-interfaces.md)。

3.  初始化 BRB 的参数。 每个 BRB 都使用相应的结构。 根据预期用途设置结构的成员。 有关 BRBs 及其相应结构的列表，请参阅[使用蓝牙驱动程序堆栈](using-the-bluetooth-driver-stack.md)。

4.  初始化 IRP 的参数。 将 IRP 的**MajorFunction**成员设置为 IRP\_MJ\_内部\_设备\_控制。 将**DeviceIoControl. IoControlCode**成员设置为 IOCTL\_内部\_BTH\_提交\_BRB。 将**Argument1**成员设置为指向 BRB。

5.  将 IRP 向下传递驱动程序堆栈。 调用[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)将 IRP 发送到下一个较低版本的驱动程序。

下面的伪代码示例演示如何设置 L2CAP Ping BRB，以使蓝牙驱动程序堆栈进行处理。

  **请注意**，为了提高可读性，下面的伪代码示例不演示错误处理。

 

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

 

 





