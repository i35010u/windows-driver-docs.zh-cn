---
title: 锁定内存
description: 锁定内存
ms.assetid: bf14e0f7-13cc-4e55-bbb1-a6b6f6b6271f
keywords:
- 锁定内存 WDK 显示
- GPU 停止防护 WDK 显示
- 内存锁定 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f9b08fbf0dcbf6c914bd0f2518f1a5d66daa467
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347548"
---
# <a name="locking-memory"></a>锁定内存


## <span id="ddk_locking_memory_gg"></span><span id="DDK_LOCKING_MEMORY_GG"></span>


若要防止拖延症图形处理单元 (GPU)，准备工作线程锁定内存而 GPU 正忙于处理其他操作。 但是，如果分配大量的完全分页到磁盘，GPU 可能会停止该驱动程序等待 GPU 计划程序中分配页时。

 

 





