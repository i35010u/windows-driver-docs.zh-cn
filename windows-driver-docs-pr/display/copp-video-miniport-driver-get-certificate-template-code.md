---
title: COPP 视频微型端口驱动程序获取证书模板代码
description: COPP 视频微型端口驱动程序获取证书模板代码
ms.assetid: 13810013-389a-458d-be9d-e81a0b248dec
keywords:
- 证书 WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af62efe54b47df8359169fa80bd4a8197ca5ba70
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373399"
---
# <a name="copp-video-miniport-driver-get-certificate-template-code"></a>COPP 视频微型端口驱动程序获取证书模板代码


## <span id="ddk_copp_video_miniport_driver_get_certificate_template_code_gg"></span><span id="DDK_COPP_VIDEO_MINIPORT_DRIVER_GET_CERTIFICATE_TEMPLATE_CODE_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 和更高版本，和 Windows XP SP2 及更高版本。

使用下面的代码示例检索大小 （字节） COPP DirectX VA 设备对象的图形硬件证书。

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

 

 





