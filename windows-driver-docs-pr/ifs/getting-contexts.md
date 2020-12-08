---
title: 获取上下文
description: 获取上下文
keywords:
- 上下文 WDK 文件系统微筛选器，获取
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b75c2db99543bf8bf913abca46130be362500728
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821467"
---
# <a name="getting-contexts"></a>获取上下文


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


微筛选器驱动程序设置对象的上下文后，它可以通过调用 **FltGet**_xxx_*_上下文_* 获取上下文，其中 *xxx* 是上下文类型。

在以下代码示例中，从 SwapBuffers 示例微筛选器驱动程序开始，微筛选器驱动程序调用 [**FltGetVolumeContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetvolumecontext) 来获取卷上下文：

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

如果对 [**FltGetVolumeContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetvolumecontext) 的调用成功， *上下文* 参数将接收调用方的卷上下文的地址。 **FltGetVolumeContext** 在 *上下文* 指针上递增引用计数。 因此，当不再需要此指针时，微筛选器驱动程序必须通过调用 [**FltReleaseContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreleasecontext)来释放它。

 

