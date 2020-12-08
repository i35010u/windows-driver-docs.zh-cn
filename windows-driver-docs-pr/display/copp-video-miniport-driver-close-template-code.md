---
title: COPP 视频微型端口驱动程序关闭模板代码
description: COPP 视频微型端口驱动程序关闭模板代码
keywords:
- 正在释放 COPP DirectX VA 设备对象
- 关闭 COPP DirectX VA 设备对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b402ba44a19343f13249858f7c520dff7d41c8c6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810105"
---
# <a name="copp-video-miniport-driver-close-template-code"></a>COPP 视频微型端口驱动程序关闭模板代码


## <span id="ddk_copp_video_miniport_driver_close_template_code_gg"></span><span id="DDK_COPP_VIDEO_MINIPORT_DRIVER_CLOSE_TEMPLATE_CODE_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。

使用以下示例代码释放 COPP DirectX VA 设备对象的实例。

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

 

 





