---
title: 设置当前索引缓冲区
description: 设置当前索引缓冲区
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，索引缓冲区
- 索引缓冲区 WDK Directx 8。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6aaa72f12dc9304f849a40e707d70d35e960cc8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826597"
---
# <a name="setting-the-current-index-buffer"></a>设置当前索引缓冲区


## <span id="ddk_setting_the_current_index_buffer_gg"></span><span id="DDK_SETTING_THE_CURRENT_INDEX_BUFFER_GG"></span>


与顶点数据一样，由绘图基元使用的索引缓冲区不再是通过基元传递给驱动程序的数据的一部分，而是驱动程序状态。 当前索引缓冲区由新的 DP2 标记 D3DDP2OP \_ SETINDICES 设置。 此标记将给定句柄的索引缓冲区建立为要在绘制索引基元时使用的当前索引缓冲区，直到设置了新的索引缓冲区，或者清除了当前索引缓冲区 (在 DP2 令牌数据) 中指定了零的索引缓冲区句柄。

 

 





