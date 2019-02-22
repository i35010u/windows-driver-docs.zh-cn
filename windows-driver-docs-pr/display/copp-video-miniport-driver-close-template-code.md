---
title: COPP 视频微型端口驱动程序关闭模板代码
description: COPP 视频微型端口驱动程序关闭模板代码
ms.assetid: a7b088d6-a6cd-479d-b256-04def1de1736
keywords:
- 释放 COPP DirectX VA 设备对象
- 关闭 COPP DirectX VA 设备对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38110cb52cb8e963d4a5179e21f66657db0d0d10
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546002"
---
# <a name="copp-video-miniport-driver-close-template-code"></a>COPP 视频微型端口驱动程序关闭模板代码


## <span id="ddk_copp_video_miniport_driver_close_template_code_gg"></span><span id="DDK_COPP_VIDEO_MINIPORT_DRIVER_CLOSE_TEMPLATE_CODE_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 和更高版本，和 Windows XP SP2 及更高版本。

使用下面的示例代码以释放 COPP DirectX VA 设备对象的实例。

```cpp
VP_STATUS
IoctlCOPPCloseDevice(
    PHW_DEVICE_EXTENSION pHwDeviceExtension,
    PVIDEO_REQUEST_PACKET pVideoRequestPacket
    )
{
    COPP_IO_InputBuffer* pInBuff = pVideoRequestPacket->InputBuffer;
    COPP_DeviceData* pThis = (COPP_DeviceData*)*pInBuff->ppThis;
     *pInBuff->phr = COPPCloseVideoSession(pThis);
    VideoPortFreePool(pHwDeviceExtension, pThis);
    *pInBuff->ppThis = NULL;
    return NO_ERROR;
}
```

 

 





