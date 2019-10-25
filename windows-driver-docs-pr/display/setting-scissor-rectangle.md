---
title: 设置裁切矩形
description: 设置裁切矩形
ms.assetid: e85b4987-26b7-4005-b8eb-81ca36a9a777
keywords:
- 剪刀矩形 WDK DirectX 9。0
- 矩形剪辑区域 WDK DirectX 9。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93fa5db94bc32bea0811919565b45eb3e6a031b8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825824"
---
# <a name="setting-scissor-rectangle"></a>设置裁切矩形


## <span id="ddk_setting_scissor_rectangle_gg"></span><span id="DDK_SETTING_SCISSOR_RECTANGLE_GG"></span>


DirectX 9.0 版本驱动程序必须支持设置矩形剪辑区域，即剪式矩形。 设置此剪刀矩形后，呈现仅限于由剪刀矩形指定的呈现器目标部分。 若要设置剪刀矩形，驱动程序必须在其[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)函数中处理 D3DDP2OP\_SETSCISSORRECT 操作代码。 一个 RECT 结构，它指定矩形剪辑区域在[命令流](command-stream.md)中遵循操作代码。

 

 





