---
title: 同步视频解码操作
description: 同步视频解码操作
ms.assetid: 4c88bf8f-0f10-4281-b856-a0e056d69d0e
keywords:
- 视频解码 WDK DirectX VA，同步
- 解码视频 WDK DirectX VA，同步
- 同步 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b10c168597a872aff9adea873cf955b5ac92363f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825515"
---
# <a name="synchronizing-video-decode-operations"></a>同步视频解码操作


## <span id="ddk_synchronizing_video_decode_operations_gg"></span><span id="DDK_SYNCHRONIZING_VIDEO_DECODE_OPERATIONS_GG"></span>


DirectX VA 2.0 的同步机制经过了1.0 版本的改进，更类似于 Microsoft Direct3D 操作所使用的同步机制。

在 DirectX VA 1.0 中，同步主要由解码器执行。 在解码器可以使用压缩的缓冲区之前，它会调用[*DdMoCompQueryStatus*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_querystatus)函数来确定缓冲区是否可供使用（即，硬件未访问缓冲区）。 如果缓冲区不可用，则解码器必须睡眠、轮询或执行其他操作。

DirectX VA 2.0 使用 Direct3D 已在顶点缓冲区和索引缓冲区上使用的同步模型。 在 DirectX VA 2.0 中，通过解码器锁定压缩缓冲区来执行同步。 如果用户模式显示驱动程序尝试锁定压缩缓冲区，并且缓冲区正在使用中，则驱动程序可能会导致锁定或重命名缓冲区失败。 用户模式显示驱动程序请求当驱动程序在对[**pfnLockCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lockcb)函数的调用中设置[**D3DDDICB\_LOCKFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddicb_lockflags)结构的**丢弃**成员时，视频内存管理器会重命名缓冲区。 如果用户模式显示驱动程序重命名了缓冲区，则驱动程序将返回一个指向备用缓冲区的指针，使解码器可以继续而不会被阻止。

通常，对于 DirectX VA 2.0，仅当硬件可以直接使用压缩缓冲区而无需额外的缓冲副本时，同步才会出现问题。

 

 





