---
title: 适用于 Windows 10 的通用照相机驱动程序枚举
description: 提供有关适用于 Windows 10 的通用照相机驱动程序枚举的信息。
ms.date: 03/23/2021
ms.localizationpriority: medium
ms.openlocfilehash: e66738d037ab80020e59b52b2e5c6c41f15f4e08
ms.sourcegitcommit: 2a27786ed72024f064bbfef20933b0d0b429d4b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105106147"
---
# <a name="universal-camera-driver-enumerations-for-windows-10"></a>适用于 Windows 10 的通用照相机驱动程序枚举

适用于 Windows 10 的相机驱动程序接口已聚合到所有设备，并使用通用照相机驱动程序模型。

以下主题提供有关适用于 Windows 10 的通用照相机驱动程序枚举的信息：

| 标题 | 说明 |
|--|--|
| [KSCAMERA_EXTENDEDPROP_FOCUSSTATE](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-kscamera_extendedprop_focusstate) | 此枚举包含焦点状态。 |
| [KSCAMERA_EXTENDEDPROP_MetadataAlignment](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-kscamera_extendedprop_metadataalignment) | 此枚举包含元数据对齐方式的标识符。 |
| [KSCAMERA_EXTENDEDPROP_ROITYPE](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-kscamera_extendedprop_roitype) | 此枚举包含 ROI 类型。 |
| [KSCAMERA_MetadataId](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-kscamera_metadataid) | 此枚举包含元数据项的标识符。 |
| [KSCAMERA_PERFRAMESETTING_ITEM_TYPE](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-kscamera_perframesetting_item_type) | 此枚举包含每帧设置 DDI 的不同项类型。 |
| [KSDEVICE_THERMAL_STATE](/windows-hardware/drivers/ddi/ks/ne-ks-ksdevice_thermal_state) | 用于热量状态更改的 KS 定义的枚举。 |
| [KSEVENT_CAMERAEVENT](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksevent_cameraevent) | KSEVENT_CAMERAEVENT 枚举可由管道用来从驱动程序启用或禁用照相机事件通知的内核流事件集。 |
| [KSPIN_MDL_CACHING_EVENT](/windows-hardware/drivers/ddi/ks/ne-ks-kspin_mdl_caching_event) | 此枚举由操作系统在内部使用。 |
| [KSPPROPERTY_ALLOCATOR_MDLCACHING](/windows-hardware/drivers/ddi/ks/ne-ks-kspproperty_allocator_mdlcaching) | 此枚举由操作系统在内部使用。 |
| [KSPROPERTY_CAMERACONTROL_EXTENDED_PROPERTY](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_cameracontrol_extended_property) | 此枚举包含扩展相机控件。 |
| [KSPROPERTY_CAMERACONTROL_PERFRAMESETTING_PROPERTY](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_cameracontrol_perframesetting_property) | 此枚举包含为每帧属性集定义的属性 Id。 |

## <a name="see-also"></a>另请参阅

[适用于 Windows 10 的通用相机驱动程序设计指南](windows-10-technical-preview-camera-drivers-design-guide.md)

[适用于 Windows 10 的通用照相机驱动程序控件](camera-driver-controls.md)

[适用于 Windows 10 的通用照相机驱动程序功能](camera-driver-functions.md)

[适用于 Windows 10 的通用照相机驱动程序结构](camera-driver-structures.md)

[流媒体设备驱动程序参考](/windows-hardware/drivers/ddi/_stream/index)
