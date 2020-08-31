---
title: 检索 DirectX VA 设备
description: 检索 DirectX VA 设备
ms.assetid: 7af82243-7cb3-4e66-a6ee-3f4220baa459
keywords:
- DirectX 视频加速 WDK Windows 2000 显示，检索设备
- 检索 DirectX VA 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4da929b4d4094e8330d92917a0b90a806041405
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064016"
---
# <a name="retrieving-directx-va-devices"></a>检索 DirectX VA 设备


## <span id="ddk_retrieving_directx_va_devices_gg"></span><span id="DDK_RETRIEVING_DIRECTX_VA_DEVICES_GG"></span>


使用以下示例代码检索 DirectX VA 设备。 此代码是 [*DdMoCompGetGuids*](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_getguids) 回调函数的实现。 [**DD \_ MOTIONCOMPCALLBACKS**](/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)结构的**GetMoCompGuids**成员指向回调函数。

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

 

