---
title: 传播 DO_BUFFERED_IO 和 DO_DIRECT_IO 标志
description: 传播 DO_BUFFERED_IO 和 DO_DIRECT_IO 标志
ms.assetid: a0cb4f1a-3c27-4608-a208-ffcf4113b722
keywords:
- 筛选器驱动程序 WDK 文件系统，将附加筛选器
- 文件系统筛选器驱动程序 WDK，附加筛选器
- 附加到文件系统卷的筛选器
- WDK 卷文件系统，将附加筛选器
- DO_BUFFERED_IO
- 传播 DO_BUFFERED_IO 标志
- DO_DIRECT_IO
- 传播 DO_DIRECT_IO 标志
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6eb99205772be342a2c5ac0ddd592919d1affde7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541929"
---
# <a name="propagating-the-dobufferedio-and-dodirectio-flags"></a>传播 DO\_缓冲\_IO 和 DO\_直接\_IO 标志


## <span id="ddk_propagating_the_do_buffered_io_and_do_direct_io_flags_if"></span><span id="DDK_PROPAGATING_THE_DO_BUFFERED_IO_AND_DO_DIRECT_IO_FLAGS_IF"></span>


在后将筛选设备对象附加到文件系统或卷，始终请务必设置或清除执行\_缓冲\_IO 并执行\_直接\_IO 标志根据需要使其与下一步低设备的值驱动程序堆栈的对象。 (有关这些标志的详细信息，请参阅[方法的访问数据缓冲区](https://msdn.microsoft.com/library/windows/hardware/ff554436)。)此示例如下：

```cpp
if (FlagOn( DeviceObject->Flags, DO_BUFFERED_IO )) {
    SetFlag( myLegacyFilterDeviceObject->Flags, DO_BUFFERED_IO );
}
if (FlagOn( DeviceObject->Flags, DO_DIRECT_IO )) {
    SetFlag(myLegacyFilterDeviceObject->Flags, DO_DIRECT_IO );
}
```

在上面的代码段*DeviceObject*是指向到的设备对象的筛选设备对象只是已附加; myLegacyFilter *DeviceObject*指向筛选设备对象的指针本身。

 

 




