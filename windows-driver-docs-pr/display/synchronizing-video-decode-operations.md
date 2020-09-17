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
ms.openlocfilehash: 7817a5a07f0c474366c3f6e4dec985573b6c42f0
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715986"
---
# <a name="synchronizing-video-decode-operations"></a>同步视频解码操作


## <span id="ddk_synchronizing_video_decode_operations_gg"></span><span id="DDK_SYNCHRONIZING_VIDEO_DECODE_OPERATIONS_GG"></span>


DirectX VA 2.0 的同步机制经过了1.0 版本的改进，更类似于 Microsoft Direct3D 操作所使用的同步机制。

在 DirectX VA 1.0 中，同步主要由解码器执行。 在解码器可以使用压缩的缓冲区之前，它会调用 [*DdMoCompQueryStatus*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_querystatus) 函数来确定缓冲区是否可用于 (也就是说，硬件不会访问缓冲区) 。 如果缓冲区不可用，则解码器必须睡眠、轮询或执行其他操作。

DirectX VA 2.0 使用 Direct3D 已在顶点缓冲区和索引缓冲区上使用的同步模型。 在 DirectX VA 2.0 中，通过解码器锁定压缩缓冲区来执行同步。 如果用户模式显示驱动程序尝试锁定压缩缓冲区，并且缓冲区正在使用中，则驱动程序可能会导致锁定或重命名缓冲区失败。 用户模式显示驱动程序请求当驱动程序在对[**pfnLockCb**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lockcb)函数的调用中设置[**D3DDDICB \_ LOCKFLAGS**](/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddicb_lockflags)结构的**丢弃**成员时，视频内存管理器会重命名缓冲区。 如果用户模式显示驱动程序重命名了缓冲区，则驱动程序将返回一个指向备用缓冲区的指针，使解码器可以继续而不会被阻止。

通常，对于 DirectX VA 2.0，仅当硬件可以直接使用压缩缓冲区而无需额外的缓冲副本时，同步才会出现问题。

 

