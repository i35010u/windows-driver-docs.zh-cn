---
title: 提供 DirectX VA 2.0 扩展模式的功能
description: 提供 DirectX VA 2.0 扩展模式的功能
keywords:
- DirectX 视频加速 WDK 显示，扩展支持
- 视频加速 WDK DirectX，扩展支持
- VA WDK DirectX，扩展支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cbc74b6866424a7c09d84f71782324145445e6c6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792939"
---
# <a name="providing-capabilities-for-directx-va-20-extension-modes"></a>提供 DirectX VA 2.0 扩展模式的功能


调用 [**GetCaps**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)函数时，用户模式显示驱动程序将基于请求类型为 DirectX VA 2.0 扩展模式提供以下功能， (该类型在 *pData* 参数指向) 的 [**D3DDDIARG \_ GetCaps**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)结构的 **type** 成员中指定：

<span id="D3DDDICAPS_GETEXTENSIONGUIDCOUNT_and_D3DDDICAPS_GETEXTENSIONGUIDS_request_types"></span><span id="d3dddicaps_getextensionguidcount_and_d3dddicaps_getextensionguids_request_types"></span><span id="D3DDDICAPS_GETEXTENSIONGUIDCOUNT_AND_D3DDDICAPS_GETEXTENSIONGUIDS_REQUEST_TYPES"></span>D3DDDICAPS \_ GETEXTENSIONGUIDCOUNT 和 D3DDDICAPS \_ GETEXTENSIONGUIDS 请求类型  
用户模式显示驱动程序返回其支持的扩展模式的 Guid 列表。 运行时首先请求支持的 Guid 的数目，并请求提供支持的 Guid 列表的请求。

<span id="D3DDDICAPS_GETEXTENSIONCAPS_request_type"></span><span id="d3dddicaps_getextensioncaps_request_type"></span><span id="D3DDDICAPS_GETEXTENSIONCAPS_REQUEST_TYPE"></span>D3DDDICAPS \_ GETEXTENSIONCAPS 请求类型  
用户模式显示驱动程序支持的每个扩展模式可以具有独特的功能。 用户模式显示驱动程序在 \_ 传递 D3DDDICAPS GETEXTENSIONCAPS 请求类型时返回这些功能。 Direct3D 运行时为扩展 GUID 指定 [**DXVADDI \_ QUERYEXTENSIONCAPSINPUT**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvaddi_queryextensioncapsinput)结构，以便在 [**D3DDDIARG \_ GETCAPS**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)的 **pInfo** 成员指向的变量中检索的功能。 用户模式显示驱动程序返回 D3DDDIARG GETCAPS 的 **pData** 成员指向的私有结构中的扩展 GUID 功能 \_ 。

 

