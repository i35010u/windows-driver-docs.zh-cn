---
title: KSPROPERTY \_ CAMERACONTROL \_ 焦距 \_
description: KSPROPERTY \_ CAMERACONTROL \_ 焦距 \_ 属性检索照相机的焦距信息。
ms.assetid: a7fba5e4-abd1-46ae-b93c-5fede0249771
keywords:
- KSPROPERTY_CAMERACONTROL_FOCAL_LENGTH 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_FOCAL_LENGTH
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 06/18/2020
ms.localizationpriority: medium
ms.openlocfilehash: f93e1ff10e42f369aa7f245ebfaf79b83eb27454
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192551"
---
# <a name="ksproperty_cameracontrol_focal_length"></a>KSPROPERTY \_ CAMERACONTROL \_ 焦距 \_

KSPROPERTY \_ CAMERACONTROL \_ 焦距 \_ 属性检索照相机的焦距信息。

## <a name="usage-summary-table"></a>使用情况摘要表

| 获取 | 设置 | 目标 | 属性描述符类型 | 属性值类型 |
|--|--|--|--|--|
| 是 | 否 | 筛选器或节点 | [**KSPROPERTY_CAMERACONTROL_FOCAL_LENGTH_S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_focal_length_s)或[ **KSPROPERTY_CAMERACONTROL_NODE_FOCAL_LENGTH_S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_focal_length_s) | LONG |

 (操作数据) 的属性值是指定相机焦距的 LONG。

## <a name="remarks"></a>备注

您可以使用此属性请求来解释缩放值。 缩放范围应介于**lObjectiveFocalLengthMin** / **lOcularFocalLength**和**lObjectiveFocalLengthMax** / **lOcularFocalLength**之间。  (**lOcularFocalLength**、 **lObjectiveFocalLengthMin**和 **lObjectiveFocalLengthMax** 是 [**KSPROPERTY \_ CAMERACONTROL \_ 焦距 \_ \_ **](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_focal_length_s) s 和 [**KSPROPERTY \_ CAMERACONTROL \_ 节点 \_ 焦 \_ 长度 \_ s**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_focal_length_s) 结构的成员。 ) 

例如，如果 **lObjectiveFocalLengthMax** = 105， **lOcularFocalLength** = 35，则此照相机的最大视觉缩放比率为105/35，即为3。

另请参阅 USB 视频类设备类规范的 " *光学缩放* " 部分。 此规范可在 [USB 实现论坛](https://www.usb.org/) 网站上找到。

## <a name="requirements"></a>要求

| &nbsp; | &nbsp; |
| --- | --- |
| **标头** | Ksmedia (包含 Ksmedia)  |

## <a name="see-also"></a>另请参阅

[**KSPROPERTY \_ CAMERACONTROL \_ 焦距 \_ \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_focal_length_s)

[**KSPROPERTY \_ CAMERACONTROL \_ 节点 \_ 焦 \_ 长度 \_**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_focal_length_s)

[**KSPROPERTY \_ CAMERACONTROL \_ 缩放**](ksproperty-cameracontrol-zoom.md)

[**KSPROPERTY \_ CAMERACONTROL \_ ZOOM \_ 相对**](ksproperty-cameracontrol-zoom-relative.md)