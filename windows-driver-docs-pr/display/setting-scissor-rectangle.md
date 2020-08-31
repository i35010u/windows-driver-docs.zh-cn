---
title: 设置裁切矩形
description: 设置裁切矩形
ms.assetid: e85b4987-26b7-4005-b8eb-81ca36a9a777
keywords:
- 剪刀矩形 WDK DirectX 9。0
- 矩形剪辑区域 WDK DirectX 9。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f1a85dfa9b41d8a2b230a0d77f78e83eaf2e001
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063476"
---
# <a name="setting-scissor-rectangle"></a>设置裁切矩形


## <span id="ddk_setting_scissor_rectangle_gg"></span><span id="DDK_SETTING_SCISSOR_RECTANGLE_GG"></span>


DirectX 9.0 版本驱动程序必须支持设置矩形剪辑区域，即剪式矩形。 设置此剪刀矩形后，呈现仅限于由剪刀矩形指定的呈现器目标部分。 若要设置剪刀矩形，驱动程序必须 \_ 在其 [**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb) 函数中处理 D3DDP2OP SETSCISSORRECT 操作代码。 一个 RECT 结构，它指定矩形剪辑区域在 [命令流](command-stream.md)中遵循操作代码。

 

