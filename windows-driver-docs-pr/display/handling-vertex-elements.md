---
title: 处理顶点元素
description: 处理顶点元素
keywords:
- 顶点着色器声明 WDK DirectX 9.0，处理顶点元素
- 着色器声明 WDK DirectX 9.0，处理顶点元素
- 顶点元素 WDK DirectX 9。0
- 顶点元素 WDK DirectX 9.0，顶点着色器声明
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6458c4118e3f2f9b2b9f668ac6ea3bb119fd8e05
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830667"
---
# <a name="handling-vertex-elements"></a>处理顶点元素


## <span id="ddk_handling_vertex_elements_gg"></span><span id="DDK_HANDLING_VERTEX_ELEMENTS_GG"></span>


DirectX 9.0 版本驱动程序可以处理的着色器声明中的顶点元素数取决于驱动程序的设备是否支持固定函数或可编程顶点处理。 有关着色器声明中的顶点元素的详细信息，请参阅 [分隔顶点着色器的声明和代码](separating-declarations-and-code-for-vertex-shaders.md)。

如果设备支持固定函数顶点处理，则驱动程序必须处理最多17个顶点元素， (FVF 代码) 。

如果设备支持可编程顶点处理，则驱动程序必须处理最多64个顶点元素，并跳过不使用的元素。 由于每个通道 (最多4个输入寄存器的)  (16 个支持顶点着色器 3 0 的设备的最大) \_ ，并且更高版本可以单独声明，最大为 64 (\* 有16个) 顶点元素。 此最大数目为64，不包括 end 元素，它是从 D3DDECL \_ 结束宏组成的。

 

 





