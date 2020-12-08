---
title: 流零
description: 流零
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，多个顶点流
- 多个顶点流 WDK DirectX 8。0
- 顶点多流 WDK DirectX 8。0
- 流零 WDK DirectX 8。0
- 顶点流零 WDK DirectX 8。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 629000aca19d04bec2d3db9bcf36eb03f9872ae2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831891"
---
# <a name="stream-zero"></a>流零


## <span id="ddk_stream_zero_gg"></span><span id="DDK_STREAM_ZERO_GG"></span>


顶点流零的处理方式不同于其他流，因为它是早期版本的 Direct3D 支持的唯一流。 具有灵活顶点格式 (FVF) （其中 FVF 字段为非零）的顶点缓冲区只能绑定到流零。 但是，这并不意味着绑定到流零的顶点缓冲区始终具有灵活的顶点格式。

当一种特殊的固定函数顶点着色器为当前顶点着色器控点时，Stream zero 也是隐含的顶点源。

 

 





