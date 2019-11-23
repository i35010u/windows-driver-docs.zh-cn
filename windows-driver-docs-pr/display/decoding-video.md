---
title: 解码视频
description: 解码视频
ms.assetid: d434469f-1279-47c4-b824-61daeb25b214
keywords:
- 视频解码 WDK DirectX VA，关于解码视频
- 解码视频 WDK DirectX VA，关于解码视频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 499a7929ba429ef464bf8dc8a411563270d10f40
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839018"
---
# <a name="decoding-video"></a>解码视频


Microsoft Direct3D runtime 调用用户模式显示驱动程序的[**DecodeBeginFrame**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_decodebeginframe)和[**DecodeEndFrame**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_decodeendframe)函数，以指示这些函数调用之间的时间段，用户模式显示驱动程序可以解码视频。 在用户模式显示驱动程序可以执行任何视频解码操作之前，Microsoft Direct3D 运行时必须调用用户模式显示驱动程序的[**SetDecodeRenderTarget**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_setdecoderendertarget)函数，以便为这些解码操作设置呈现目标图面。 但是，对**SetDecodeRenderTarget**的调用只能出现在开始框架和结束帧时间段之外。

在保护模式和对[**DecodeBeginFrame**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_decodebeginframe)的调用中，Direct3D 运行时设置或更改[**D3DDDIARG\_DecodeBeginFrame**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_decodebeginframe)结构的**pPVPSetKey**成员指向的变量中的 DirectX VA 内容密钥。 解码设备使用此密钥在此和后续帧上传输压缩的 DirectX VA 缓冲区。

**请注意**   Direct3D 运行时仅将**pPVPSetKey**指针设置为更改或设置密钥。 为了使以前设置的密钥保持使用，运行时将指针设置为**NULL** ，以避免可能需要重新加载相同键的时间。 该驱动程序不会消除冗余设置。 解码器应用程序必须避免冗余设置。

 

设置用于解码操作的呈现目标图面后，用户模式显示驱动程序可以接收对其[**DecodeExecute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_decodeexecute)函数的调用，以执行开始帧时间和结束帧时间段之间的视频解码操作。

在对[**DecodeExecute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_decodeexecute)的调用中，并非 PCOMPRESSEDBUFFERS [ **\_D3DDDIARG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_decodeexecute)结构的 DecodeExecute\_**成员指定**的每个解码 GUID 都使用 hDecode 的**D3DDDIARG 数组的** **CompressedBufferType** [ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvaddi_decodebufferdesc)成员中指定的所有缓冲区类型。 例如，切片控制（D3DDDIFMT\_SLICECONTROLDATA）、反量化（D3DDDIFMT\_INVERSEQUANTIZATIONDATA）和位流（D3DDDIFMT\_BITSTREAMDATA）缓冲区只需要进行可变长度解码（VLD）处理，而的 deblocking 控件缓冲区（D3DDDIFMT\_DEBLOCKINGDATA）不会全部使用。

在保护模式下，为带有内容密钥的受保护传输加密的缓冲区包含指向其缓冲区说明符中的初始计数器值的指针（即，在**pCipherCounter**成员的[**DXVADDI\_DECODEBUFFERDESC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvaddi_decodebufferdesc)结构指向的变量中）。 每次调用用户模式显示驱动程序的[**DecodeExecute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_decodeexecute)函数时，都必须在**DecodeExecute**使用缓冲区中的数据进行解码操作之前，执行此类缓冲区的受保护传输。 但是，不存在任何计划来加密除残留差异（D3DDDIFMT\_RESIDUALDIFFERENCEDATA）和位流（D3DDDIFMT\_BITSTREAMDATA）类型之外的 DirectX VA 压缩缓冲区。

 

 





