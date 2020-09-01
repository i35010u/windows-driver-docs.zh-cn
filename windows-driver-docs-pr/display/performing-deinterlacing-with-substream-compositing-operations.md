---
title: 执行具有子流组合操作的取消隔行扫描
description: 执行反交错与子流复合操作
ms.assetid: e6759e88-5cbb-4372-8a92-312f1684b99d
keywords:
- 取消隔行扫描 WDK DirectX VA，组合子流组合
- 组合子流合成 WDK DirectX VA
- 子流合成 WDK DirectX VA
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 1333a1a7d897555e6b7326f3a9310c2b2c879eda
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067302"
---
# <a name="performing-deinterlacing-with-substream-compositing-operations"></a>执行反交错与子流复合操作

**本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。**

使用以下示例代码来执行以下操作：将取消隔行扫描与视频流组合在一起，并在视频流顶部合成视频 substreams。 示例代码实现了 [*DdMoCompRender*](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render) 回调函数。 [**DD \_ MOTIONCOMPCALLBACKS**](/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)结构的**RenderMoComp**成员指向回调函数。 示例代码只显示了如何将 *DdMoCompRender* 用于具有子流组合操作的取消隔行扫描。 有关执行 ProcAmp 控件和取消隔行扫描操作的 *DdMoCompRender* 的实现，请参阅 [执行 ProcAmp 控件和取消隔行扫描操作](performing-procamp-control-and-deinterlacing-operations.md)。

```cpp
DWORD APIENTRY
MOCOMPCB_RENDER(PDD_RENDERMOCOMPDATA lpData)
{
  // The driver saves the device class object in lpDriverReserved1 
   // during the DdMoCompCreate callback. For more information, 
   // see Creating Instances of DirectX VA Device Objects.
 DXVA_DeviceBaseClass* pDXVABase =
         (DXVA_DeviceBaseClass*)lpData->lpMoComp->lpDriverReserved1;
 if (pDXVABase == NULL) {
      lpData->ddRVal = E_POINTER;  
      return DDHAL_DRIVER_HANDLED;
  }
  switch (lpData->dwFunction) {
  case DXVA_DeinterlaceBltExFnCode:
 {  
      DXVA_DeinterlaceBobDeviceClass* pDXVADev =
                        (DXVA_DeinterlaceBobDeviceClass*)pDXVABase;
      DXVA_DeinterlaceBltEx* lpBlt = 
             (DXVA_DeinterlaceBltEx*)lpData->lpInputData;
      LPDDMOCOMPBUFFERINFO lpBuffInfo = lpData->BufferInfo;

      for (DWORD i = 0; i < lpBlt->NumSourceSurfaces; i++) {
          lpBlt->Source[i].lpDDSSrcSurface = 
                          lpBuffInfo[1 + i].lpCompSurface;
      }

       // Part of the Deinterlace DDI.
      lpData->ddRVal = pDXVADev->DeinterlaceBltEx(
                                       lpBlt->rtTarget,
                                       &lpBlt->rcTarget,
                                       lpBlt->BackgroundColor,
                                       lpBlt->DestinationFormat,
                                       lpBlt->DestinationFlags,
                                       lpBuffInfo[0].lpCompSurface,
                                       lpBlt->Source,
                                       lpBlt->NumSourceSurfaces,
                                       lpBlt->Alpha);
      return DDHAL_DRIVER_HANDLED;
  }
  default:
      lpData->ddRVal = E_INVALIDARG;
 return DDHAL_DRIVER_HANDLED;
  }

lpData->ddRVal = DDERR_CURRENTLYNOTAVAIL;
return DDHAL_DRIVER_HANDLED;
}
```

 

