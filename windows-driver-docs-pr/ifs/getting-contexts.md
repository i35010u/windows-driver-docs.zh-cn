---
title: 获取上下文
description: 获取上下文
ms.assetid: e0e659e5-6f95-4378-8764-63d96c7d07d4
keywords:
- 上下文 WDK 文件系统微筛选器，获取
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b9c17b94974189899b796ec8aac72249b646f00
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370335"
---
# <a name="getting-contexts"></a>获取上下文


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


一旦微筛选器驱动程序已设置的对象上下文，它可以通过调用获取上下文**FltGet***Xxx***上下文**，其中*Xxx*是上下文类型。

在下面的代码示例摘自 SwapBuffers 示例微筛选器驱动程序，微筛选器驱动程序将调用[ **FltGetVolumeContext** ](https://msdn.microsoft.com/library/windows/hardware/ff543189)获取卷上下文：

```cpp
status = FltGetVolumeContext(
 FltObjects->Filter,    //Filter
 FltObjects->Volume,    //Volume
                &volCtx);              //Context
...
if (volCtx != NULL) {
 FltReleaseContext(volCtx);
}
```

如果在调用[**FltGetVolumeContext** ](https://msdn.microsoft.com/library/windows/hardware/ff543189) θ *上下文*参数接收调用方的卷上下文的地址。 **FltGetVolumeContext**的引用计数的增量*上下文*指针。 因此，当不再需要此指针时，微筛选器驱动程序必须将其释放通过调用[ **FltReleaseContext**](https://msdn.microsoft.com/library/windows/hardware/ff544314)。

 

 




