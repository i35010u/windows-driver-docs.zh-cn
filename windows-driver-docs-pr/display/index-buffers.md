---
title: 索引缓冲区
description: 索引缓冲区
ms.assetid: 5bf7dc12-d988-4194-a81f-52c9c5356610
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示、 索引缓冲区
- 索引缓冲区 WDK Directx 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd3acecf1f197d1ceb9893612ea9349a38cc6776
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350269"
---
# <a name="index-buffers"></a>索引缓冲区


## <span id="ddk_index_buffers_gg"></span><span id="DDK_INDEX_BUFFERS_GG"></span>


DirectX 8.0 引入索引缓冲区的概念。 这类缓冲区很非常类似于顶点缓冲区，但存储中的顶点数据的简单 16 或 32 位索引而不是本身的顶点数据。 索引缓冲区扩展顶点缓冲区，例如最佳的下载和缓存，对数据编制索引的所有的权益。

创建、 锁定、 解锁和销毁与相同的驱动程序入口点所使用的顶点缓冲区索引缓冲区。 驱动程序可以区分这些缓冲区类型使用新的图面上功能位 DDSCAPS2\_INDEXBUFFER。 针对索引缓冲区中设置此标志**ddsCapsEx.dwCaps2**字段的面[ **DD\_图面\_详细**](https://msdn.microsoft.com/library/windows/hardware/ff551737)结构。 可以明确的顶点缓冲区。

与许多其他图面上的类型，驱动程序不需要设置功能 DDSCAPS2\_INDEXBUFFER 向运行时报告其功能时接收驱动程序调用索引缓冲区创建、 析构和锁定。 假定支持顶点缓冲区的 DirectX 8.0 驱动程序还支持索引缓冲区。 如果基础硬件具有索引缓冲区不直接支持，该驱动程序应通过面的分配系统内存处理缓冲区创建索引。

 

 





