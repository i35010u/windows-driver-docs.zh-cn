---
title: 传播 FILE_DEVICE_SECURE_OPEN 标志
description: 传播 FILE_DEVICE_SECURE_OPEN 标志
keywords:
- 筛选器驱动程序 WDK 文件系统，附加筛选器
- 文件系统筛选器驱动程序 WDK，附加筛选器
- 将筛选器附加到文件系统或卷
- 卷 WDK 文件系统，附加筛选器
- FILE_DEVICE_SECURE_OPEN
- 传播 FILE_DEVICE_SECURE_OPEN 标志
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1baa66dade8800e4b3372ed0d7f06a2423ccece8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838605"
---
# <a name="propagating-the-file_device_secure_open-flag"></a>传播文件 \_ 设备 \_ 安全 \_ 打开标志


## <span id="ddk_clearing_the_do_device_initializing_flag_if"></span><span id="DDK_CLEARING_THE_DO_DEVICE_INITIALIZING_FLAG_IF"></span>


将筛选器设备对象连接到文件系统 (但不能连接到卷) 后，请始终确保 \_ \_ \_ 根据需要在筛选器设备对象上设置文件设备安全打开标志，使其与驱动程序堆栈上下一个较低设备对象的值相匹配。  (有关此标志的详细信息，请参阅内核参考中的 "内核体系结构设计指南" 和 "[**设备 \_ 对象**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)" 中的 [指定设备特征](../kernel/specifying-device-characteristics.md)。 ) 的示例如下：

```cpp
if (FlagOn( DeviceObject->Characteristics, FILE_DEVICE_SECURE_OPEN )) {
    SetFlag(myLegacyFilterDeviceObject->Characteristics, FILE_DEVICE_SECURE_OPEN );
}
```

在上面的代码片段中， *DeviceObject* 是指向刚附加了筛选设备对象的设备对象的指针;myLegacyFilter *DeviceObject* 是一个指针，指向筛选器设备对象本身。

 

