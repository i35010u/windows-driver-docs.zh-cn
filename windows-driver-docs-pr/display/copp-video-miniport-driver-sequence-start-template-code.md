---
title: COPP 视频微型端口驱动程序序列开始模板代码
description: COPP 视频微型端口驱动程序序列开始模板代码
ms.assetid: f1fc0d03-43f6-44a0-b911-1ca473e4e701
keywords:
- 序列启动 WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb5c9294e1b38975e75bb8c49c9328a38faf6de6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526619"
---
# <a name="copp-video-miniport-driver-sequence-start-template-code"></a>COPP 视频微型端口驱动程序序列开始模板代码


## <span id="ddk_copp_video_miniport_driver_sequence_start_template_code_gg"></span><span id="DDK_COPP_VIDEO_MINIPORT_DRIVER_SEQUENCE_START_TEMPLATE_CODE_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 和更高版本，和 Windows XP SP2 及更高版本。

下面的示例代码用于将当前的视频会话设置为受保护模式 COPP DirectX VA 设备对象。

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

 

 





