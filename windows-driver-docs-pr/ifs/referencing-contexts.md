---
title: 引用上下文
description: 引用上下文
keywords:
- 上下文 WDK 文件系统微筛选器，引用
- 引用上下文
ms.date: 01/22/2021
ms.localizationpriority: medium
ms.openlocfilehash: 8ea46fe7dcc5513d19d2dcec6f82f35b2529e8d8
ms.sourcegitcommit: 204ed37ede1cd462ef6f6c9211a223fd304da4a5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2021
ms.locfileid: "99502038"
---
# <a name="referencing-contexts"></a>引用上下文

筛选器管理器使用引用计数来管理微筛选器上下文的生存期。 引用计数是一个数字，用于指示上下文的状态。

只要成功创建了上下文，上下文的引用计数就会初始化为一个 (这称为对上下文) 的初始引用。

只要引用上下文（例如，成功地 [设置](setting-contexts.md) 或 [获取](getting-contexts.md)上下文），上下文的引用计数就会递增1。

如果不再需要某个上下文，则必须减少其引用计数。 正引用计数意味着上下文可用。 如果引用计数变为零，则上下文不可用，筛选器管理器最终将其释放。

通常，当对象解除锁定时，通常会释放上下文的初始引用。 但是，如果微筛选器必须从对象中删除上下文，则微筛选器必须以某种方式发布对上下文的初始引用。 为了安全地释放对上下文的初始引用，微筛选器驱动程序会调用 [**FltDeleteContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeletecontext)。

微筛选器可以通过调用 [**FltReferenceContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreferencecontext) 将其自己的引用添加到上下文，以增加上下文的引用计数。 通过调用 [**FltReleaseContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreleasecontext)，最终必须删除此添加的引用。
