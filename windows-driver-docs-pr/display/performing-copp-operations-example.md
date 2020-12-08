---
title: 执行 COPP 操作的示例
description: 执行 COPP 操作的示例
keywords:
- 复制保护 WDK COPP，COPP 操作示例代码
- 视频复制保护 WDK COPP，COPP 操作示例代码
- COPP WDK DirectX VA，操作示例代码
- 受保护的视频 WDK COPP，COPP 操作示例代码
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c01814363a36d90bfc6c252c2cb37f5b22c75a31
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815459"
---
# <a name="performing-copp-operations-example"></a>执行 COPP 操作的示例


## <span id="ddk_performing_copp_operations_gg"></span><span id="DDK_PERFORMING_COPP_OPERATIONS_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。**

使用以下示例代码，通过认证的输出保护协议 (COPP) 执行操作。 示例代码实现了 [*DdMoCompRender*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_render) 回调函数。 [**DD \_ MOTIONCOMPCALLBACKS**](/windows/win32/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)结构的 **RenderMoComp** 成员指向回调函数。 示例代码只显示了如何将 *DdMoCompRender* 用于 COPP 操作。 有关执行 ProcAmp 控件和取消隔行扫描操作的 *DdMoCompRender* 的实现，请参阅 [执行 ProcAmp 控件和取消隔行扫描操作](performing-procamp-control-and-deinterlacing-operations.md) 和 [使用子流组合操作执行取消隔行扫描](performing-deinterlacing-with-substream-compositing-operations.md)。

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

 

