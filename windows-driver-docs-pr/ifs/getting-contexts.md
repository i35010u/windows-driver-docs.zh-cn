---
title: 获取上下文
description: 获取上下文
keywords:
- 上下文 WDK 文件系统微筛选器，获取
ms.date: 01/22/2021
ms.localizationpriority: medium
ms.openlocfilehash: e77e684ff0c0a06a73d190426b07d3ad31b3cb96
ms.sourcegitcommit: 204ed37ede1cd462ef6f6c9211a223fd304da4a5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2021
ms.locfileid: "99502050"
---
# <a name="getting-contexts"></a>获取上下文

微筛选器驱动程序 [设置对象的上下文](setting-contexts.md) 后，它可以通过调用以下 get 例程之一获取上下文：

- [**FltGetContexts**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetcontexts)
- [**FltGetContextsEx**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetcontextsex)
- [**FltGetFileContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetfilecontext)
- [**FltGetInstanceContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetinstancecontext)
- [**FltGetStreamContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetstreamcontext)
- [**FltGetStreamHandleContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetstreamhandlecontext)
- [**FltGetTransactionContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgettransactioncontext)
- [**FltGetVolumeContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetvolumecontext)

每个成功的 get 例程都会增加上下文的引用计数，要求微筛选器调用 [**FltReleaseContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreleasecontext) 而不再需要上下文指针。

在以下代码示例中，从 [SwapBuffers 示例微筛选](https://github.com/microsoft/Windows-driver-samples/tree/master/filesys/miniFilter/swapBuffers)器中获取，微筛选器驱动程序调用 [**FltGetVolumeContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetvolumecontext) 来获取卷上下文：

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
