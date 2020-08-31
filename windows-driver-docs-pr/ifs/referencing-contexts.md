---
title: 引用上下文
description: 引用上下文
ms.assetid: 9ac3aedb-e057-4e19-9de5-709311072b09
keywords:
- 上下文 WDK 文件系统微筛选器，引用
- 引用上下文
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 030285400293dbd0cff98daf2ef4f2de0c954597
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063256"
---
# <a name="referencing-contexts"></a>引用上下文


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


筛选器管理器使用引用计数来管理微筛选器驱动程序上下文的生存期。 引用计数是一个数字，用于指示上下文的状态。 每当创建上下文时，上下文的引用计数都将初始化为一个 (这称为对上下文) 的初始引用。 每当系统组件引用上下文时，上下文的引用计数将递增1。 如果不再需要某个上下文，则会减少其引用计数。 正引用计数意味着上下文可用。 如果引用计数变为零，则上下文不可用，筛选器管理器最终将其释放。

通常，当对象解除锁定时，通常会释放上下文的初始引用。 但是，如果微筛选器驱动程序必须从对象中删除上下文，则微筛选器驱动程序必须以某种方式发布对上下文的初始引用。 为了安全地释放对上下文的初始引用，微筛选器驱动程序会调用 [**FltDeleteContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeletecontext)。

微筛选器驱动程序可以通过调用 [**FltReferenceContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreferencecontext) 将其自己的引用添加到上下文，以增加上下文的引用计数。 通过调用 [**FltReleaseContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreleasecontext)，最终必须删除此添加的引用。

 

