---
title: COPP 视频微型端口驱动程序获取证书模板代码
description: COPP 视频微型端口驱动程序获取证书模板代码
keywords:
- 证书 WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ba0de93b0f52d92870c421332579870b7f06295
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821565"
---
# <a name="copp-video-miniport-driver-get-certificate-template-code"></a>COPP 视频微型端口驱动程序获取证书模板代码


## <span id="ddk_copp_video_miniport_driver_get_certificate_template_code_gg"></span><span id="DDK_COPP_VIDEO_MINIPORT_DRIVER_GET_CERTIFICATE_TEMPLATE_CODE_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。

使用以下示例代码检索 COPP DirectX VA 设备对象的图形硬件证书的大小（以字节为单位）。

```cpp
VP_STATUS
IoctlCOPPGetCertificateLength(
    PHW_DEVICE_EXTENSION pHwDeviceExtension,
    PVIDEO_REQUEST_PACKET pVideoRequestPacket
    )
{
    COPP_IO_InputBuffer* pInBuff = pVideoRequestPacket->InputBuffer;
    COPP_DeviceData* pThis = (COPP_DeviceData*)*pInBuff->ppThis;
    HRESULT* phr = pInBuff->phr;
     *phr = COPPGetCertificateLength(pThis, (ULONG*)pVideoRequestPacket->OutputBuffer);
    if (*phr == NO_ERROR) {
        pVideoRequestPacket->StatusBlock->Information = sizeof(ULONG);
    }
    return NO_ERROR;
}
```

 

 





