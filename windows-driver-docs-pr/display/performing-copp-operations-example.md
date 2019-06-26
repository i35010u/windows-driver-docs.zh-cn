---
title: 执行 COPP 操作的示例
description: 用于执行 COPP 操作示例
ms.assetid: ba5c98d3-63d1-4e2d-ba11-6054c1623e80
keywords:
- 复制保护 WDK COPP，COPP 操作的示例代码
- 视频复制保护 WDK COPP，COPP 操作的示例代码
- COPP WDK DirectX va，因此操作的示例代码
- 受保护视频 WDK COPP，COPP 操作的示例代码
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f5954313b6994309e2a56d1e80ab7bde6204bae
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385582"
---
# <a name="performing-copp-operations-example"></a>执行 COPP 操作的示例


## <span id="ddk_performing_copp_operations_gg"></span><span id="DDK_PERFORMING_COPP_OPERATIONS_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 和更高版本，和 Windows XP SP2 及更高版本。**

使用下面的代码示例通过认证的输出保护协议 (COPP) 执行操作。 代码示例实现了[ *DdMoCompRender* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)回调函数。 **RenderMoComp**的成员[ **DD\_MOTIONCOMPCALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)结构指向回调函数。 该示例代码仅演示如何*DdMoCompRender* COPP 操作中使用。 实现*DdMoCompRender*执行 ProcAmp 控件和去隔行操作，请参阅[执行 ProcAmp 控制和去隔行操作](performing-procamp-control-and-deinterlacing-operations.md)和[执行与子流组合的情况下操作去隔行](performing-deinterlacing-with-substream-compositing-operations.md)。

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
    // This is the COPP device.
    case DXVA_DeviceCOPP:
        {
            DXVA_COPPDeviceClass* pDXVACopp =
                        (DXVA_COPPDeviceClass*)pDXVABase;
            ULONG BytesReturned;
            HANDLE handle = (HANDLE)GetDriverHandleFromPDEV(lpData->lpDD->lpGbl->dhpdev)
            COPP_IO_InputBuffer InputBuffer;
            InputBuffer.ppThis = &pDXVACopp->m_pThis;
            InputBuffer.phr = &lpData->ddRVal;
            switch (lpData->dwFunction) {
            case DXVA_COPPGetCertificateLengthFnCode:
                if (lpData->dwOutputDataSize < sizeof(ULONG)) {
 lpData->ddRVal = E_INVALIDARG;
                }
                else { 
 InputBuffer.InputBuffer = NULL;
                    EngDeviceIoControl(handle,
                                      IOCTL_COPP_GetCertificateLength,
                                      &InputBuffer,
                                      sizeof(InputBuffer),
                                      lpData->lpOutputData,
                                      lpData->dwOutputDataSize,
                                      &BytesReturned);
                }
                break;
            case DXVA_COPPKeyExchangeFnCode:
                if (lpData->dwOutputDataSize < sizeof(DXVA_COPPKeyExchangeOutput)) {
  lpData->ddRVal = E_INVALIDARG;
                }
                else {
 InputBuffer.InputBuffer = NULL;
                    DD_SURFACE_LOCAL* lpCompSurf =
                        lpData->lpBufferInfo[0].lpCompSurface;
                    InputBuffer.InputBuffer = (PVOID)lpCompSurf->lpGbl->fpVidMem;
                    EngDeviceIoControl(handle
                                       IOCTL_COPP_KeyExchange,
                                       &InputBuffer,
                                        sizeof(InputBuffer),
                                       lpData->lpOutputData,
                                       lpData->dwOutputDataSize,
                                       &BytesReturned);
                }
                break;
            case DXVA_COPPSequenceStartFnCode:
                if (lpData->dwInputDataSize < sizeof(DXVA_COPPSignature)) {
 lpData->ddRVal = E_INVALIDARG;
                }
                else {
                    InputBuffer.InputBuffer = lpData->lpInputData;
                    EngDeviceIoControl(handle,
 IOCTL_COPP_StartSequence,
                                       &InputBuffer,
                                       sizeof(InputBuffer),
                                       NULL,
                                       0,
                                       &BytesReturned);
                }
                break;
            case DXVA_COPPCommandFnCode:
                if (lpData->dwInputDataSize < sizeof(DXVA_COPPCommand)) {
 lpData->ddRVal = E_INVALIDARG;
                }
                else {
                    InputBuffer.InputBuffer = lpData->lpInputData;
                    EngDeviceIoControl(handle,
 IOCTL_COPP_Command,
                                       &InputBuffer,
                                       sizeof(InputBuffer),
                                       NULL,
                                       0,
                                       &BytesReturned);
                }
                break;
            case DXVA_COPPQueryStatusFnCode:
                if (lpData->dwInputDataSize < sizeof(DXVA_COPPStatusInput) ||
                    lpData->dwOutputDataSize < sizeof(DXVA_COPPStatusOutput)) {
 lpData->ddRVal = E_INVALIDARG;
                }
                else {
                    InputBuffer.InputBuffer = lpData->lpInputData;
                    EngDeviceIoControl(handle,
 IOCTL_COPP_Status,
                                       &InputBuffer,
                                       sizeof(InputBuffer),
                                       lpData->lpOutputData,
                                       lpData->dwOutputDataSize,
                                       &BytesReturned);
 }
                break;
            default:
                lpData->ddRVal = E_INVALIDARG;
 break;
            }
            break;
        }
    }
    return DDHAL_DRIVER_HANDLED;
}
```

 

 





