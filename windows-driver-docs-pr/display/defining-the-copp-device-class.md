---
title: 定义 COPP 设备类
description: 定义 COPP 设备类
keywords:
- 复制保护 WDK COPP，COPP 设备
- 视频复制保护 WDK COPP，COPP 设备
- COPP WDK DirectX VA，COPP 设备
- 受保护的视频 WDK COPP，COPP 设备
- COPP 设备 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74da713552213358a860610f6062174904555bcf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809609"
---
# <a name="defining-the-copp-device-class"></a>定义 COPP 设备类


## <span id="ddk_defining_the_copp_device_class_gg"></span><span id="DDK_DEFINING_THE_COPP_DEVICE_CLASS_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。

使用以下示例代码定义 COPP 设备类：

```cpp
// COPP device class.
struct DXVA_COPPDeviceClass : public DXVA_DeviceBaseClass
{
    VOID*   m_pThis;
};
```

 

 





