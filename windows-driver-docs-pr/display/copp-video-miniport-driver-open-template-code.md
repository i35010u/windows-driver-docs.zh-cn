---
title: COPP 视频微型端口驱动程序开放模板代码
description: COPP 视频微型端口驱动程序开放模板代码
keywords:
- 打开 COPP DirectX VA 设备对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f434104efcfe208aa9dc4af82e4f527f240d86c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804187"
---
# <a name="copp-video-miniport-driver-open-template-code"></a>COPP 视频微型端口驱动程序开放模板代码


## <span id="ddk_copp_video_miniport_driver_open_template_code_gg"></span><span id="DDK_COPP_VIDEO_MINIPORT_DRIVER_OPEN_TEMPLATE_CODE_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。

使用以下示例代码创建 COPP DirectX VA 设备对象的实例。

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

 

 





