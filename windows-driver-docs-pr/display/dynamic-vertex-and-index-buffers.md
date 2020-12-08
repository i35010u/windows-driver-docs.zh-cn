---
title: 动态顶点和索引缓冲区
description: 动态顶点和索引缓冲区
keywords:
- 动态顶点 WDK DirectX 9。0
- 索引缓冲区 WDK DirectX 9。0
- 动态缓冲 WDK DirectX 9。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 644589927d19690e0799fd55057cf43e0d366435
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840395"
---
# <a name="dynamic-vertex-and-index-buffers"></a>动态顶点和索引缓冲区


## <span id="ddk_dynamic_vertex_and_index_buffers_gg"></span><span id="DDK_DYNAMIC_VERTEX_AND_INDEX_BUFFERS_GG"></span>


动态顶点或索引缓冲区是应用程序频繁锁定并写入到的资源。 当在对驱动程序的 [*LockD3DBuffer*](/previous-versions/windows/hardware/drivers/ff568216(v=vs.85)) 函数的调用中锁定动态缓冲区时，DDLOCK \_ OKTOSWAP 位 (也称为 " \_ DD DwFlags 结构" 的 **LOCKDATA** 成员的 D3DLOCK 丢弃位) ， \_ 可将其设置为指示调用方不需要缓冲区的现有内容。 因此，在将指针返回到缓冲区数据之前，驱动程序可以丢弃内容。 由于调用方不需要现有的内容，因此驱动程序可以通过将缓冲区的 DD SURFACE 全局结构的 **fpVidMem** 成员 \_ 设置 \_ 为新值来重命名缓冲区。 通过重命名缓冲区 (即，设置多个缓冲) ，驱动程序可避免硬件停止。

\_只能将 DDLOCK OKTOSWAP 位设置为锁定动态缓冲区，并且决不会锁定静态缓冲区。

请注意，驱动程序应在 [AGP](agp-support.md) 内存中存储动态缓冲区，因为如果动态缓冲区存储在本地视频内存中，并且应用程序以非顺序的方式将数据写入到这些缓冲区中，则可能会严重影响总线性能。

 

