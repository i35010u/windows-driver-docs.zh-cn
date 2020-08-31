---
title: 删除 DirectX VA 设备对象的实例
description: 删除 DirectX VA 设备对象的实例
ms.assetid: fab8c6eb-97fa-427e-9fb2-6da249d8d97d
keywords:
- 删除 DirectX VA 设备对象的实例
- 删除 DirectX VA 设备对象的实例
- DirectX 视频加速 WDK Windows 2000 显示，删除实例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66486fc2cb24a3a0cf3f25af53c4a1b3da390aad
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063936"
---
# <a name="deleting-instances-of-directx-va-device-objects"></a>删除 DirectX VA 设备对象的实例


## <span id="ddk_deleting_instances_of_directx_va_device_objects_gg"></span><span id="DDK_DELETING_INSTANCES_OF_DIRECTX_VA_DEVICE_OBJECTS_GG"></span>


使用以下示例代码删除 DirectX VA 设备对象的实例。 此代码是 [*DdMoCompDestroy*](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_destroy) 回调函数的实现。 [**DD \_ MOTIONCOMPCALLBACKS**](/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)结构的**DestroyMoComp**成员指向回调函数。

```cpp
DWORD APIENTRY
  MOCOMPCB_DESTROY(
    PDD_DESTROYMOCOMPDATA  lpData
    )
{
    // The driver saves the device class object in lpDriverReserved1 
     // during the call to the DdMoCompCreate callback. For more information, 
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
        lpData->ddRVal = S_OK;
        delete pDXVABase;
        break;

    // This is the ProcAmp control device.
 case DXVA_DeviceProcAmpControl:
        {
            DXVA_ProcAmpControlDeviceClass* pDXVADev =
 (DXVA_ProcAmpControlDeviceClass*)pDXVABase;
             // Part of the ProcAmp Control DDI.
            lpData->ddRVal = pDXVADev->ProcAmpControlCloseStream();
            delete pDXVADev;
        }
        break;

    // This is the deinterlace bob device.
 case DXVA_DeviceDeinterlacer:
        {
            DXVA_DeinterlaceBobDeviceClass* pDXVADev =
 (DXVA_DeinterlaceBobDeviceClass*)pDXVABase;
             // Part of the Deinterlace DDI.
            lpData->ddRVal = pDXVADev->DeinterlaceCloseStream();
            delete pDXVADev;
        }
        break;

    // This is the COPP device.
    case DXVA_DeviceCOPP:
        DXVA_COPPDeviceClass* pDXVADev = (DXVA_COPPDeviceClass*)pDXVABase;
        ULONG BytesReturned;
        HANDLE handle = (HANDLE)GetDriverHandleFromPDEV(lpData ->lpDD->lpGbl->dhpdev)
        COPP_IO_InputBuffer InputBuffer;
        InputBuffer.ppThis = &pDXVADev->m_pThis;
        InputBuffer.InputBuffer = NULL;
        InputBuffer.phr = &lpData->ddRVal;
        EngDeviceIoControl(handle,
                           IOCTL_COPP_CloseDevice,
                           &InputBuffer,
                           sizeof(InputBuffer),
                           NULL,
                           0,
                           &BytesReturned);
            delete pDXVADev;
        }
        break;
    }
    return DDHAL_DRIVER_HANDLED;
}
```

 

