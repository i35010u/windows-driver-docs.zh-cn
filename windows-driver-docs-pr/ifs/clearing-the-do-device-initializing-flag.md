---
title: 清除 DO_DEVICE_INITIALIZING 标志
description: 清除 DO_DEVICE_INITIALIZING 标志
keywords:
- 筛选器驱动程序 WDK 文件系统，附加筛选器
- 文件系统筛选器驱动程序 WDK，附加筛选器
- 将筛选器附加到文件系统或卷
- 卷 WDK 文件系统，附加筛选器
- DO_DEVICE_INITIALIZING
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dfdcb3912368eeb6386a368807beb28356afeb1f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818447"
---
# <a name="clearing-the-do_device_initializing-flag"></a>清除 "执行 \_ 设备 \_ 初始化" 标志


## <span id="ddk_clearing_the_do_device_initializing_flag_if"></span><span id="DDK_CLEARING_THE_DO_DEVICE_INITIALIZING_FLAG_IF"></span>


将筛选器设备对象附加到文件系统或卷后，请始终确保清除 \_ \_ 筛选器设备对象上的 "执行设备初始化" 标志。  (有关此标志的详细信息，请参阅内核引用中的 [**设备 \_ 对象**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)。 ) 可以使用 *Ntifs* 中定义的 **ClearFlag** 宏来完成此操作：

```cpp
ClearFlag(NewDeviceObject->Flags, DO_DEVICE_INITIALIZING);
```

创建筛选器设备对象后， [**IoCreateDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice) 将在 \_ \_ 设备对象上设置 "对设备进行初始化" 标志。 成功附加筛选器后，必须清除此标志。 请注意，如果未清除此标志，则无法再附加筛选器驱动程序，因为对 [**IoAttachDeviceToDeviceStackSafe**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioattachdevicetodevicestacksafe) 的调用将失败。

**注意**   无需清除 \_ \_ 在 DriverEntry 中创建的设备对象上的 "执行设备初始化" 标志，因为这是由 I/o 管理器自动完成的。 但是，驱动程序应该清除它创建的所有其他设备对象上的此标志。

 

 

