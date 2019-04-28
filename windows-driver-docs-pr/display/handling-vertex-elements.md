---
title: 处理顶点元素
description: 处理顶点元素
ms.assetid: b931b674-f8c4-4852-a66a-97d545059287
keywords:
- 顶点着色器声明 WDK DirectX 9.0 中，处理顶点元素
- 着色器声明 WDK DirectX 9.0 中，处理顶点元素
- 顶点元素 WDK DirectX 9.0
- 顶点元素 WDK DirectX 9.0 中，顶点着色器声明
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 921f232be4ef716f33b6c803958e41447ed0b00f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353871"
---
# <a name="handling-vertex-elements"></a>处理顶点元素


## <span id="ddk_handling_vertex_elements_gg"></span><span id="DDK_HANDLING_VERTEX_ELEMENTS_GG"></span>


DirectX 9.0 版本驱动程序可以处理的着色器声明中的顶点元素的数目取决于驱动程序的设备是否支持固定函数或可编程顶点处理。 有关顶点着色器声明中的元素的详细信息，请参阅[分隔的声明和顶点着色器代码](separating-declarations-and-code-for-vertex-shaders.md)。

如果设备支持处理固定函数顶点，该驱动程序必须处理多达 17 顶点元素 （FVF 代码）。

如果设备支持可编程顶点处理，该驱动程序必须处理最多 64 个顶点元素，并跳过不使用这些元素。 由于输入每个通道 (最大 4) 支持顶点着色器 3 的设备注册 （最多 16）\_0 和更高版本可以单独声明，最多 64 个 (16 \* 4) 可使用顶点元素。 此最大 64 数不包括结束元素，它构成 D3DDECL\_结束宏。

 

 





