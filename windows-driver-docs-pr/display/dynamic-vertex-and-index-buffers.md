---
title: 动态顶点和索引缓冲区
description: 动态顶点和索引缓冲区
ms.assetid: 81ee22c6-3f98-4767-a4cd-a7907ed8f8a2
keywords:
- 动态顶点 WDK DirectX 9.0
- 索引缓冲区 WDK DirectX 9.0
- 动态缓冲区 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c91fbbb9f1a2d52a447615698fd06c2ef4e7a57d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360363"
---
# <a name="dynamic-vertex-and-index-buffers"></a>动态顶点和索引缓冲区


## <span id="ddk_dynamic_vertex_and_index_buffers_gg"></span><span id="DDK_DYNAMIC_VERTEX_AND_INDEX_BUFFERS_GG"></span>


动态顶点或索引缓冲区是应用程序经常会锁定，并将写入到的资源。 动态缓冲，驱动程序的调用中的锁定时[ *LockD3DBuffer* ](https://msdn.microsoft.com/library/windows/hardware/ff568216)函数，DDLOCK\_OKTOSWAP 位 (也称为 D3DLOCK\_放弃位) 的**dwFlags** DD 成员\_LOCKDATA 结构可以设置，以指示调用方不需要缓冲区的现有内容。 因此，该驱动程序可以返回到缓冲区数据的指针之前放弃内容。 因为调用方不需要的现有内容，该驱动程序可以通过重命名缓冲区设置**fpVidMem** DD 成员\_面\_全局结构为新值的缓冲区。 通过重命名的缓冲区 （即，设置多个缓冲），该驱动程序可避免硬件停滞。

DDLOCK\_OKTOSWAP 位只能锁定动态缓冲区并永远不会锁定静态缓冲区设置。

请注意，驱动程序应存储中的动态缓冲区[AGP](agp-support.md)内存因为如果本地视频内存中存储动态缓冲区，并且应用程序写入到这些缓冲区数据以无序的方式，总线性能可能会严重受影响。

 

 





