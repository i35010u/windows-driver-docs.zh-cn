---
title: 扩展的相机控件有效负载
description: KSPROPERTYSETID_ExtendedCameraControl 属性集内的控件属性使用通用负载格式来获取和设置属性数据。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7e849903d5b08ba7ffefbda3b9427cef6b2614b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837077"
---
# <a name="extended-camera-control-payloads"></a>扩展的相机控件有效负载


[KSPROPERTYSETID \_ ExtendedCameraControl](./kspropertysetid-extendedcameracontrol.md)属性集内的控件属性使用通用负载格式来获取和设置属性数据。

## <a name="extended-camera-property-header"></a>扩展照相机属性标头


所有负载都以 [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) 结构开始。 此结构包含具有关联控件标志和功能的 PIN 目标。 根据特定的控件， **功能** 成员将包含控件提供的一组功能。 **Flags** 成员将包含当前设置的或要为控件设置的实际功能。

**PinId** 成员指定目标为相机 pin 或筛选器 pin。 如果该属性是筛选器级别控件，则 **PinId** 设置为 KSCAMERA \_ EXTENDEDPROP \_ FILTERSCOPE。

属性控件为同步或异步。 如果控件是同步的，则 KSCAMERA \_ EXTENDEDPROP \_ cap \_ ASYNCCONTROL 标志设置 **Capabilities** 为 "功能"。 此外，如果控件可取消，则 **功能** 成员包括 KSCAMERA \_ EXTENDEDPROP \_ cap \_ 可取消标志。

负载大小是在大小成员中设置的。 **Size** 的值是有效负载的整个大小。 如果属性仅使用标题，则 **Size**  =  **sizeof** (KSCAMERA \_ EXTENDEDPROP \_ 标头) 。 否则，**大小** 为  =  **sizeof** (KSCAMERA \_ EXTENDEDPROP \_ 标头) + **sizeof** (控件特定数据) 。

## <a name="control-specific-data"></a>控制特定数据


某些属性控件使用其他结构来保存其他数据。 使用单个数据值时，属性数据将在 [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)之后包含 [**KSCAMERA \_ EXTENDEDPROP \_ 值**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)结构。 **KSCAMERA \_ EXTENDEDPROP \_ 值** 结构允许属性将单个值表示为多种数据类型之一。

若要获取或设置其他数据，属性将在 [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)后具有其自己的特殊数据结构。 下面的示例演示了一个驱动程序代码片段，该片段为 \_ \_ [**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ FIELDOFVIEW**](./ksproperty-cameracontrol-extended-fieldofview.md) 属性的 KSPROPERTY 类型 GET 请求设置特定于属性的数据。

```cpp
#define FL_WIDE_ANGLE 35
#define FL_NORMAL     50

PBYTE Payload = (PBYTE)PropData;
PKSCAMERA_EXTENDEDPROP_HEADER ExtendedPropHeader = (PKSCAMERA_EXTENDEDPROP_HEADER)Payload;
PKSCAMERA_EXTENDEDPROP_FIELDOFVIEW ExtendedDataFov = (PKSCAMERA_EXTENDEDPROP_FIELDOFVIEW)(Payload + sizeof(KSCAMERA_EXTENDEDPROP_HEADER));

ExtendedPropHeader->Version = 1;
ExtendedPropHeader->PinId = KSCAMERA_EXTENDEDPROP_FILTERSCOPE;
ExtendedPropHeader->Size = sizeof(KSCAMERA_EXTENDEDPROP_HEADER) + sizeof(KSCAMERA_EXTENDEDPROP_FIELDOFVIEW);
ExtendedPropHeader->Result = 0;
ExtendedPropHeader->Flags = 0;
ExtendedPropHeader->Capability = 0;

ExtendedDataFov->NormalizedFocalLengthX = FL_WIDE_ANGLE;
ExtendedDataFov->NormalizedFocalLengthY = FL_WIDE_ANGLE;
ExtendedDataFov->Flag = 0;
ExtendedDataFov->Reserved = 0;
```

 

