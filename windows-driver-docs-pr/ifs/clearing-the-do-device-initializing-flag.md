---
title: 清除 DO_DEVICE_INITIALIZING 标志
description: 清除 DO_DEVICE_INITIALIZING 标志
ms.assetid: 1c1cca60-bb95-4a8d-9e17-4db54983bbb0
keywords:
- 筛选器驱动程序 WDK 文件系统，将附加筛选器
- 文件系统筛选器驱动程序 WDK，附加筛选器
- 附加到文件系统卷的筛选器
- WDK 卷文件系统，将附加筛选器
- DO_DEVICE_INITIALIZING
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5bcd78c2ea07d6bd5550cada1c16b158ef062d75
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378999"
---
# <a name="clearing-the-dodeviceinitializing-flag"></a>清除 DO\_设备\_正在初始化标志


## <span id="ddk_clearing_the_do_device_initializing_flag_if"></span><span id="DDK_CLEARING_THE_DO_DEVICE_INITIALIZING_FLAG_IF"></span>


之后将筛选设备对象附加到文件系统或卷，始终为确保清除 DO\_设备\_筛选设备对象上的正在初始化标志。 (有关此标志的详细信息，请参阅[**设备\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_object)内核引用中。)这可以按如下所示使用**ClearFlag**中定义的宏*ntifs.h*:

```cpp
ClearFlag(NewDeviceObject->Flags, DO_DEVICE_INITIALIZING);
```

创建筛选器设备对象后， [ **IoCreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatedevice)设置执行\_设备\_正在初始化标志上的设备对象。 已成功附加筛选器后，必须清除此标志。 请注意，是否不清除此标志，则没有更多的筛选器驱动程序可以将附加到筛选器链因为对[ **IoAttachDeviceToDeviceStackSafe** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioattachdevicetodevicestacksafe)将失败。

**请注意**  不需要清除 DO\_设备\_正在初始化创建 DriverEntry，因为这自动完成的 I/O 管理器的设备对象上的标志。 但是，您的驱动程序应清除它创建的所有其他设备对象上的此标志。

 

 

 




