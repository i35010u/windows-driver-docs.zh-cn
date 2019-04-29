---
title: 定义 COPP 设备类
description: 定义 COPP 设备类
ms.assetid: eb5e7269-fe4c-44d1-9024-f5b1a180e10b
keywords:
- 复制保护 WDK COPP，COPP 设备
- 视频复制保护 WDK COPP，COPP 设备
- COPP WDK DirectX VA，COPP 设备
- 受保护视频 WDK COPP，COPP 设备
- COPP 设备 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d4f2fe1fd6e4e6ba783bb485ee2e75569837e2b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327204"
---
# <a name="defining-the-copp-device-class"></a>定义 COPP 设备类


## <span id="ddk_defining_the_copp_device_class_gg"></span><span id="DDK_DEFINING_THE_COPP_DEVICE_CLASS_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 和更高版本，和 Windows XP SP2 及更高版本。

使用下面的示例代码来定义 COPP 设备类：

```cpp
// COPP device class.
struct DXVA_COPPDeviceClass : public DXVA_DeviceBaseClass
{
    VOID*   m_pThis;
};
```

 

 





