---
title: 获取上下文
description: 获取上下文
ms.assetid: e0e659e5-6f95-4378-8764-63d96c7d07d4
keywords:
- 上下文 WDK 文件系统微筛选器，获取
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f644c53e895b7283e1cc72c8ec66a06b9e0c4ea6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365897"
---
# <a name="getting-contexts"></a>获取上下文


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


一旦微筛选器驱动程序已设置的对象上下文，它可以通过调用获取上下文**FltGet***Xxx***上下文**，其中*Xxx*是上下文类型。

在下面的代码示例摘自 SwapBuffers 示例微筛选器驱动程序，微筛选器驱动程序将调用[ **FltGetVolumeContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltgetvolumecontext)获取卷上下文：

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

如果在调用[**FltGetVolumeContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltgetvolumecontext) θ *上下文*参数接收调用方的卷上下文的地址。 **FltGetVolumeContext**的引用计数的增量*上下文*指针。 因此，当不再需要此指针时，微筛选器驱动程序必须将其释放通过调用[ **FltReleaseContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltreleasecontext)。

 

 




