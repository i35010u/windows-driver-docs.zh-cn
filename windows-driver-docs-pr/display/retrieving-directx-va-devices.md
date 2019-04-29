---
title: 检索 DirectX VA 设备
description: 检索 DirectX VA 设备
ms.assetid: 7af82243-7cb3-4e66-a6ee-3f4220baa459
keywords:
- DirectX 视频加速 WDK Windows 2000 显示，检索设备
- 检索 DirectX VA 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2facbc48422e8f394f06defe29a51474d4b45c7e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378521"
---
# <a name="retrieving-directx-va-devices"></a>检索 DirectX VA 设备


## <span id="ddk_retrieving_directx_va_devices_gg"></span><span id="DDK_RETRIEVING_DIRECTX_VA_DEVICES_GG"></span>


使用下面的代码示例检索 DirectX VA 设备。 此代码是实现[ *DdMoCompGetGuids* ](https://msdn.microsoft.com/library/windows/hardware/ff550236)回调函数。 **GetMoCompGuids**的成员[ **DD\_MOTIONCOMPCALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff551660)结构指向回调函数。

```cpp
DWORD g_dwDXVANumSupportedGUIDs = 4;
const GUID* g_DXVASupportedGUIDs[4] = {
 &DXVA_DeinterlaceContainerDevice,
    &DXVA_ProcAmpControlDevice
    &DXVA_DeinterlaceBobDevice
 &DXVA_COPPDevice
};

DWORD APIENTRY
  MOCOMPCB_GETGUIDS(
    PDD_GETMOCOMPGUIDSDATA  lpData
    )
{
    DWORD dwNumToCopy;

    // If lpGuids == NULL, the driver must return the number of 
    // supported GUIDS in the dwNumGuids parameter. If non-NULL, 
    // the supported GUIDS must be copied into the buffer at lpGuids.
    if (lpData->lpGuids) {
        dwNumToCopy = min(g_dwDXVANumSupportedGUIDs, lpData->dwNumGuids);
        for (DWORD i = 0; i < dwNumToCopy; i++) {
            lpData->lpGuids[i] = *g_DXVASupportedGUIDs[i];
        }
    }
    else {
        dwNumToCopy = g_dwDXVANumSupportedGUIDs;
    }

    lpData->dwNumGuids = dwNumToCopy;
    lpData->ddRVal = DD_OK;

    return DDHAL_DRIVER_HANDLED;
}
```

 

 





