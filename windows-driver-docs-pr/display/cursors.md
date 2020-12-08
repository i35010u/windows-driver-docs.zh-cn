---
title: 光标
description: 光标
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，光标
- 游标 WDK DirectX 8。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b802b2494a21528b6dd53950fb5a09ec1141a28f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823301"
---
# <a name="cursors"></a>光标


## <span id="ddk_cursors_gg"></span><span id="DDK_CURSORS_GG"></span>


DirectX 8.0 添加了一个 API，用于支持高更新频率游标，而不需要对主要表面的 API 级别直接访问。 对于 DirectX 8.0，如果功能允许，游标是标准的 GDI 游标，否则将通过 DirectDraw blts 对其进行模拟。 为了支持 DirectX 游标 API，驱动程序必须在 D3DCAPS8 中返回功能信息。

应将 " **CursorCaps** " 字段设置为 "D3DCURSORCAPS"、"D3DCURSORCAPS" 或 "/"， \_ \_ 以指示支持单色和彩色硬件光标。 **MaxCursorEdgeSize** 字段应设置为最大宽度和最大高度为硬件游标 (或零（如果不支持) 硬件游标）。 不能为光标的宽度和高度表示不同的最大大小。

 

 





