---
title: 流零
description: 流零
ms.assetid: d6f0a625-c594-45b6-a229-b9c8a5275002
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，多个顶点流
- 多个顶点流式传输 WDK DirectX 8.0
- 顶点多个流 WDK DirectX 8.0
- 流式传输零 WDK DirectX 8.0
- 顶点流式传输零 WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 837cfe8887973a692f4dbb54b155e43d6db52f1d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376000"
---
# <a name="stream-zero"></a>流零


## <span id="ddk_stream_zero_gg"></span><span id="DDK_STREAM_ZERO_GG"></span>


顶点流零的处理方式是从其他流，因为它是唯一的 Direct3D 的早期版本支持的流。 具有灵活的顶点的格式 (FVF)，其中 FVF 字段不为零，顶点缓冲区只能绑定到流零。 但是，这并不意味着始终绑定到流零的顶点缓冲区具有灵活的顶点格式。

当一个特殊的固定功能顶点着色器是当前的顶点着色器句柄，Stream 零也是隐式的顶点源。

 

 





