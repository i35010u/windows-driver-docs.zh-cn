---
title: KSPROPERTYSETID \_ NetworkCameraControl
description: 定义网络摄像机属性集 ID。
ms.date: 07/07/2020
ms.localizationpriority: medium
ms.openlocfilehash: 7cd4e5c5d08cea86e0f02927b567ee2d0994f60d
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104454"
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

[**KSPROPERTY_NETWORKCAMERACONTROL_NTP**](./ksproperty-networkcameracontrol-ntp.md)

[**KSPROPERTY_NETWORKCAMERACONTROL_URI**](./ksproperty-networkcameracontrol-uri.md)

这些属性名称在 [KSPROPERTY_NETWORKCAMERACONTROL_PROPERTY](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_networkcameracontrol_property) 枚举中定义。