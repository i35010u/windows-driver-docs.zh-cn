---
title: 顶点缓冲区回调和 Windows 2000
description: 顶点缓冲区回调和 Windows 2000
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示、顶点缓冲区、回调
- 顶点缓冲 WDK DirectX 8.0、回调和 Windows 2000
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0bee6ef04f3045c298d9b93e694bafa88b4af6a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798231"
---
# <a name="vertex-buffer-callbacks-and-windows-2000"></a>顶点缓冲区回调和 Windows 2000


## <span id="ddk_vertex_buffer_callbacks_and_windows_2000_gg"></span><span id="DDK_VERTEX_BUFFER_CALLBACKS_AND_WINDOWS_2000_GG"></span>


Windows 2000 的初始零售版中的 DirectX 7.0 可防止在运行时调用驱动程序的执行缓冲区 (D3D 缓冲区) 回调。 这可以防止驱动程序收到有关顶点缓冲区创建请求的通知，因此，在此方案中无法创建或使用任何视频内存或非本地视频内存缓冲区。 在 directx 8.0 和 directx 8.0 随附的 DirectX 7.0 版本中启用了视频内存顶点缓冲区。 此外，Windows 2000 Service Pack 1 (SP1) 启用视频内存顶点缓冲区，并且 Windows 2000 的所有未来版本都将启用视频内存顶点缓冲区。 但是，除了安装 DirectX 8.0 外，不能使用 Windows 2000 上的视频内存顶点缓冲区。

 

 





