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
ms.openlocfilehash: 4eb4af9bebe2b5fe0a66312e9898c0ef74e87126
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826033"
---
# <a name="providing-capabilities-for-directx-va-20-extension-modes"></a>提供 DirectX VA 2.0 扩展模式的功能


调用[**GetCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)函数时，用户模式显示驱动程序会根据请求类型（在*pData*参数指向的[**D3DDDIARG\_GetCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)结构的**类型**成员中指定）为 DirectX VA 2.0 扩展模式提供以下功能：

<span id="D3DDDICAPS_GETEXTENSIONGUIDCOUNT_and_D3DDDICAPS_GETEXTENSIONGUIDS_request_types"></span><span id="d3dddicaps_getextensionguidcount_and_d3dddicaps_getextensionguids_request_types"></span><span id="D3DDDICAPS_GETEXTENSIONGUIDCOUNT_AND_D3DDDICAPS_GETEXTENSIONGUIDS_REQUEST_TYPES"></span>D3DDDICAPS\_GETEXTENSIONGUIDCOUNT 和 D3DDDICAPS\_GETEXTENSIONGUIDS 请求类型  
用户模式显示驱动程序返回其支持的扩展模式的 Guid 列表。 运行时首先请求支持的 Guid 的数目，并请求提供支持的 Guid 列表的请求。

<span id="D3DDDICAPS_GETEXTENSIONCAPS_request_type"></span><span id="d3dddicaps_getextensioncaps_request_type"></span><span id="D3DDDICAPS_GETEXTENSIONCAPS_REQUEST_TYPE"></span>D3DDDICAPS\_GETEXTENSIONCAPS 请求类型  
用户模式显示驱动程序支持的每个扩展模式可以具有独特的功能。 用户模式显示驱动程序在传递 D3DDDICAPS\_GETEXTENSIONCAPS 请求类型时返回那些功能。 Direct3D 运行时为扩展 GUID 指定[**DXVADDI\_QUERYEXTENSIONCAPSINPUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvaddi_queryextensioncapsinput)结构，以便在[**D3DDDIARG\_GETCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)的**pInfo**成员指向的变量中检索的功能。 用户模式显示驱动程序返回**pData**成员 D3DDDIARG\_GETCAPS 指向的私有结构中的扩展 GUID 功能。

 

 





