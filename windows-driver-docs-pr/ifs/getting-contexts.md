---
title: 获取上下文
description: 获取上下文
ms.assetid: e0e659e5-6f95-4378-8764-63d96c7d07d4
keywords:
- 上下文 WDK 文件系统微筛选器，获取
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee24dfbc5311ca30bee4d57af3619447a72f3315
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066920"
---
# <a name="getting-contexts"></a>获取上下文


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


微筛选器驱动程序设置对象的上下文后，它可以通过调用 **FltGet***xxx***上下文**获取上下文，其中 *xxx* 是上下文类型。

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

 

