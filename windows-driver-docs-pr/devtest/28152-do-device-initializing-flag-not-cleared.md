---
title: C28152
description: 警告 C28152 从类似 AddDevice 的函数返回意外 DO_DEVICE_INITIALIZING。
ms.assetid: df2b68dc-b22b-4aaa-b1ba-b34bfdd9b886
keywords:
- 警告列出 WDK PREfast for Drivers
- 错误列出 WDK PREfast for Drivers
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28152
ms.openlocfilehash: 2604f9b5ead9eab0fc17d9e8e9897929d295491b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364110"
---
# <a name="c28152"></a>C28152


警告 C28152:从类似 AddDevice 的函数返回意外执行\_设备\_正在初始化

该驱动程序已经从返回其**AddDevice**例程或类似的实用程序例程，但**做\_设备\_正在初始化**位**标志**word (**DeviceObject-&gt;标志**) 中**DeviceObject**例程不会被清除。

**AddDevice**例程必须包含类似于下面的代码以清除**做\_设备\_正在初始化**标志。

```
FunctionalDeviceObject->Flags &= ~DO_DEVICE_INITIALIZING;
```

有关详细信息**AddDevice**例程，请参阅[AddDevice 例程在函数或筛选器驱动程序](https://docs.microsoft.com/windows-hardware/drivers/kernel/adddevice-routines-in-function-or-filter-drivers)

 

 





