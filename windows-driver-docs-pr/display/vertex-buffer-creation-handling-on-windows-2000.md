---
title: Windows 2000 上的顶点缓冲区创建处理
description: Windows 2000 上的顶点缓冲区创建处理
ms.assetid: 4155a4c6-cbac-4a75-8ddf-5983fe5099c6
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示、 顶点缓冲区、 创建处理
- 顶点缓冲区 WDK DirectX 8.0，Windows 2000 上处理的创建
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fdb5c445d2547351318cf2c365cf6c602966725d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565051"
---
# <a name="vertex-buffer-creation-handling-on-windows-2000"></a>Windows 2000 上的顶点缓冲区创建处理


## <span id="ddk_vertex_buffer_creation_handling_on_windows_2000_gg"></span><span id="DDK_VERTEX_BUFFER_CREATION_HANDLING_ON_WINDOWS_2000_GG"></span>


在 DirectX 8.0 纹理变 DirectX 7.0 中，可以管理顶点 （和索引） 的缓冲区。 也就是说，顶点缓冲区的系统内存副本维护在所有时间和实际需要该顶点缓冲区时，仅将分配的视频内存副本。

如果该驱动程序不会分配视频内存中的顶点缓冲区，但相反，需要运行时无法分配在系统内存中的缓冲区，它不应返回 DDHAL\_驱动程序\_NOTHANDLED 而是应返回 DDHAL\_驱动程序\_已处理，并通过设置指示故障**ddRVal** E 的\_失败。 如果该驱动程序返回 DDHAL\_驱动程序\_NOTHANDLED，在运行时尝试从堆返回的驱动程序的视频内存分配图面。 这可能会失败，并向应用程序或分配的本地或非本地的视频内存 （这不是意图） 的图面中的结果返回错误。

因此，如果您想要分配顶点缓冲区代表你的系统内存中的运行时，将**ddRVal**到 E\_失败，并且返回 DDHAL\_驱动程序\_已处理。

 

 





