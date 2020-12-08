---
title: 注册快速 I/O 调度例程
description: 注册快速 I/O 调度例程
keywords:
- 注册快速 i/o 调度例程
- 调度例程 WDK 文件系统
- 快速 i/o 调度例程 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0008f86f07598844e2df98014f567a0e54da7eb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829653"
---
# <a name="registering-fast-io-dispatch-routines"></a>注册快速 I/O 调度例程


## <span id="ddk_registering_fast_io_dispatch_routines_if"></span><span id="DDK_REGISTERING_FAST_IO_DISPATCH_ROUTINES_IF"></span>


筛选器驱动程序的 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程的 *DriverObject* 参数提供一个指针，指向筛选器驱动 [**程序的驱动程序对象**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_driver_object)。

若要注册文件系统筛选器驱动程序的快速 i/o 调度例程，必须分配和初始化快速 i/o 调度表，将快速 i/o 调度例程的入口点存储到表中，并将表的地址存储在驱动程序对象的 **FastIoDispatch** 成员中。

例如，假设的 "MyLegacyFilter" 驱动程序可以为其快速 i/o 调度例程设置入口点，如下所示：

```cpp
RtlZeroMemory(fastIoDispatch, sizeof(FAST_IO_DISPATCH));
fastIoDispatch->SizeOfFastIoDispatch = sizeof(FAST_IO_DISPATCH);
fastIoDispatch->FastIoCheckIfPossible = MyLegacyFilterIoCheckIfPossible;
fastIoDispatch->FastIoRead = MyLegacyFilterIoRead;
fastIoDispatch->FastIoWrite = MyLegacyFilterIoWrite;
fastIoDispatch->FastIoQueryBasicInfo = MyLegacyFilterIoQueryBasicInfo;
fastIoDispatch->FastIoQueryStandardInfo = MyLegacyFilterIoQueryStandardInfo;
fastIoDispatch->FastIoLock = MyLegacyFilterIoLock;
fastIoDispatch->FastIoUnlockSingle = MyLegacyFilterIoUnlockSingle;
fastIoDispatch->FastIoUnlockAll = MyLegacyFilterIoUnlockAll;
fastIoDispatch->FastIoUnlockAllByKey = MyLegacyFilterIoUnlockAllByKey;
fastIoDispatch->FastIoDeviceControl = MyLegacyFilterIoDeviceControl;
fastIoDispatch->FastIoDetachDevice = MyLegacyFilterIoDetachDevice;
fastIoDispatch->FastIoQueryNetworkOpenInfo = MyLegacyFilterIoQueryNetworkOpenInfo;
fastIoDispatch->MdlRead = MyLegacyFilterIoMdlRead;
fastIoDispatch->MdlReadComplete = MyLegacyFilterIoMdlReadComplete;
fastIoDispatch->PrepareMdlWrite = MyLegacyFilterIoPrepareMdlWrite;
fastIoDispatch->MdlWriteComplete = MyLegacyFilterIoMdlWriteComplete;
fastIoDispatch->FastIoReadCompressed = MyLegacyFilterIoReadCompressed;
fastIoDispatch->FastIoWriteCompressed = MyLegacyFilterIoWriteCompressed;
fastIoDispatch->MdlReadCompleteCompressed = MyLegacyFilterIoMdlReadCompleteCompressed;
fastIoDispatch->MdlWriteCompleteCompressed = MyLegacyFilterIoMdlWriteCompleteCompressed;
fastIoDispatch->FastIoQueryOpen = MyLegacyFilterIoQueryOpen;

DriverObject->FastIoDispatch = fastIoDispatch;
```

 

