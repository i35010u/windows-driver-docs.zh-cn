---
title: COPP 视频微型端口驱动程序密钥交换模板代码
description: COPP 视频微型端口驱动程序密钥交换模板代码
ms.assetid: 5c0de949-e460-4f01-a762-706eac3abee0
keywords:
- 密钥交换 WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cffbc50947b0358709dd9800c2c8678e752a22f9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555212"
---
# <a name="copp-video-miniport-driver-key-exchange-template-code"></a>COPP 视频微型端口驱动程序密钥交换模板代码


## <span id="ddk_copp_video_miniport_driver_key_exchange_template_code_gg"></span><span id="DDK_COPP_VIDEO_MINIPORT_DRIVER_KEY_EXCHANGE_TEMPLATE_CODE_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 和更高版本，和 Windows XP SP2 及更高版本。

使用下面的代码示例检索数字证书的图形硬件用于 COPP DirectX VA 设备对象。

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

 

 





