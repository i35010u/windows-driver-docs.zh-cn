---
title: 引用上下文
description: 引用上下文
keywords:
- 上下文 WDK 文件系统微筛选器，引用
- 引用上下文
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb078d60f0d22e3abc66ae876586ad10fd433ec2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829667"
---
# <a name="referencing-contexts"></a>引用上下文


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


筛选器管理器使用引用计数来管理微筛选器驱动程序上下文的生存期。 引用计数是一个数字，用于指示上下文的状态。 每当创建上下文时，上下文的引用计数都将初始化为一个 (这称为对上下文) 的初始引用。 每当系统组件引用上下文时，上下文的引用计数将递增1。 如果不再需要某个上下文，则会减少其引用计数。 正引用计数意味着上下文可用。 如果引用计数变为零，则上下文不可用，筛选器管理器最终将其释放。

通常，当对象解除锁定时，通常会释放上下文的初始引用。 但是，如果微筛选器驱动程序必须从对象中删除上下文，则微筛选器驱动程序必须以某种方式发布对上下文的初始引用。 为了安全地释放对上下文的初始引用，微筛选器驱动程序会调用 [**FltDeleteContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeletecontext)。

微筛选器驱动程序可以通过调用 [**FltReferenceContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreferencecontext) 将其自己的引用添加到上下文，以增加上下文的引用计数。 通过调用 [**FltReleaseContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreleasecontext)，最终必须删除此添加的引用。

 

