---
title: 设置当前索引缓冲区
description: 设置当前索引缓冲区
ms.assetid: 4d190ce1-56a0-4445-9a68-6a24f3a9aee4
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示、 索引缓冲区
- 索引缓冲区 WDK Directx 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dbd3afef68b667f8fc5ecc1ce128295f51fb8908
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390440"
---
# <a name="setting-the-current-index-buffer"></a>设置当前索引缓冲区


## <span id="ddk_setting_the_current_index_buffer_gg"></span><span id="DDK_SETTING_THE_CURRENT_INDEX_BUFFER_GG"></span>


与顶点数据一样，要由绘图基元的索引缓冲区不再是传递给与基元，驱动程序的数据的一部分，但而是驱动程序状态。 当前索引缓冲区设置的新 DP2 令牌 D3DDP2OP\_SETINDICES。 此令牌建立具有给定句柄的索引缓冲区为当前的索引缓冲区，用于绘制索引的基元，直到新的索引缓冲区设置或清除当前索引缓冲区 （在 DP2 令牌数据中指定的索引缓冲区句柄为零）。

 

 





