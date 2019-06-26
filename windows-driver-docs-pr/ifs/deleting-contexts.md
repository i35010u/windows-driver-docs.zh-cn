---
title: 删除上下文
description: 删除上下文
ms.assetid: 43a30a75-4344-4fc5-ad57-28b48c2e54a8
keywords:
- 上下文 WDK 文件系统微筛选器，删除
- 正在删除上下文
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c56ebde9775c8dcc7dcec160cb4a5b4eb0c576b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376111"
---
# <a name="deleting-contexts"></a>删除上下文


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


通过成功调用设置每个上下文**FltSet***Xxx***上下文**最终必须删除。 但是，筛选器管理器上下文将自动删除附加到的对象中删除时，从卷分离微筛选器驱动程序实例时或在卸载微筛选器驱动程序时。 因此，很少需要显式删除上下文微筛选器驱动程序。

微筛选器驱动程序可以通过调用来删除上下文**FltDelete***Xxx***上下文**，其中*Xxx*的上下文类型，或通过调用[ **FltDeleteContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltdeletecontext)。

仅当为某个对象当前设置，可以删除上下文。 无法删除上下文，如果它尚未尚未设置，或者已替换为在成功调用**FltSet***Xxx***上下文**。

在调用**FltDelete***Xxx***上下文**，旧的上下文中返回*OldContext*参数，如果为非**NULL**。 如果*OldContext*参数是**NULL**，除非微筛选器驱动程序对其具有未完成的引用被释放上下文的筛选器管理器递减引用计数。

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

在此示例中， [ **FltDeleteStreamContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltdeletestreamcontext)删除流，但它的流上下文不减小上下文的引用计数，因为*OldContext*参数为非**NULL**。 **FltDeleteStreamContext**返回的已删除的上下文中的地址*OldContext*参数。 调用方执行任何所需的处理后，必须通过调用释放已删除的上下文**FltReleaseContext**。

 

 




