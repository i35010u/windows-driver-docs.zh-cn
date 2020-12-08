---
title: COPP 视频微型端口驱动程序 IOCTL 模板代码
description: COPP 视频微型端口驱动程序 IOCTL 模板代码
keywords:
- IOCTLs WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e831ef968bd66655ade8b254e6011f42a61031b0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820847"
---
# <a name="copp-video-miniport-driver-ioctl-template-code"></a>COPP 视频微型端口驱动程序 IOCTL 模板代码


## <span id="ddk_copp_video_miniport_driver_ioctl_template_code_gg"></span><span id="DDK_COPP_VIDEO_MINIPORT_DRIVER_IOCTL_TEMPLATE_CODE_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。

视频微型端口驱动程序必须实现 [*HwVidStartIO*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_start_io) 函数以处理源自显示驱动程序的 i/o 请求。 以下示例代码仅演示视频微型端口驱动程序如何处理 COPP IOCTLs：

```cpp
BOOLEAN
HwVidStartIO(
    PHW_DEVICE_EXTENSION pHwDeviceExtension,
    PVIDEO_REQUEST_PACKET pVideoRequestPacket
    )
{
    VP_STATUS vpStatus;
    switch (pVideoRequestPacket->IoControlCode)
    {
        case IOCTL_COPP_OpenDevice:
            vpStatus = IoctlCOPPOpenDevice(pHwDeviceExtension, pVideoRequestPacket);
            break;
        case IOCTL_COPP_GetCertificateLength:
            vpStatus = IoctlCOPPGetCertificateLength(pHwDeviceExtension, pVideoRequestPacket);
            break;
        case IOCTL_COPP_KeyExchange:
            vpStatus = IoctlCOPPKeyExchange(pHwDeviceExtension, pVideoRequestPacket);
            break;
        case IOCTL_COPP_StartSequence:
            vpStatus = IoctlCOPPStartSeqence(pHwDeviceExtension, pVideoRequestPacket);
            break;
        case IOCTL_COPP_Command:
            vpStatus = IoctlCOPPCommand(pHwDeviceExtension, pVideoRequestPacket);
            break;
        case IOCTL_COPP_Status:
            vpStatus = IoctlCOPPStatus(pHwDeviceExtension, pVideoRequestPacket);
            break;
        case IOCTL_COPP_CloseDevice:
            vpStatus = IoctlCOPPCloseDevice(pHwDeviceExtension, pVideoRequestPacket);
            break;
        default:
            vpStatus = ERROR_INVALID_FUNCTION;
            break;
    }
    pVideoRequestPacket->StatusBlock->Status = vpStatus;
    return TRUE;
}
```

 

