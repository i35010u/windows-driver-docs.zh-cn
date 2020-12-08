---
title: COPP 视频微型端口驱动程序状态模板代码
description: COPP 视频微型端口驱动程序状态模板代码
keywords:
- 状态信息 WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d5dce9d03dda44dbf5b83902fe4bcf1e1ae3b66
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795023"
---
# <a name="copp-video-miniport-driver-status-template-code"></a>COPP 视频微型端口驱动程序状态模板代码


## <span id="ddk_copp_video_miniport_driver_status_template_code_gg"></span><span id="DDK_COPP_VIDEO_MINIPORT_DRIVER_STATUS_TEMPLATE_CODE_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。

使用以下示例代码来检索与 COPP DirectX VA 设备对象相关联的受保护视频会话的状态。

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

 

 





