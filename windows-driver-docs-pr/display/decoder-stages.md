---
title: 解码器阶段
description: 解码器阶段
ms.assetid: 34562b2a-9568-440d-b6ec-dbd1e5004d56
keywords:
- DirectX 视频加速 WDK Windows 2000 显示视频解码
- 视频加速 WDK DirectX，视频解码
- VA WDK DirectX，视频解码
- 解码视频 WDK DirectX VA，解码器阶段
- 视频解码 WDK DirectX VA，解码器阶段
- 解码器暂存 WDK DirectX VA
- 逆变离散余弦 WDK DirectX VA
- IDCT WDK DirectX VA
- MCP WDK DirectX VA
- 运动补偿 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c1a39d09d330a48e2ff21153c87d4af4e3d7e3b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360093"
---
# <a name="decoder-stages"></a>解码器阶段


## <span id="ddk_decoder_stages_gg"></span><span id="DDK_DECODER_STAGES_GG"></span>


下图中描述的解码器阶段显示运动补偿预测 (MCP) 和逆变离散余弦值的操作的加速器 (IDCT) 部分。 数据表示为 dct\_类型是一个用于控制执行 IDCT 的类型的语法元素。

![说明解码器阶段的关系图](images/decstages.png)

 

 





