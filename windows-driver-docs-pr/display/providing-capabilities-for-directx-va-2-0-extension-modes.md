---
title: 提供 DirectX VA 2.0 扩展模式的功能
description: 提供 DirectX VA 2.0 扩展模式的功能
ms.assetid: 86283ac8-a56c-4da9-a3ef-6f4d694130a7
keywords:
- DirectX 视频加速 WDK 显示，扩展支持
- 视频加速 WDK DirectX，扩展支持
- VA WDK DirectX，扩展支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dfdbfa68ea84703031c1505a2cd798d12feffce8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370169"
---
# <a name="providing-capabilities-for-directx-va-20-extension-modes"></a>提供 DirectX VA 2.0 扩展模式的功能


当其[ **GetCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff566762)函数被调用时，用户模式显示驱动程序提供以下功能的 DirectX VA 2.0 扩展模式基于请求类型 (中指定**类型**的成员[ **D3DDDIARG\_GETCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff543148)结构*pData*参数指向):

<span id="D3DDDICAPS_GETEXTENSIONGUIDCOUNT_and_D3DDDICAPS_GETEXTENSIONGUIDS_request_types"></span><span id="d3dddicaps_getextensionguidcount_and_d3dddicaps_getextensionguids_request_types"></span><span id="D3DDDICAPS_GETEXTENSIONGUIDCOUNT_AND_D3DDDICAPS_GETEXTENSIONGUIDS_REQUEST_TYPES"></span>D3DDDICAPS\_GETEXTENSIONGUIDCOUNT 和 D3DDDICAPS\_GETEXTENSIONGUIDS 请求类型  
用户模式显示驱动程序返回数和它支持的扩展模式下的 Guid 的列表。 在运行时首先请求支持 Guid 后, 跟一系列受支持的 Guid 的请求数。

<span id="D3DDDICAPS_GETEXTENSIONCAPS_request_type"></span><span id="d3dddicaps_getextensioncaps_request_type"></span><span id="D3DDDICAPS_GETEXTENSIONCAPS_REQUEST_TYPE"></span>D3DDDICAPS\_GETEXTENSIONCAPS 请求类型  
每个用户模式显示驱动程序支持的扩展模式可具有独特的功能。 用户模式显示驱动程序返回这些功能时 D3DDDICAPS\_传递 GETEXTENSIONCAPS 请求类型。 Direct3D 运行时指定[ **DXVADDI\_QUERYEXTENSIONCAPSINPUT** ](https://msdn.microsoft.com/library/windows/hardware/ff562926)扩展要检索的变量中的功能 GUID 结构的**pInfo**的成员[ **D3DDDIARG\_GETCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff543148)指向。 用户模式显示驱动程序返回功能中专用的扩展 GUID 结构的**pData** D3DDDIARG 成员\_GETCAPS 指向。

 

 





