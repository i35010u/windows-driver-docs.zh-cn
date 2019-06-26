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
ms.openlocfilehash: a9d122f7e31ef3f9104638deda2d8b8048bf8cee
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383902"
---
# <a name="providing-capabilities-for-directx-va-20-extension-modes"></a>提供 DirectX VA 2.0 扩展模式的功能


当其[ **GetCaps** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)函数被调用时，用户模式显示驱动程序提供以下功能的 DirectX VA 2.0 扩展模式基于请求类型 (中指定**类型**的成员[ **D3DDDIARG\_GETCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)结构*pData*参数指向):

<span id="D3DDDICAPS_GETEXTENSIONGUIDCOUNT_and_D3DDDICAPS_GETEXTENSIONGUIDS_request_types"></span><span id="d3dddicaps_getextensionguidcount_and_d3dddicaps_getextensionguids_request_types"></span><span id="D3DDDICAPS_GETEXTENSIONGUIDCOUNT_AND_D3DDDICAPS_GETEXTENSIONGUIDS_REQUEST_TYPES"></span>D3DDDICAPS\_GETEXTENSIONGUIDCOUNT 和 D3DDDICAPS\_GETEXTENSIONGUIDS 请求类型  
用户模式显示驱动程序返回数和它支持的扩展模式下的 Guid 的列表。 在运行时首先请求支持 Guid 后, 跟一系列受支持的 Guid 的请求数。

<span id="D3DDDICAPS_GETEXTENSIONCAPS_request_type"></span><span id="d3dddicaps_getextensioncaps_request_type"></span><span id="D3DDDICAPS_GETEXTENSIONCAPS_REQUEST_TYPE"></span>D3DDDICAPS\_GETEXTENSIONCAPS 请求类型  
每个用户模式显示驱动程序支持的扩展模式可具有独特的功能。 用户模式显示驱动程序返回这些功能时 D3DDDICAPS\_传递 GETEXTENSIONCAPS 请求类型。 Direct3D 运行时指定[ **DXVADDI\_QUERYEXTENSIONCAPSINPUT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_dxvaddi_queryextensioncapsinput)扩展要检索的变量中的功能 GUID 结构的**pInfo**的成员[ **D3DDDIARG\_GETCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)指向。 用户模式显示驱动程序返回功能中专用的扩展 GUID 结构的**pData** D3DDDIARG 成员\_GETCAPS 指向。

 

 





