---
title: 传播 DO_BUFFERED_IO 和 DO_DIRECT_IO 标志
description: 传播 DO_BUFFERED_IO 和 DO_DIRECT_IO 标志
keywords:
- 筛选器驱动程序 WDK 文件系统，附加筛选器
- 文件系统筛选器驱动程序 WDK，附加筛选器
- 将筛选器附加到文件系统或卷
- 卷 WDK 文件系统，附加筛选器
- DO_BUFFERED_IO
- 传播 DO_BUFFERED_IO 标志
- DO_DIRECT_IO
- 传播 DO_DIRECT_IO 标志
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe5c5f2dca6cdbde8700a3d91a5b464dc41e20fa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838607"
---
# <a name="propagating-the-do_buffered_io-and-do_direct_io-flags"></a>传播执行 \_ 缓冲 \_ IO 和执行 \_ 直接 \_ IO 标志


## <span id="ddk_propagating_the_do_buffered_io_and_do_direct_io_flags_if"></span><span id="DDK_PROPAGATING_THE_DO_BUFFERED_IO_AND_DO_DIRECT_IO_FLAGS_IF"></span>


将筛选器设备对象附加到文件系统或卷后，请始终确保设置或清除 "执行 \_ 缓冲 \_ io"，并 \_ \_ 根据需要执行直接 IO 标记，使其与驱动程序堆栈上的下一个较低设备对象的值匹配。  (有关这些标志的详细信息，请参阅 [访问数据缓冲区的方法](../kernel/methods-for-accessing-data-buffers.md)。 ) 的示例如下：

```cpp
if (FlagOn( DeviceObject->Flags, DO_BUFFERED_IO )) {
    SetFlag( myLegacyFilterDeviceObject->Flags, DO_BUFFERED_IO );
}
if (FlagOn( DeviceObject->Flags, DO_DIRECT_IO )) {
    SetFlag(myLegacyFilterDeviceObject->Flags, DO_DIRECT_IO );
}
```

在上面的代码片段中， *DeviceObject* 是指向刚附加了筛选设备对象的设备对象的指针;myLegacyFilter *DeviceObject* 是一个指针，指向筛选器设备对象本身。

 

