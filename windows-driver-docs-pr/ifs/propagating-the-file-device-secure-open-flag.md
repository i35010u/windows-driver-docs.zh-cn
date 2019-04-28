---
title: 传播 FILE_DEVICE_SECURE_OPEN 标志
description: 传播 FILE_DEVICE_SECURE_OPEN 标志
ms.assetid: cbc254ab-3ac6-44aa-bb16-16d701d5ada7
keywords:
- 筛选器驱动程序 WDK 文件系统，将附加筛选器
- 文件系统筛选器驱动程序 WDK，附加筛选器
- 附加到文件系统卷的筛选器
- WDK 卷文件系统，将附加筛选器
- FILE_DEVICE_SECURE_OPEN
- 传播 FILE_DEVICE_SECURE_OPEN 标志
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea027f7b7eef6b90c9e7bb1ed8e16e9704197e73
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352749"
---
# <a name="propagating-the-filedevicesecureopen-flag"></a>传播文件\_设备\_SECURE\_打开标志


## <span id="ddk_clearing_the_do_device_initializing_flag_if"></span><span id="DDK_CLEARING_THE_DO_DEVICE_INITIALIZING_FLAG_IF"></span>


附加后筛选设备对象到文件系统中 （但不是到的卷），务必将文件设置\_设备\_SECURE\_打开标志，使其匹配的下一步越低值到所需的筛选器设备对象设备驱动程序堆栈上的对象。 (有关此标志的详细信息，请参阅[指定设备特征](https://msdn.microsoft.com/library/windows/hardware/ff563818)内核体系结构设计指南中并[**设备\_对象**](https://msdn.microsoft.com/library/windows/hardware/ff543147)中内核参考。）此示例如下：

```cpp
if (FlagOn( DeviceObject->Characteristics, FILE_DEVICE_SECURE_OPEN )) {
    SetFlag(myLegacyFilterDeviceObject->Characteristics, FILE_DEVICE_SECURE_OPEN );
}
```

在上面的代码段*DeviceObject*是指向到的设备对象的筛选设备对象只是已附加; myLegacyFilter *DeviceObject*指向筛选设备对象的指针本身。

 

 




