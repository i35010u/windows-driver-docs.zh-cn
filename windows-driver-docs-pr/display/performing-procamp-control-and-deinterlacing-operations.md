---
title: 执行 ProcAmp 控制和反交错操作
description: 执行 ProcAmp 控制和反交错操作
keywords:
- ProcAmp WDK DirectX VA，取消隔行扫描操作
- 取消隔行扫描 WDK DirectX VA，ProcAmp
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b0864a42230d500130855a7529f73253d7906e47
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838059"
---
# <a name="performing-procamp-control-and-deinterlacing-operations"></a>执行 ProcAmp 控制和反交错操作


## <span id="ddk_performing_procamp_control_and_deinterlacing_operations_gg"></span><span id="DDK_PERFORMING_PROCAMP_CONTROL_AND_DEINTERLACING_OPERATIONS_GG"></span>


使用以下示例代码来执行 ProcAmp 控制和取消隔行扫描操作。 此代码是 [*DdMoCompRender*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_render) 回调函数的实现。 [**DD \_ MOTIONCOMPCALLBACKS**](/windows/win32/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)结构的 **RenderMoComp** 成员指向回调函数。

```cpp
DWORD APIENTRY
  MOCOMPCB_RENDER(
    PDD_RENDERMOCOMPDATA  lpData
    )
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
    // Process according to the device type in the class object.
     // For more information, see Defining DirectX VA Device Classes.
    switch (pDXVABase->m_DeviceType) {
    // This is the deinterlace container device.
    case DXVA_DeviceContainer:
        switch (lpData->dwFunction) {
        case DXVA_DeinterlaceQueryAvailableModesFnCode:
            {
                DXVA_DeinterlaceContainerDeviceClass* pDXVADev =
                    (DXVA_DeinterlaceContainerDeviceClass*)pDXVABase;

                DXVA_DeinterlaceQueryAvailableModes* pQAM =
           (DXVA_DeinterlaceQueryAvailableModes*)lpData->lpOutputData;

                 // Part of the Deinterlace DDI.
                lpData->ddRVal = 
                             pDXVADev->DeinterlaceQueryAvailableModes(
                                (DXVA_VideoDesc*)lpData->lpInputData,
                                 &pQAM->NumGuids,
                                 &pQAM->Guids[0]);
            }
            return DDHAL_DRIVER_HANDLED;

        case DXVA_DeinterlaceQueryModeCapsFnCode:
            {
                DXVA_DeinterlaceContainerDeviceClass* pDXVADev =
                    (DXVA_DeinterlaceContainerDeviceClass*)pDXVABase;

                DXVA_DeinterlaceQueryModeCaps* pQMC =
                 (DXVA_DeinterlaceQueryModeCaps*)lpData->lpInputData;

                DXVA_DeinterlaceCaps*pDC =
                    (DXVA_DeinterlaceCaps*)lpData->lpOutputData;

                 // Part of the Deinterlace DDI.
                lpData->ddRVal = pDXVADev->DeinterlaceQueryModeCaps(
                                    &pQMC->Guid,
                                    &pQMC->VideoDesc,
                                    pDC);
            }
            return DDHAL_DRIVER_HANDLED;

        case DXVA_ProcAmpControlQueryCapsFnCode:
            {
                DXVA_DeinterlaceContainerDeviceClass* pDXVADev =
                    (DXVA_DeinterlaceContainerDeviceClass*)pDXVABase;

                DXVA_VideoDesc* pVideoDesc =
                    (DXVA_VideoDesc *)lpData->lpInputData;

 DXVA_ProcAmpControlCaps* pCC =
                    (DXVA_ProcAmpControlCaps*)lpData->lpOutputData;

  // Part of the ProcAmp Control DDI.
 lpData->ddRVal = pDXVADev->ProcAmpControlQueryCaps(
                                    pVideoDesc,
 pCC);
            }
            return DDHAL_DRIVER_HANDLED;

        case DXVA_ProcAmpControlQueryRangeFnCode:
            {
                DXVA_DeinterlaceContainerDeviceClass* pDXVADev =
 (DXVA_DeinterlaceContainerDeviceClass*)pDXVABase;

                DXVA_ProcAmpControlQueryRange* pccqr =
                (DXVA_ProcAmpControlQueryRange *)lpData->lpInputData;

                DXVA_VideoPropertyRange*pPR =
 (DXVA_VideoPropertyRange*)lpData->lpOutputData;

                  // Part of the ProcAmp Control DDI.
 lpData->ddRVal = pDXVADev->ProcAmpControlQueryRange(
                                    pccqr->ProcAmpControlProp,
 &pccqr->VideoDesc,
                                    pPR);
            }
            return DDHAL_DRIVER_HANDLED;

  default:
            lpData->ddRVal = E_INVALIDARG;
 return DDHAL_DRIVER_HANDLED;
        }
        break;
    // This is the ProcAmp control device.
    case DXVA_DeviceProcAmpControl:
        switch (lpData->dwFunction) {
 case DXVA_ProcAmpControlBltFnCode:
            {
                DXVA_ProcAmpControlDeviceClass* pDXVADev =
                    (DXVA_ProcAmpControlDeviceClass*)pDXVABase;

                DXVA_ProcAmpControlBlt* lpBlt = 
                      (DXVA_ProcAmpControlBlt*)lpData->lpInputData;
                LPDDMOCOMPBUFFERINFO lpBuffInfo = lpData->lpBufferInfo;
  // Part of the ProcAmp Control DDI.
                lpData->ddRVal = pDXVADev->ProcAmpControlBlt(
                                         lpBuffInfo[0].lpCompSurface,
                                         lpBuffInfo[1].lpCompSurface,
                                         lpBlt);
            }
            return DDHAL_DRIVER_HANDLED;

 default:
            lpData->ddRVal = E_INVALIDARG;
 return DDHAL_DRIVER_HANDLED;
        }
        break;
    // This is the deinterlace bob device.
    case DXVA_DeviceDeinterlacer:
        switch (lpData->dwFunction) {
        case DXVA_DeinterlaceBltFnCode:
            {
                DXVA_DeinterlaceBobDeviceClass* pDXVADev =
                        (DXVA_DeinterlaceBobDeviceClass*)pDXVABase;

                DXVA_DeinterlaceBlt* lpBlt = 
                         (DXVA_DeinterlaceBlt*)lpData->lpInputData;
                LPDDMOCOMPBUFFERINFO lpBuffInfo = lpData->lpBufferInfo;

                for (DWORD i = 0; i < lpBlt->NumSourceSurfaces; i++) {
                    lpBlt->Source[i].lpDDSSrcSurface = 
                                      lpBuffInfo[1 + i].lpCompSurface;
                }
                 // Part of the Deinterlace DDI.
                lpData->ddRVal = pDXVADev->DeinterlaceBlt(
                                          lpBlt->rtTarget,
                                          &lpBlt->DstRect,
                                          lpBuffInfo[0].lpCompSurface,
                                          &lpBlt->SrcRect,
                                          lpBlt->Source,
                                          lpBlt->NumSourceSurfaces,
                                          lpBlt->Alpha);
            }
            return DDHAL_DRIVER_HANDLED;

        default:
            lpData->ddRVal = E_INVALIDARG;
            return DDHAL_DRIVER_HANDLED;
        }
        break;
    }

    lpData->ddRVal = DDERR_CURRENTLYNOTAVAIL;
    return DDHAL_DRIVER_HANDLED;
}
```

 

