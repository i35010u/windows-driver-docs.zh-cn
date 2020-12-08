---
title: COPP 视频微型端口驱动程序序列启动模板代码
description: COPP 视频微型端口驱动程序序列启动模板代码
keywords:
- 序列启动 WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 431d29a9b5376865639b117ca383ef96b16195b1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804179"
---
# <a name="copp-video-miniport-driver-sequence-start-template-code"></a>COPP 视频微型端口驱动程序序列启动模板代码


## <span id="ddk_copp_video_miniport_driver_sequence_start_template_code_gg"></span><span id="DDK_COPP_VIDEO_MINIPORT_DRIVER_SEQUENCE_START_TEMPLATE_CODE_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。

使用以下示例代码将当前视频会话设置为 COPP DirectX VA 设备对象的保护模式。

```cpp
VP_STATUS
IoctlCOPPStartSeqence(
    PHW_DEVICE_EXTENSION pHwDeviceExtension,
    PVIDEO_REQUEST_PACKET pVideoRequestPacket
    )
{
    COPP_IO_InputBuffer* pInBuff = pVideoRequestPacket->InputBuffer;
    COPP_DeviceData* pThis = (COPP_DeviceData*)*pInBuff->ppThis;
    DXVA_COPPSignature* lpin = (DXVA_COPPSignature*)pInBuff->InputBuffer;
     *pInBuff->phr = COPPSequenceStart(pThis, lpin);
    return NO_ERROR;
}
```

 

 





