---
title: 排除延迟上下文的 DDI 函数
description: 排除延迟上下文的 DDI 函数
ms.assetid: f6e7898a-7fb8-4a70-ab2e-3372a28db6f4
keywords:
- Direct3D 版本 11 WDK Windows 7 显示，延迟上下文，不包括 DDI 函数
- Direct3D 版本 11 WDK Windows Server 2008 R2 显示，延迟上下文，不包括 DDI 函数
- 延迟的上下文 WDK Windows 7 显示，不包括 DDI 函数
- 延迟的上下文 WDK Windows Server 2008 R2 显示，不包括 DDI 函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca7ae43a6e11a566ebd9ef494d184f36012f7a73
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066730"
---
# <a name="excluding-ddi-functions-for-deferred-contexts"></a>排除延迟上下文的 DDI 函数


本部分仅适用于 Windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

当 Microsoft Direct3D 运行时调用用户模式显示驱动程序的 [**CreateDeferredContext**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createdeferredcontext) 函数来创建延迟的上下文时，驱动程序将提供运行时可为该延迟上下文调用的函数。 驱动程序将填充[**D3D11DDIARG \_ CREATEDEFERREDCONTEXT**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddiarg_createdeferredcontext)结构的**P11ContextFuncs**成员指向的[**D3D11DDI \_ DEVICEFUNCS**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddi_devicefuncs)结构的成员。 驱动程序只为延迟上下文提供一小部分功能，因为驱动程序会直接执行上下文。

驱动程序通过将 [**D3D11DDI \_ DEVICEFUNCS**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddi_devicefuncs) 或 [**D3D11 \_ 1DDI \_ DEVICEFUNCS**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddi_devicefuncs) 的以下成员设置为 **NULL**，排除延迟上下文的许多函数：

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

 

