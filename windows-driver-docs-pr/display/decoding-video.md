---
title: 解码视频
description: 解码视频
keywords:
- 视频解码 WDK DirectX VA，关于解码视频
- 解码视频 WDK DirectX VA，关于解码视频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cfa134f73919ac9500d5a203928f002ed813cbfc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809621"
---
# <a name="decoding-video"></a>解码视频


Microsoft Direct3D runtime 调用用户模式显示驱动程序的 [**DecodeBeginFrame**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_decodebeginframe) 和 [**DecodeEndFrame**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_decodeendframe) 函数，以指示这些函数调用之间的时间段，用户模式显示驱动程序可以解码视频。 在用户模式显示驱动程序可以执行任何视频解码操作之前，Microsoft Direct3D 运行时必须调用用户模式显示驱动程序的 [**SetDecodeRenderTarget**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_setdecoderendertarget) 函数，以便为这些解码操作设置呈现目标图面。 但是，对 **SetDecodeRenderTarget** 的调用只能出现在开始框架和结束帧时间段之外。

在保护模式和对 [**DecodeBeginFrame**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_decodebeginframe)的调用中，Direct3D 运行时在 [**D3DDDIARG \_ DecodeBeginFrame**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_decodebeginframe)结构的 **pPVPSetKey** 成员指向的变量中设置或更改 DirectX VA 内容密钥。 解码设备使用此密钥在此和后续帧上传输压缩的 DirectX VA 缓冲区。

**注意**   Direct3D 运行时仅将 **pPVPSetKey** 指针设置为更改或设置密钥。 为了使以前设置的密钥保持使用，运行时将指针设置为 **NULL** ，以避免可能需要重新加载相同键的时间。 该驱动程序不会消除冗余设置。 解码器应用程序必须避免冗余设置。

 

设置用于解码操作的呈现目标图面后，用户模式显示驱动程序可以接收对其 [**DecodeExecute**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_decodeexecute) 函数的调用，以执行开始帧时间和结束帧时间段之间的视频解码操作。

在对 [**DecodeExecute**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_decodeexecute)**的调用** 中，并非 pCompressedBuffers D3DDDIARG 结构 DecodeExecute 成员的 **CompressedBufferType** 成员中指定的所有缓冲区类型都用于 hDecode D3DDDIARG **的 DECODEEXECUTE 成员** 指定 [**的每 \_**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvaddi_decodebufferdesc)个解码 GUID [**\_**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_decodeexecute) \_ 。 例如，切片控件 (D3DDDIFMT \_ SLICECONTROLDATA) 、反量化 (D3DDDIFMT \_ INVERSEQUANTIZATIONDATA) 和位流 (D3DDDIFMT \_ BITSTREAMDATA) 仅限可变长度解码 (VLD) 处理，且不会使用 deblocking 控件缓冲区 (D3DDDIFMT \_ DEBLOCKINGDATA) ，根本不使用。

在保护模式下，为带有内容密钥的受保护传输加密的缓冲区包含指向其缓冲区说明符中的初始计数器值的指针， (即，在 [**DXVADDI \_ DECODEBUFFERDESC**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvaddi_decodebufferdesc)结构的 **pCipherCounter** 成员指向) 的变量中。 每次调用用户模式显示驱动程序的 [**DecodeExecute**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_decodeexecute) 函数时，都必须在 **DecodeExecute** 使用缓冲区中的数据进行解码操作之前，执行此类缓冲区的受保护传输。 但是，不存在任何计划，因此无法将除残留差异 (D3DDDIFMT \_ RESIDUALDIFFERENCEDATA) 和位流 (D3DDDIFMT \_ BITSTREAMDATA) 类型之外的 DirectX VA 压缩缓冲类型加密。

 

