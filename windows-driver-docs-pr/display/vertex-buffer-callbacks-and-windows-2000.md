---
title: 顶点缓冲区回调和 Windows 2000
description: 顶点缓冲区回调和 Windows 2000
ms.assetid: d3b92bc9-d4f1-4079-86f1-53c04bcab443
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，顶点缓冲区回调
- 顶点缓冲区 WDK DirectX 8.0、 回调和 Windows 2000
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6091eb4bb6539f35d864913ec7076b5c1d848b9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542030"
---
# <a name="vertex-buffer-callbacks-and-windows-2000"></a>顶点缓冲区回调和 Windows 2000


## <span id="ddk_vertex_buffer_callbacks_and_windows_2000_gg"></span><span id="DDK_VERTEX_BUFFER_CALLBACKS_AND_WINDOWS_2000_GG"></span>


在初始的零售版本的 Windows 2000 上的 DirectX 7.0 可以防止驱动程序的执行由运行时调用的缓冲区 （D3D 缓冲区） 回调。 这样可以防止驱动程序的顶点缓冲区创建请求的通知，并且因此，可以创建或在此方案中使用任何视频内存或非本地的视频内存缓冲区。 DirectX 8.0 和使用 DirectX 8.0 DirectX 7.0 附带的版本中启用的视频内存顶点缓冲区。 此外，Windows 2000 Service Pack 1 (SP1) 使视频内存顶点缓冲区和所有将来版本的 Windows 2000 将使视频内存顶点缓冲区。 但是，没有解决方法若要启用 Windows 2000 上的视频内存顶点缓冲区而不安装 DirectX 8.0。

 

 





