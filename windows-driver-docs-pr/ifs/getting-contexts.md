---
title: 获取上下文
description: 获取上下文
ms.assetid: e0e659e5-6f95-4378-8764-63d96c7d07d4
keywords:
- 上下文 WDK 文件系统微筛选器，获取
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65b5d74ddda725c48621620076973e2550ea0277
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841228"
---
# <a name="getting-contexts"></a>获取上下文


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


微筛选器驱动程序设置对象的上下文后，它可以通过调用**FltGet***xxx***上下文**获取上下文，其中*xxx*是上下文类型。

在以下代码示例中，从 SwapBuffers 示例微筛选器驱动程序开始，微筛选器驱动程序调用[**FltGetVolumeContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetvolumecontext)来获取卷上下文：

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

如果对[**FltGetVolumeContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetvolumecontext)的调用成功，*上下文*参数将接收调用方的卷上下文的地址。 **FltGetVolumeContext**在*上下文*指针上递增引用计数。 因此，当不再需要此指针时，微筛选器驱动程序必须通过调用[**FltReleaseContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreleasecontext)来释放它。

 

 




