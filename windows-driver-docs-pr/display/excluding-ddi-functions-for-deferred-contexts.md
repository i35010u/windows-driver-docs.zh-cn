---
title: 对于延迟的上下文中不包括 DDI 函数
description: 对于延迟的上下文中不包括 DDI 函数
ms.assetid: f6e7898a-7fb8-4a70-ab2e-3372a28db6f4
keywords:
- Direct3D 版本显示 11 WDK Windows 7，延迟的上下文中，不包括 DDI 函数
- Direct3D 11 版 WDK Windows Server 2008 R2 显示，延迟的上下文，不包括 DDI 函数
- 显示延迟的上下文 WDK Windows 7，不包括 DDI 函数
- 显示延迟的上下文 WDK Windows Server 2008 R2，请排除 DDI 函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8a7532626cab62b764fff86c4b813f36a74de0f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520956"
---
# <a name="excluding-ddi-functions-for-deferred-contexts"></a>对于延迟的上下文中不包括 DDI 函数


本部分仅适用于 Windows 7 及更高版本、 和 Windows Server 2008 R2 和更高版本的 Windows 操作系统。

当 Microsoft Direct3D 运行时调用用户模式显示驱动程序[ **CreateDeferredContext** ](https://msdn.microsoft.com/library/windows/hardware/ff540622)函数来创建推迟的上下文，该驱动程序提供了运行时可调用的函数为此，延迟的上下文。 该驱动程序填充的成员[ **D3D11DDI\_DEVICEFUNCS** ](https://msdn.microsoft.com/library/windows/hardware/ff542141)结构**p11ContextFuncs**隶属[ **D3D11DDIARG\_CREATEDEFERREDCONTEXT** ](https://msdn.microsoft.com/library/windows/hardware/ff542044)结构指向。 该驱动程序提供了驱动程序为推迟的上下文的函数的一个子集进行即时上下文。

该驱动程序通过设置以下成员不包括用于延迟上下文的许多函数[ **D3D11DDI\_DEVICEFUNCS** ](https://msdn.microsoft.com/library/windows/hardware/ff542141)或[ **D3D11\_1DDI\_DEVICEFUNCS** ](https://msdn.microsoft.com/library/windows/hardware/hh406443)到**NULL**:

```cpp
typedef struct D3D11DDI_DEVICEFUNCS {
...
  PFND3D10DDI_RESOURCEMAP  pfnStagingResourceMap;
  PFND3D10DDI_RESOURCEUNMAP  pfnStagingResourceUnmap;
  PFND3D10DDI_QUERYGETDATA  pfnQueryGetData;
  PFND3D10DDI_FLUSH  pfnFlush;
  PFND3D10DDI_RESOURCEMAP  pfnResourceMap;
  PFND3D10DDI_RESOURCEUNMAP  pfnResourceUnmap;
  PFND3D10DDI_RESOURCEISSTAGINGBUSY  pfnResourceIsStagingBusy;
  PFND3D11DDI_CALCPRIVATERESOURCESIZE  pfnCalcPrivateResourceSize;
  PFND3D10DDI_CALCPRIVATEOPENEDRESOURCESIZE  pfnCalcPrivateOpenedResourceSize;
  PFND3D10DDI_OPENRESOURCE  fnOpenResource;
  PFND3D11DDI_CALCPRIVATESHADERRESOURCEVIEWSIZE  pfnCalcPrivateShaderResourceViewSize;
  PFND3D10DDI_CALCPRIVATERENDERTARGETVIEWSIZE  pfnCalcPrivateRenderTargetViewSize;
  PFND3D11DDI_CALCPRIVATEDEPTHSTENCILVIEWSIZE  pfnCalcPrivateDepthStencilViewSize;
  PFND3D10DDI_CALCPRIVATEELEMENTLAYOUTSIZE  pfnCalcPrivateElementLayoutSize;
  PFND3D10_1DDI_CALCPRIVATEBLENDSTATESIZE  pfnCalcPrivateBlendStateSize;
  PFND3D10DDI_CALCPRIVATEDEPTHSTENCILSTATESIZE  pfnCalcPrivateDepthStencilStateSize;
  PFND3D10DDI_CALCPRIVATERASTERIZERSTATESIZE  pfnCalcPrivateRasterizerStateSize;
  PFND3D10DDI_CALCPRIVATESHADERSIZE  pfnCalcPrivateShaderSize;
  PFND3D11DDI_CALCPRIVATEGEOMETRYSHADERWITHSTREAMOUTPUT  pfnCalcPrivateGeometryShaderWithStreamOutput;
  PFND3D10DDI_CALCPRIVATESAMPLERSIZE  pfnCalcPrivateSamplerSize;
  PFND3D10DDI_CALCPRIVATEQUERYSIZE  pfnCalcPrivateQuerySize;
  PFND3D10DDI_CHECKFORMATSUPPORT  pfnCheckFormatSupport;
  PFND3D10DDI_CHECKMULTISAMPLEQUALITYLEVELS  pfnCheckMultisampleQualityLevels;
  PFND3D10DDI_CHECKCOUNTERINFO  pfnCheckCounterInfo;
  PFND3D10DDI_CHECKCOUNTER  pfnCheckCounter;
  PFND3D11DDI_CHECKDEFERREDCONTEXTHANDLESIZES  pfnCheckDeferredContextHandleSizes;
  PFND3D11DDI_CALCDEFERREDCONTEXTHANDLESIZE  pfnCalcDeferredContextHandleSize;
  PFND3D11DDI_CALCPRIVATEDEFERREDCONTEXTSIZE  pfnCalcPrivateDeferredContextSize;
  PFND3D11DDI_CREATEDEFERREDCONTEXT  pfnCreateDeferredContext;
  PFND3D11DDI_CALCPRIVATECOMMANDLISTSIZE  pfnCalcPrivateCommandListSize;
  PFND3D11DDI_CALCPRIVATETESSELLATIONSHADERSIZE  pfnCalcPrivateTessellationShaderSize;
  PFND3D11DDI_CALCPRIVATEUNORDEREDACCESSVIEWSIZE  pfnCalcPrivateUnorderedAccessViewSize;
  PFND3D11DDI_SETRESOURCEMINLOD  pfnSetResourceMinLOD;
} D3D11DDI_DEVICEFUNCS;
```

```cpp
typedef struct D3D11_1DDI_DEVICEFUNCS {
...
  PFND3D10DDI_RESOURCEMAP  pfnStagingResourceMap;
  PFND3D10DDI_RESOURCEUNMAP  pfnStagingResourceUnmap;
  PFND3D10DDI_QUERYGETDATA  pfnQueryGetData;
  PFND3D11_1DDI_FLUSH  pfnFlush;
  PFND3D10DDI_RESOURCEMAP  pfnResourceMap;
  PFND3D10DDI_RESOURCEUNMAP  pfnResourceUnmap;
  PFND3D10DDI_RESOURCEISSTAGINGBUSY  pfnResourceIsStagingBusy;
  PFND3D11DDI_CALCPRIVATERESOURCESIZE  pfnCalcPrivateResourceSize;
  PFND3D10DDI_CALCPRIVATEOPENEDRESOURCESIZE  pfnCalcPrivateOpenedResourceSize;
  PFND3D10DDI_OPENRESOURCE  fnOpenResource;
  PFND3D11DDI_CALCPRIVATESHADERRESOURCEVIEWSIZE  pfnCalcPrivateShaderResourceViewSize;
  PFND3D10DDI_CALCPRIVATERENDERTARGETVIEWSIZE  pfnCalcPrivateRenderTargetViewSize;
  PFND3D11DDI_CALCPRIVATEDEPTHSTENCILVIEWSIZE  pfnCalcPrivateDepthStencilViewSize;
  PFND3D10DDI_CALCPRIVATEELEMENTLAYOUTSIZE  pfnCalcPrivateElementLayoutSize;
  PFND3D11_1DDI_CALCPRIVATEBLENDSTATESIZE  pfnCalcPrivateBlendStateSize;
  PFND3D10DDI_CALCPRIVATEDEPTHSTENCILSTATESIZE  pfnCalcPrivateDepthStencilStateSize;
  PFND3D11_1DDI_CALCPRIVATERASTERIZERSTATESIZE  pfnCalcPrivateRasterizerStateSize;
  PFND3D11_1DDI_CALCPRIVATESHADERSIZE  pfnCalcPrivateShaderSize;
  PFND3D11_1DDI_CALCPRIVATEGEOMETRYSHADERWITHSTREAMOUTPUT  pfnCalcPrivateGeometryShaderWithStreamOutput;
  PFND3D10DDI_CALCPRIVATESAMPLERSIZE  pfnCalcPrivateSamplerSize;
  PFND3D10DDI_CALCPRIVATEQUERYSIZE  pfnCalcPrivateQuerySize;
  PFND3D10DDI_CHECKFORMATSUPPORT  pfnCheckFormatSupport;
  PFND3D10DDI_CHECKMULTISAMPLEQUALITYLEVELS  pfnCheckMultisampleQualityLevels;
  PFND3D10DDI_CHECKCOUNTERINFO  pfnCheckCounterInfo;
  PFND3D10DDI_CHECKCOUNTER  pfnCheckCounter;
  PFND3D11DDI_CHECKDEFERREDCONTEXTHANDLESIZES  pfnCheckDeferredContextHandleSizes;
  PFND3D11DDI_CALCDEFERREDCONTEXTHANDLESIZE  pfnCalcDeferredContextHandleSize;
  PFND3D11DDI_CALCPRIVATEDEFERREDCONTEXTSIZE  pfnCalcPrivateDeferredContextSize;
  PFND3D11DDI_CREATEDEFERREDCONTEXT  pfnCreateDeferredContext;
  PFND3D11DDI_CALCPRIVATECOMMANDLISTSIZE  pfnCalcPrivateCommandListSize;
  PFND3D11_1DDI_CALCPRIVATETESSELLATIONSHADERSIZE  pfnCalcPrivateTessellationShaderSize;
  PFND3D11DDI_CALCPRIVATEUNORDEREDACCESSVIEWSIZE  pfnCalcPrivateUnorderedAccessViewSize;
  PFND3D11DDI_SETRESOURCEMINLOD  pfnSetResourceMinLOD;
} D3D11DDI_DEVICEFUNCS;
```

 

 





