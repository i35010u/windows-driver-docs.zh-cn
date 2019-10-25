---
title: 扩展的相机控件有效负载
description: KSPROPERTYSETID_ExtendedCameraControl 属性集内的控件属性使用通用负载格式来获取和设置属性数据。
ms.assetid: 347413DB-229B-40D7-BD3E-931493EE1FBC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b66fe8aa03d98317e20b6a24de91c8fa3760feb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834416"
---
# <a name="extended-camera-control-payloads"></a>扩展的相机控件有效负载


[KSPROPERTYSETID\_ExtendedCameraControl](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropertysetid-extendedcameracontrol)属性集内的控件属性使用通用负载格式来获取和设置属性数据。

## <a name="extended-camera-property-header"></a>扩展照相机属性标头


所有负载都以[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构开始。 此结构包含具有关联控件标志和功能的 PIN 目标。 根据特定的控件，**功能**成员将包含控件提供的一组功能。 **Flags**成员将包含当前设置的或要为控件设置的实际功能。

**PinId**成员指定目标为相机 pin 或筛选器 pin。 如果该属性是筛选器级别控件，则将**PinId**设置为 KSCAMERA\_EXTENDEDPROP\_FILTERSCOPE。

属性控件为同步或异步。 如果控件是同步的，则 KSCAMERA\_EXTENDEDPROP\_CAPS\_ASYNCCONTROL 标志设置为 "**功能**"。 此外，如果该控件可取消，则**功能**成员包括 KSCAMERA\_EXTENDEDPROP\_CAP\_可取消标志。

负载大小是在大小成员中设置的。 **Size**的值是有效负载的整个大小。 如果属性仅使用标题，则**Size** = **sizeof**（KSCAMERA\_EXTENDEDPROP\_标头）。 否则，**大小** = **sizeof**（KSCAMERA\_EXTENDEDPROP\_标头） + **sizeof**（控制特定数据）。

## <a name="control-specific-data"></a>控制特定数据


某些属性控件使用其他结构来保存其他数据。 在使用单个数据值的情况下，属性数据将包含[**KSCAMERA\_EXTENDEDPROP\_值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)结构，之后[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)。 **KSCAMERA\_EXTENDEDPROP\_值**结构允许属性将单个值表示为多种数据类型之一。

为获取或设置附加数据，属性将在[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)后具有其自己的特殊数据结构。 下面的示例演示了一个驱动程序代码片段，为 KSPROPERTY\_类型设置特定于属性的数据，\_GET 请求[**KSPROPERTY\_CAMERACONTROL\_扩展\_FIELDOFVIEW**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-fieldofview)属性。

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

 

 




