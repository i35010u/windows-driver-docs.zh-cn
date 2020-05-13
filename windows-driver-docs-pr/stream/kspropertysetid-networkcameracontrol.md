---
title: KSPROPERTYSETID \_ NetworkCameraControl
description: 定义网络摄像机属性集 ID。
ms.date: 04/14/2020
ms.localizationpriority: medium
ms.openlocfilehash: ebe84f7087c67a5f9b6c67e93c9a1ea77ae86da2
ms.sourcegitcommit: 958a5ced83856df22627c06eb42c9524dd547906
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/12/2020
ms.locfileid: "83270432"
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

[**KSPROPERTY_NETWORKCAMERACONTROL_NTP**](https://docs.microsoft.com/windows-hardware/drivers/stream/)

[**KSPROPERTY_NETWORKCAMERACONTROL_URI**](https://docs.microsoft.com/windows-hardware/drivers/stream/)

这些属性名称在[KSPROPERTY_NETWORKCAMERACONTROL_PROPERTY](https://docs.microsoft.com/windows-hardware/drivers/stream/ne-ksmedia-ksproperty_networkcameracontrol_property)枚举中定义。
