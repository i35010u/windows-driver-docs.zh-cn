---
title: 设置裁切矩形
description: 设置裁切矩形
keywords:
- 剪刀矩形 WDK DirectX 9。0
- 矩形剪辑区域 WDK DirectX 9。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7a615a0428c0393dd3e5937eae9877c685db08a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826588"
---
# <a name="setting-scissor-rectangle"></a>设置裁切矩形


## <span id="ddk_setting_scissor_rectangle_gg"></span><span id="DDK_SETTING_SCISSOR_RECTANGLE_GG"></span>


DirectX 9.0 版本驱动程序必须支持设置矩形剪辑区域，即剪式矩形。 设置此剪刀矩形后，呈现仅限于由剪刀矩形指定的呈现器目标部分。 若要设置剪刀矩形，驱动程序必须 \_ 在其 [**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb) 函数中处理 D3DDP2OP SETSCISSORRECT 操作代码。 一个 RECT 结构，它指定矩形剪辑区域在 [命令流](command-stream.md)中遵循操作代码。

 

