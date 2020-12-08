---
title: COPP 视频微型端口驱动程序命令模板代码
description: COPP 视频微型端口驱动程序命令模板代码
keywords:
- 命令 WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa9ee4079b1f68655c7ba977e5a07a55c62feb2f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803941"
---
# <a name="copp-video-miniport-driver-command-template-code"></a>COPP 视频微型端口驱动程序命令模板代码


## <span id="ddk_copp_video_miniport_driver_command_template_code_gg"></span><span id="DDK_COPP_VIDEO_MINIPORT_DRIVER_COMMAND_TEMPLATE_CODE_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。

使用以下示例代码在 COPP DirectX VA 设备对象上执行操作。

```cpp
VP_STATUS
IoctlCOPPCommand(
    PHW_DEVICE_EXTENSION pHwDeviceExtension,
    PVIDEO_REQUEST_PACKET pVideoRequestPacket
    )
{
    COPP_IO_InputBuffer* pInBuff = pVideoRequestPacket->InputBuffer;
    COPP_DeviceData* pThis = (COPP_DeviceData*)*pInBuff->ppThis;
    DXVA_COPPCommand* lpin = (DXVA_COPPCommand*)pInBuff->InputBuffer;
     *pInBuff->phr = COPPCommand(pThis, lpin);
    return NO_ERROR;
}
```

 

 





