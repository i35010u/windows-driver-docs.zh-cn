---
title: COPP 视频微型端口驱动程序 IOCTL 模板代码
description: COPP 视频微型端口驱动程序 IOCTL 模板代码
ms.assetid: 55a77261-016e-4ba6-8cb6-c45171759035
keywords:
- Ioctl WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71fbf14e5ffb345417be42fd1d0d375267f35718
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331338"
---
# <a name="copp-video-miniport-driver-ioctl-template-code"></a>COPP 视频微型端口驱动程序 IOCTL 模板代码


## <span id="ddk_copp_video_miniport_driver_ioctl_template_code_gg"></span><span id="DDK_COPP_VIDEO_MINIPORT_DRIVER_IOCTL_TEMPLATE_CODE_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 和更高版本，和 Windows XP SP2 及更高版本。

微型端口驱动程序必须实现[ *HwVidStartIO* ](https://msdn.microsoft.com/library/windows/hardware/ff567367)函数来处理中显示器驱动程序发出的 I/O 请求。 下面的代码示例显示了仅处理方式的微型端口驱动程序 COPP Ioctl:

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

 

 





