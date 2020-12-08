---
title: Windows 2000 上的顶点缓冲区创建处理
description: Windows 2000 上的顶点缓冲区创建处理
keywords:
- DirectX 8.0 发行说明了 WDK Windows 2000 显示、顶点缓冲区、创建处理
- 顶点缓冲 WDK DirectX 8.0，在 Windows 2000 上创建处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2cf99c61490ac8c86fdad4cdf1827cf153b87274
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798227"
---
# <a name="vertex-buffer-creation-handling-on-windows-2000"></a>Windows 2000 上的顶点缓冲区创建处理


## <span id="ddk_vertex_buffer_creation_handling_on_windows_2000_gg"></span><span id="DDK_VERTEX_BUFFER_CREATION_HANDLING_ON_WINDOWS_2000_GG"></span>


在 DirectX 8.0 中，可以对顶点 (和索引) 缓存进行管理，因为它是在 DirectX 7.0 中进行的。 也就是说，将始终维护顶点缓冲区的系统内存复制，并且仅当实际需要该顶点缓冲区时才会分配视频内存副本。

如果驱动程序没有在视频内存中分配顶点缓冲区，而是要求运行时在系统内存中分配缓冲区，则它不应返回 DDHAL \_ driver NOTHANDLED， \_ 而应返回已处理的 DDHAL \_ 驱动程序 \_ ，并通过将 **ddRVal** 设置为 "失败" 来指示故障 \_ 。 如果驱动程序返回 DDHAL \_ driver \_ NOTHANDLED，则运行时将尝试从驱动程序返回的视频内存堆中分配图面。 这可能会导致应用程序失败并向应用程序返回错误，或导致在本地或非本地视频内存中分配表面 (这并非) 目的。

因此，如果希望运行时代表您在系统内存中分配一个顶点缓冲区，请将 **ddRVal** 设置为 E， \_ 并返回 DDHAL \_ 驱动程序已 \_ 处理。

 

 





