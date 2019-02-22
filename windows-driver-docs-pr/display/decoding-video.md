---
title: 解码视频
description: 解码视频
ms.assetid: d434469f-1279-47c4-b824-61daeb25b214
keywords:
- 有关解码视频解码 WDK DirectX va，因此视频
- 有关解码视频解码视频 WDK DirectX VA，
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 932408a24eabffcf021e5a969f8db14393543050
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554769"
---
# <a name="decoding-video"></a>解码视频


Microsoft Direct3D 运行时将调用用户模式显示驱动程序[ **DecodeBeginFrame** ](https://msdn.microsoft.com/library/windows/hardware/ff551802)并[ **DecodeEndFrame** ](https://msdn.microsoft.com/library/windows/hardware/ff551805)到函数指示用户模式显示驱动程序可以对视频进行解码这些函数调用之间的时间段。 用户模式显示驱动程序可以执行任何视频之前解码操作，Microsoft Direct3D 运行时必须调用用户模式显示驱动程序[ **SetDecodeRenderTarget** ](https://msdn.microsoft.com/library/windows/hardware/ff569530)函数设置对于那些呈现目标图面解码操作。 但是，在调用**SetDecodeRenderTarget**可仅外部出现的开始范围和结束帧时间段。

在保护模式下和在调用[ **DecodeBeginFrame**](https://msdn.microsoft.com/library/windows/hardware/ff551802)，Direct3D 运行时设置或更改的变量中的 DirectX VA 内容密钥的**pPVPSetKey**的成员[ **D3DDDIARG\_DECODEBEGINFRAME** ](https://msdn.microsoft.com/library/windows/hardware/ff542987)结构指向。 解码设备使用此密钥的受保护的此压缩的 DirectX VA 缓冲区的传输和后续帧。

**请注意**   Direct3D 运行时集**pPVPSetKey**仅用于更改或设置项的指针。 若要保留以前设置中使用的键，在运行时将指针设置**NULL**以避免可能会花费较长时间重新加载的相同的密钥。 该驱动程序不会消除冗余的设置。 解码器应用程序必须避免冗余设置。

 

呈现目标图面为解码后设置操作，用户模式显示驱动程序可以接收到调用其[ **DecodeExecute** ](https://msdn.microsoft.com/library/windows/hardware/ff551808)函数来执行视频解码开始帧之间的操作并最终帧时间段。

在调用[ **DecodeExecute**](https://msdn.microsoft.com/library/windows/hardware/ff551808)，并非所有中指定的缓冲区类型**CompressedBufferType**的成员[ **DXVADDI\_DECODEBUFFERDESC** ](https://msdn.microsoft.com/library/windows/hardware/ff562896)结构**pCompressedBuffers**数组[ **D3DDDIARG\_DECODEEXECUTE** ](https://msdn.microsoft.com/library/windows/hardware/ff543001)结构用于每种解码 GUID 的**hDecode** D3DDDIARG 成员\_DECODEEXECUTE 指定。 例如，切片控件 (D3DDDIFMT\_SLICECONTROLDATA)、 反量化 (D3DDDIFMT\_INVERSEQUANTIZATIONDATA)，和位流 (D3DDDIFMT\_BITSTREAMDATA) 缓冲区所需的仅长度可变的解码 (VLD) 处理和消除马赛克功能控制缓冲区 (D3DDDIFMT\_DEBLOCKINGDATA) 根本不使用 MPEG 2。

在受保护模式下，使用内容密钥加密的受保护传输的缓冲区包含指向在其缓冲区描述符的初始的计数器值的指针 (也就是说，在变量的**pCipherCounter** 的成员[**DXVADDI\_DECODEBUFFERDESC** ](https://msdn.microsoft.com/library/windows/hardware/ff562896)结构指向)。 用户模式显示驱动程序的每次调用[ **DecodeExecute** ](https://msdn.microsoft.com/library/windows/hardware/ff551808)函数必须执行的此类缓冲区传输到本地的视频内存之前受保护**DecodeExecute**在解码操作中使用的缓冲区的数据。 但是，没有计划存在加密类型之外的剩余差异的 DirectX VA 压缩缓冲区 (D3DDDIFMT\_RESIDUALDIFFERENCEDATA) 和位流 (D3DDDIFMT\_BITSTREAMDATA) 类型。

 

 





