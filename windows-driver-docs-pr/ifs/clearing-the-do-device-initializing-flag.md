---
title: 清除 DO_DEVICE_INITIALIZING 标志
description: 清除 DO_DEVICE_INITIALIZING 标志
ms.assetid: 1c1cca60-bb95-4a8d-9e17-4db54983bbb0
keywords:
- 筛选器驱动程序 WDK 文件系统，附加筛选器
- 文件系统筛选器驱动程序 WDK，附加筛选器
- 将筛选器附加到文件系统或卷
- 卷 WDK 文件系统，附加筛选器
- DO_DEVICE_INITIALIZING
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: acb85c2c7a922dd0e06ac8b6ef363a7a29183c03
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841472"
---
# <a name="clearing-the-do_device_initializing-flag"></a>清除 DO\_设备\_初始化标志


## <span id="ddk_clearing_the_do_device_initializing_flag_if"></span><span id="DDK_CLEARING_THE_DO_DEVICE_INITIALIZING_FLAG_IF"></span>


将筛选器设备对象附加到文件系统或卷后，请始终确保清除筛选器设备对象上的 DO\_设备\_初始化标志。 （有关此标志的详细信息，请参阅内核参考中的[**设备\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)。）可以使用*ntifs*中定义的**ClearFlag**宏来完成此操作：

```cpp
ClearFlag(NewDeviceObject->Flags, DO_DEVICE_INITIALIZING);
```

创建筛选器设备对象时， [**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)会在设备对象上设置 DO\_设备\_初始化标志。 成功附加筛选器后，必须清除此标志。 请注意，如果未清除此标志，则无法再附加筛选器驱动程序，因为对[**IoAttachDeviceToDeviceStackSafe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioattachdevicetodevicestacksafe)的调用将失败。

**请注意**   不需要清除在 DriverEntry 中创建的设备对象上的 "执行\_设备\_初始化" 标志，因为这是由 I/o 管理器自动完成的。 但是，驱动程序应该清除它创建的所有其他设备对象上的此标志。

 

 

 




