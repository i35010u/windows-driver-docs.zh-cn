---
title: 索引缓冲区
description: 索引缓冲区
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，索引缓冲区
- 索引缓冲区 WDK Directx 8。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fdcdda532ebc283c7646939ee6c3c52593443621
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827285"
---
# <a name="index-buffers"></a>索引缓冲区


## <span id="ddk_index_buffers_gg"></span><span id="DDK_INDEX_BUFFERS_GG"></span>


DirectX 8.0 引入了索引缓冲区的概念。 这些缓冲区与顶点缓冲区非常相似，但将简单的16或32位索引存储到顶点数据而不是顶点数据本身。 索引缓冲区扩展了顶点缓冲区的所有优点，例如，为数据编制索引的最佳下载和缓存。

使用与用于顶点缓冲区的驱动程序入口点相同的驱动程序入口点创建、锁定、解除锁定和销毁索引缓冲区。 驱动程序可以使用新的 surface DDSCAPS2 INDEXBUFFER 来区分这些缓冲区类型 \_ 。 对于索引缓冲区，此标志是在图面图 [**\_ 面图面 \_**](/windows/win32/api/ddrawint/ns-ddrawint-dd_surface_more)上的 " **ddsCapsEx. dwCaps2** " 字段中设置的。 对于顶点缓冲区，这会很清楚。

与许多其他表面类型不同，驱动程序 \_ 在向运行时报告其功能以便接收索引缓冲区创建、析构和锁定的驱动程序调用时，不需要设置功能 DDSCAPS2 INDEXBUFFER。 假定支持顶点缓冲区的 DirectX 8.0 驱动程序也支持索引缓冲区。 如果基础硬件不能直接支持索引缓冲区，则驱动程序应该通过为图面分配系统内存来处理索引缓冲区创建。

 

