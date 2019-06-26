---
title: 排除延迟上下文的 DDI 函数
description: 排除延迟上下文的 DDI 函数
ms.assetid: f6e7898a-7fb8-4a70-ab2e-3372a28db6f4
keywords:
- Direct3D 版本显示 11 WDK Windows 7，延迟的上下文中，不包括 DDI 函数
- Direct3D 11 版 WDK Windows Server 2008 R2 显示，延迟的上下文，不包括 DDI 函数
- 显示延迟的上下文 WDK Windows 7，不包括 DDI 函数
- 显示延迟的上下文 WDK Windows Server 2008 R2，请排除 DDI 函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fee0417d08b59cca12f90d766d993ad0e949c000
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370991"
---
# <a name="excluding-ddi-functions-for-deferred-contexts"></a>排除延迟上下文的 DDI 函数


本部分仅适用于 Windows 7 及更高版本、 和 Windows Server 2008 R2 和更高版本的 Windows 操作系统。

当 Microsoft Direct3D 运行时调用用户模式显示驱动程序[ **CreateDeferredContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createdeferredcontext)函数来创建推迟的上下文，该驱动程序提供了运行时可调用的函数为此，延迟的上下文。 该驱动程序填充的成员[ **D3D11DDI\_DEVICEFUNCS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d11ddi_devicefuncs)结构**p11ContextFuncs**隶属[ **D3D11DDIARG\_CREATEDEFERREDCONTEXT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d11ddiarg_createdeferredcontext)结构指向。 该驱动程序提供了驱动程序为推迟的上下文的函数的一个子集进行即时上下文。

该驱动程序通过设置以下成员不包括用于延迟上下文的许多函数[ **D3D11DDI\_DEVICEFUNCS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d11ddi_devicefuncs)或[ **D3D11\_1DDI\_DEVICEFUNCS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d11_1ddi_devicefuncs)到**NULL**:

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

 

 





