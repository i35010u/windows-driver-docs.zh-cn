---
title: 定义反交错 Bob 设备类
description: 定义反交错 Bob 设备类
ms.assetid: 1efe0a08-c3aa-4083-a19f-96e5ba94d517
keywords:
- 取消隔行扫描 WDK DirectX VA bob
- bob 去隔行 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7845cb8019d32368980e189bab971a3a3801ef9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327965"
---
# <a name="defining-the-deinterlace-bob-device-class"></a>定义反交错 Bob 设备类


## <span id="ddk_defining_the_deinterlace_bob_device_class_gg"></span><span id="DDK_DEFINING_THE_DEINTERLACE_BOB_DEVICE_CLASS_GG"></span>


使用下面的示例代码来定义取消隔行扫描 bob 设备类：

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

 

 





