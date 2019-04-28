---
title: COPP 视频微型端口驱动程序开放模板代码
description: COPP 视频微型端口驱动程序开放模板代码
ms.assetid: 41facdef-c5f7-42f1-a251-07e4685649de
keywords:
- 打开 COPP DirectX VA 设备对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b2dc452c4c889dd13c0e48f7e7aaa0ebed0abfa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331321"
---
# <a name="copp-video-miniport-driver-open-template-code"></a>COPP 视频微型端口驱动程序开放模板代码


## <span id="ddk_copp_video_miniport_driver_open_template_code_gg"></span><span id="DDK_COPP_VIDEO_MINIPORT_DRIVER_OPEN_TEMPLATE_CODE_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 和更高版本，和 Windows XP SP2 及更高版本。

下面的示例代码用于创建设备对象的实例的 COPP DirectX VA。

```cpp
VP_STATUS
IoctlCOPPOpenDevice(
    PHW_DEVICE_EXTENSION pHwDeviceExtension,
    PVIDEO_REQUEST_PACKET pVideoRequestPacket
    )
{
    COPP_IO_InputBuffer* pInBuff = pVideoRequestPacket->InputBuffer;
    ULONG uDevID = *(ULONG*)pInBuff->InputBuffer;
    COPP_DeviceData* pThis = VideoPortAllocatePool(pHwDeviceExtension,
                                              VpPagedPool,
                                              sizeof(COPP_DeviceData),
                                              'PPOC');
    *pInBuff->ppThis = NULL;
    if (pThis == NULL) {
        *pInBuff->phr = ERROR_NOT_ENOUGH_MEMORY;
        return NO_ERROR;
    }
     *pInBuff->phr = COPPOpenVideoSession(pThis, uDevID);
    if (*pInBuff->phr == NO_ERROR) {
        *pInBuff->ppThis = pThis;
    }
    else {
        VideoPortFreePool(pHwDeviceExtension, pThis);
        *pInBuff->ppThis = NULL;
    }
    return NO_ERROR;
}
```

 

 





