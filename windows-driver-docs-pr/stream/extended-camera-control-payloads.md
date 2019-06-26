---
title: 扩展的相机控件有效负载
description: KSPROPERTYSETID_ExtendedCameraControl 属性集内的控件属性用于获取和设置属性数据使用常见的负载格式。
ms.assetid: 347413DB-229B-40D7-BD3E-931493EE1FBC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81d54c27308b87bb684d89d3b51486361b6fbb2a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384098"
---
# <a name="extended-camera-control-payloads"></a>扩展的相机控件有效负载


中的控件属性[KSPROPERTYSETID\_ExtendedCameraControl](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropertysetid-extendedcameracontrol)属性集使用的通用的有效负载格式，用于获取和设置属性数据。

## <a name="extended-camera-property-header"></a>扩展的相机属性标头


所有负载都开头[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构。 此结构包含在固定的关联的控制标志和功能。 具体取决于特定的控件，**功能**成员将包含一组由控件提供的功能。 **标志**成员将包含的实际功能当前设置或为控件设置。

**PinId**成员指定的目标是相机 PIN 或筛选器的 PIN。 如果该属性是一个筛选器级别控件，则**PinId**设置为 KSCAMERA\_EXTENDEDPROP\_FILTERSCOPE。

属性控制是同步还是异步。 如果控件是同步的然后 KSCAMERA\_EXTENDEDPROP\_CAPS\_中设置 ASYNCCONTROL 标志**功能**。 此外，如果该控件是可取消，则**功能**成员包括 KSCAMERA\_EXTENDEDPROP\_CAPS\_可取消的标志。

Size 成员中设置的有效负载大小。 值**大小**是整个负载的大小。 如果该属性使用仅标头，然后**大小** = **sizeof**(KSCAMERA\_EXTENDEDPROP\_标头)。 否则为**大小** = **sizeof**(KSCAMERA\_EXTENDEDPROP\_标头) + **sizeof**（控制特定的数据）。

## <a name="control-specific-data"></a>控制特定数据


某些属性控件使用的其他结构保存的其他数据。 使用单个数据值时，将包含属性数据[ **KSCAMERA\_EXTENDEDPROP\_值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)结构后[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)。 **KSCAMERA\_EXTENDEDPROP\_值**结构允许以单个值表示为多种数据类型之一的属性。

若要获取或设置额外的数据，属性将具有其自己的特殊数据结构以下[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)。 下面的示例显示了驱动程序代码片段设置属性的特定数据的 KSPROPERTY\_类型\_的 GET 请求[ **KSPROPERTY\_CAMERACONTROL\_扩展\_FIELDOFVIEW** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-fieldofview)属性。

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

 

 




