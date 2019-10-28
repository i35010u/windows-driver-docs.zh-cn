---
title: 传播 FILE_DEVICE_SECURE_OPEN 标志
description: 传播 FILE_DEVICE_SECURE_OPEN 标志
ms.assetid: cbc254ab-3ac6-44aa-bb16-16d701d5ada7
keywords:
- 筛选器驱动程序 WDK 文件系统，附加筛选器
- 文件系统筛选器驱动程序 WDK，附加筛选器
- 将筛选器附加到文件系统或卷
- 卷 WDK 文件系统，附加筛选器
- FILE_DEVICE_SECURE_OPEN
- 传播 FILE_DEVICE_SECURE_OPEN 标志
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 461d9dcd3394106f949699e8ff6d6871ed287aba
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841020"
---
# <a name="propagating-the-file_device_secure_open-flag"></a>\_SECURE\_打开标志\_设备传播文件


## <span id="ddk_clearing_the_do_device_initializing_flag_if"></span><span id="DDK_CLEARING_THE_DO_DEVICE_INITIALIZING_FLAG_IF"></span>


将筛选器设备对象附加到文件系统（但不是卷）后，请始终确保将文件\_设备设置为在筛选器设备对象上\_SECURE\_打开标志，使其与驱动程序堆栈。 （有关此标志的详细信息，请参阅内核体系结构设计指南中的[指定设备特征](https://docs.microsoft.com/windows-hardware/drivers/kernel/specifying-device-characteristics)和内核参考中的[**设备\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)。）下面是一个示例：

```cpp
if (FlagOn( DeviceObject->Characteristics, FILE_DEVICE_SECURE_OPEN )) {
    SetFlag(myLegacyFilterDeviceObject->Characteristics, FILE_DEVICE_SECURE_OPEN );
}
```

在上面的代码片段中， *DeviceObject*是指向刚附加了筛选设备对象的设备对象的指针;myLegacyFilter *DeviceObject*是一个指针，指向筛选器设备对象本身。

 

 




