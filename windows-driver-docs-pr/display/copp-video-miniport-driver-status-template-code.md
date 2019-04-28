---
title: COPP 视频微型端口驱动程序状态模板代码
description: COPP 视频微型端口驱动程序状态模板代码
ms.assetid: 4d0d0f95-8a21-4863-9930-ddee7d944c04
keywords:
- WDK COPP 的状态信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f59194f385daa93503174b640e6a7f71b56ad9f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331315"
---
# <a name="copp-video-miniport-driver-status-template-code"></a>COPP 视频微型端口驱动程序状态模板代码


## <span id="ddk_copp_video_miniport_driver_status_template_code_gg"></span><span id="DDK_COPP_VIDEO_MINIPORT_DRIVER_STATUS_TEMPLATE_CODE_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 和更高版本，和 Windows XP SP2 及更高版本。

下面的示例代码用于检索受保护的视频会话 COPP DirectX VA 设备对象与关联的状态。

```cpp
VP_STATUS
IoctlCOPPStatus(
    PHW_DEVICE_EXTENSION pHwDeviceExtension,
    PVIDEO_REQUEST_PACKET pVideoRequestPacket
    )
{
    COPP_IO_InputBuffer* pInBuff = pVideoRequestPacket->InputBuffer;
    COPP_DeviceData* pThis = (COPP_DeviceData*)*pInBuff->ppThis;
    DXVA_COPPStatusInput* lpin = (DXVA_COPPStatusInput*)pInBuff->InputBuffer;
    DXVA_COPPStatusOutput* lpout = (DXVA_COPPStatusOutput*)pVideoRequestPacket->OutputBuffer;
    HRESULT* phr = pInBuff->phr;
     *phr =  COPPQueryStatus(pThis, lpin, lpout);
    if (*phr == NO_ERROR) {
        pVideoRequestPacket->StatusBlock->Information = sizeof(DXVA_COPPStatusOutput);
    }
    return S_OK;
}
```

 

 





