---
title: KSPROPERTYSETID \_ NetworkCameraControl
description: 定义网络摄像机属性集 ID。
ms.date: 07/07/2020
ms.localizationpriority: medium
ms.openlocfilehash: f8fc6ec8b7f6f3b4de57c920c1b7d590ecaae6e6
ms.sourcegitcommit: 8b6d83bcedea8c872ec8c7df874344421a39dd57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/08/2020
ms.locfileid: "86128883"
---
# <a name="kspropertysetid_networkcameracontrol"></a>KSPROPERTYSETID \_ NetworkCameraControl

*Ksmedia*头文件定义**KSPROPERTYSETID \_ NetworkCameraControl**属性集 ID，如下所示：

```cpp
#define STATIC_KSPROPERTYSETID_NetworkCameraControl \
    0xe780f09, 0x5745, 0x4e3a,  0xbc, 0x9f, 0xf2, 0x26, 0xea, 0x43, 0xa6, 0xec
DEFINE_GUIDSTRUCT("0E780F09-5745-4E3A-BC9F-F226EA43A6EC", KSPROPERTYSETID_NetworkCameraControl);
#define KSPROPERTYSETID_NetworkCameraControl DEFINE_GUIDNAMED(KSPROPERTYSETID_NetworkCameraControl)
```

**KSPROPERTYSETID \_ NetworkCameraControl**属性集包含以下属性：

[**KSPROPERTY_NETWORKCAMERACONTROL_NTP**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-networkcameracontrol-ntp)

[**KSPROPERTY_NETWORKCAMERACONTROL_URI**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-networkcameracontrol-uri)

这些属性名称在[KSPROPERTY_NETWORKCAMERACONTROL_PROPERTY](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_networkcameracontrol_property)枚举中定义。
