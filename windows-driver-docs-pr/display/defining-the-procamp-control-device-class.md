---
title: 定义 ProcAmp 控制设备类
description: 定义 ProcAmp 控制设备类
ms.assetid: 382f5ecf-ce87-4100-adc7-7006cc7dc5ed
keywords:
- ProcAmp WDK DirectX VA，定义设备类
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00034db803536f6627214801e005ef0579081723
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348924"
---
# <a name="defining-the-procamp-control-device-class"></a>定义 ProcAmp 控制设备类


## <span id="ddk_defining_the_procamp_control_device_class_gg"></span><span id="DDK_DEFINING_THE_PROCAMP_CONTROL_DEVICE_CLASS_GG"></span>


使用下面的示例代码来定义 ProcAmp 控制设备类：

```cpp
// ProcAmp control device class.
struct DXVA_ProcAmpControlDeviceClass : public DXVA_DeviceBaseClass
{
    DXVA_VideoDesc  m_VideoDesc;
    // Uses the base class's constructor.
    DXVA_ProcAmpControlDeviceClass(const GUID& guid, DXVA_DeviceType Type) :
        DXVA_DeviceBaseClass(guid, Type)
    {}
    // The following three functions are part of the 
     // ProcAmp Control DDI.
    HRESULT ProcAmpControlOpenStream(LPDXVA_VideoDesc lpVideoDescription);
    HRESULT ProcAmpControlCloseStream();
    HRESULT ProcAmpControlBlt(
                           LPVOID lpDDSDstSurface,
                           LPVOID lpDDSSrcSurface,
                           DXVA_ProcAmpControlBlt* pCcBlt);
};
```

 

 





