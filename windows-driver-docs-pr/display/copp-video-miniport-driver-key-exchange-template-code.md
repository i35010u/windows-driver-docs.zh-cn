---
title: COPP 视频微型端口驱动程序密钥交换模板代码
description: COPP 视频微型端口驱动程序密钥交换模板代码
keywords:
- 密钥交换 WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3e8ccdebbc05f14a09f825a616f9fc3925a6b17
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804193"
---
# <a name="copp-video-miniport-driver-key-exchange-template-code"></a>COPP 视频微型端口驱动程序密钥交换模板代码


## <span id="ddk_copp_video_miniport_driver_key_exchange_template_code_gg"></span><span id="DDK_COPP_VIDEO_MINIPORT_DRIVER_KEY_EXCHANGE_TEMPLATE_CODE_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。

使用以下示例代码检索 COPP DirectX VA 设备对象的图形硬件使用的数字证书。

```cpp
VP_STATUS
IoctlCOPPKeyExchange(
    PHW_DEVICE_EXTENSION pHwDeviceExtension,
    PVIDEO_REQUEST_PACKET pVideoRequestPacket
    )
{
    COPP_IO_InputBuffer* pInBuff = pVideoRequestPacket->InputBuffer;
    COPP_DeviceData* pThis = (COPP_DeviceData*)*pInBuff->ppThis;
    GUID* lpout = (GUID*)pVideoRequestPacket->OutputBuffer;
    BYTE* pCertificate = (BYTE*)pInBuff->InputBuffer;
    HRESULT* phr = pInBuff->phr;
     *phr = COPPKeyExchange(pThis, lpout, pCertificate);
    if (*phr == NO_ERROR) {
        pVideoRequestPacket->StatusBlock->Information = pVideoRequestPacket->OutputBufferLength;
    }
    return NO_ERROR;
}
```

 

 





