---
title: 删除上下文
description: 删除上下文
ms.assetid: 43a30a75-4344-4fc5-ad57-28b48c2e54a8
keywords:
- 上下文 WDK 文件系统微筛选器，删除
- 正在删除上下文
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8fe713cd61cc4678812d23482cb1d951d144275
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065076"
---
# <a name="deleting-contexts"></a>删除上下文


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


成功调用 **FltSet***Xxx***上下文** 所设置的每个上下文都必须最终删除。 不过，筛选器管理器会在其附加到的对象被删除、从卷中分离了筛选器驱动程序实例或卸载微筛选器驱动程序时自动删除上下文。 因此，微筛选器驱动程序很少需要显式删除上下文。

微筛选器驱动程序可以通过调用 **FltDelete***xxx***上下文**（其中 *Xxx* 是上下文类型，或通过调用 [**FltDeleteContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeletecontext)）来删除上下文。

只有在当前为对象设置了上下文时，才能删除该上下文。 如果上下文尚未设置，或者它已由成功调用 **FltSet***Xxx***上下文**替换，则无法删除该上下文。

在调用**FltDelete***Xxx***上下文**时，如果不为**NULL**，则将在*OldContext*参数中返回旧上下文。 如果 *OldContext* 参数为 **NULL**，筛选器管理器将减少上下文中的引用计数，除非微微筛选器驱动程序对其具有未完成的引用，否则会释放该引用计数。

下面的代码示例演示如何删除流上下文：

```cpp
status = FltDeleteStreamContext(
 FltObjects->Instance,      //Instance
 FltObjects->FileObject,    //FileObject
           &oldContext);              //OldContext
...
if (oldContext != NULL) {
 FltReleaseContext(oldContext);
}
```

在此示例中， [**FltDeleteStreamContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeletestreamcontext) 从流中删除流上下文，但不会减小上下文的引用计数，因为 *OldContext* 参数为非**NULL**。 **FltDeleteStreamContext** 返回 *OldContext* 参数中已删除上下文的地址。 执行任何所需的处理后，调用方必须通过调用 **FltReleaseContext**来释放已删除的上下文。

 

