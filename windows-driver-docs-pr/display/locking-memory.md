---
title: 锁定内存
description: 锁定内存
keywords:
- 锁定内存 WDK 显示
- GPU 延迟防护 WDK 显示
- 内存锁定 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ffe738e34a18016cd10ed4b700f71576843e0b1d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796247"
---
# <a name="locking-memory"></a>锁定内存


## <span id="ddk_locking_memory_gg"></span><span id="DDK_LOCKING_MEMORY_GG"></span>


为了使图形处理单元 (GPU) 停止，准备工作线程在 GPU 忙于处理其他操作时锁定内存。 但是，如果将大量分配完全分页到磁盘，则在驱动程序等待 GPU 计划程序在分配中分页时，GPU 可能会停止。

 

 





