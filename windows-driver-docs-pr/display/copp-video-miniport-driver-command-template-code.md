---
title: COPP 视频微型端口驱动程序命令模板代码
description: COPP 视频微型端口驱动程序命令模板代码
ms.assetid: a772fc78-0024-4834-8ff3-a1cf6672b316
keywords:
- WDK COPP 命令
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 685c20c7ccf515fe5879790694e94346839e268e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566057"
---
# <a name="copp-video-miniport-driver-command-template-code"></a>COPP 视频微型端口驱动程序命令模板代码


## <span id="ddk_copp_video_miniport_driver_command_template_code_gg"></span><span id="DDK_COPP_VIDEO_MINIPORT_DRIVER_COMMAND_TEMPLATE_CODE_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 和更高版本，和 Windows XP SP2 及更高版本。

使用下面的示例代码执行 COPP DirectX VA 设备对象的操作。

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

 

 





