---
title: 删除上下文
description: 删除上下文
keywords:
- 上下文 WDK 文件系统微筛选器，删除
- 正在删除上下文
ms.date: 01/22/2021
ms.localizationpriority: medium
ms.openlocfilehash: 2efc217fa923c07f5d9c9b86410099921938a3cc
ms.sourcegitcommit: 204ed37ede1cd462ef6f6c9211a223fd304da4a5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2021
ms.locfileid: "99502044"
---
# <a name="deleting-contexts"></a>删除上下文

成功调用 **FltSet *Xxx* 上下文** 所 [设置](setting-contexts.md)的每个上下文都必须最终删除。

当出现以下情况时，筛选器管理器会自动删除上下文：

- 上下文附加到的对象已被删除
- 从卷中分离了微筛选器实例
- 已卸载微筛选器驱动程序

*因此，微筛选器很少需要显式删除上下文。*

微筛选器可以通过调用以下上下文删除例程之一删除上下文：

- [**FltDeleteContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeletecontext)
- [**FltDeleteFileContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeletefilecontext)
- [**FltDeleteInstanceContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeleteinstancecontext)
- [**FltDeleteStreamContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeletestreamcontext)
- [**FltDeleteStreamHandleContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeletestreamhandlecontext)
- [**FltDeleteTransactionContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeletetransactioncontext)
- [**FltDeleteVolumeContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeletevolumecontext)

只有在当前为 [对象设置](setting-contexts.md)了上下文时，才能删除该上下文。 如果上下文尚未设置，或者它已由成功调用 **FltSet *Xxx* 上下文** 替换，则无法删除该上下文。

**FltDelete *Xxx* 上下文** 例程返回指向 *OldContext* 参数中的旧上下文的指针，如果 *OldContext* 为非 **NULL** ，并且未指向 NULL_CONTEXT。 如果 *OldContext* 为 **NULL**，则筛选器管理器将减少上下文中的引用计数，除非微筛选器没有未完成的引用，否则将会释放该计数。

下面的代码示例演示如何删除流上下文：

```cpp
status = FltDeleteStreamContext(
 FltObjects->Instance,      //Instance
 FltObjects->FileObject,    //FileObject
           &oldContext);              //OldContext
//
// Perform any needed processing
// ...
//
if (oldContext != NULL) {
 FltReleaseContext(oldContext);
}
```

在此示例中， [**FltDeleteStreamContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeletestreamcontext)：

- 从流中删除流上下文。
- 不 *会减小上下文* 的引用计数，因为 *OldContext* 参数为非 NULL。
- 返回从 *OldContext* 参数中的流) 删除的上下文的已删除 (上下文的地址。

由于非空的 *OldContext* 参数，执行任何所需的处理后，筛选器必须通过调用 [**FltReleaseContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreleasecontext)来释放已删除的上下文。
