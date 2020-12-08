---
title: 定义反交错 Bob 设备类
description: 定义反交错 Bob 设备类
keywords:
- 取消隔行扫描 WDK DirectX VA，bob
- bob 取消隔行扫描 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c29c1364c6347dd0f3e075bbceb98f6b755cc5b1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809595"
---
# <a name="defining-the-deinterlace-bob-device-class"></a>定义反交错 Bob 设备类


## <span id="ddk_defining_the_deinterlace_bob_device_class_gg"></span><span id="DDK_DEFINING_THE_DEINTERLACE_BOB_DEVICE_CLASS_GG"></span>


使用以下示例代码定义隔行扫描 bob 设备类：

```cpp
// Deinterlace bob device class.
struct DXVA_DeinterlaceBobDeviceClass : public DXVA_DeviceBaseClass
{
    DXVA_VideoDesc  m_VideoDesc;
    // Uses the base class's constructor.
    DXVA_DeinterlaceBobDeviceClass(const GUID& guid, DXVA_DeviceType Type) :
        DXVA_DeviceBaseClass(guid, Type)
    {}
    // The following functions are part of the 
     // Deinterlace DDI.
    HRESULT DeinterlaceOpenStream(LPDXVA_VideoDesc lpVideoDescription);
    HRESULT DeinterlaceCloseStream();
    HRESULT DeinterlaceBlt(
                           REFERENCE_TIME  rtTargetFrame,
                           LPRECT  lprcDstRect,
                           LPDDSURFACE  lpDDSDstSurface,
                           LPRECT  lprcSrcRect,
                           LPDXVA_VideoSample  lpDDSrcSurfaces,
                           DWORD  dwNumSurfaces,
                           FLOAT  fAlpha);
    HRESULT DeinterlaceBltEx(
                           REFERENCE_TIME  rtTargetFrame,
                           LPRECT  lprcTargetRect,
                           DXVA_AYUVsample2  BackgroundColor,
                           DWORD  dwDestinationFormat,
                           DWORD  dwDestinationFlags,
                           LPDDSURFACE  lpDDSDstSurface,
                           LPDXVA_VideoSample2  lpDDSrcSurfaces,
                           DWORD  dwNumSurfaces,
                           FLOAT  fAlpha);
};
```

 

 





