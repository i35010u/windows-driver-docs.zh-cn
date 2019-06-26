---
title: 引用上下文
description: 引用上下文
ms.assetid: 9ac3aedb-e057-4e19-9de5-709311072b09
keywords:
- 上下文 WDK 文件系统微筛选器，引用
- 引用上下文
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33d5010dc4197c856c67630ca48fd0fd5ce4a863
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385137"
---
# <a name="referencing-contexts"></a>引用上下文


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


筛选器管理器使用引用计数来管理微筛选器驱动程序上下文的生存期。 引用计数是一个数字，指示上下文的状态。 无论何时创建上下文，上下文的引用计数初始化为一个 （这称为对上下文的初始引用）。 每当系统组件通过引用上下文，则上下文的引用计数就会递增 1。 当不再需要上下文时，其引用计数将递减。 正引用计数意味着上下文可用。 当引用计数变为零时，上下文是不可用，并筛选器管理器最终将其释放。

对象，则将调用时，通常被释放到上下文的初始引用。 但是，如果微筛选器驱动程序必须删除从对象上下文，微筛选器驱动程序必须以某种方式释放上下文，初始引用。 若要安全地释放上下文，初始引用，微筛选器驱动程序调用[ **FltDeleteContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltdeletecontext)。

微筛选器驱动程序可以通过调用添加自己的上下文的引用[ **FltReferenceContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltreferencecontext)来增加上下文的引用计数。 这添加最终必须通过调用删除引用[ **FltReleaseContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltreleasecontext)。

 

 




