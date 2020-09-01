---
title: KSPROPERTY \_ RAW \_ AVC \_ CMD
description: KSPROPERTY \_ raw \_ AVC \_ CMD 属性发出原始 AV/C 命令。 仅 IEEE 1394 总线设备支持原始 AV/C 命令。
ms.assetid: f3ff3815-0f4f-4fcb-89bd-e77d8002813c
keywords:
- KSPROPERTY_RAW_AVC_CMD 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_RAW_AVC_CMD
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 06/18/2020
ms.localizationpriority: medium
ms.openlocfilehash: 0fec56871365aba35981ac242c5b26366a97be36
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190875"
---
# <a name="ksproperty_raw_avc_cmd"></a>KSPROPERTY \_ RAW \_ AVC \_ CMD

KSPROPERTY \_ raw \_ AVC \_ CMD 属性发出原始 AV/C 命令。 仅 IEEE 1394 总线设备支持原始 AV/C 命令。

## <a name="usage-summary-table"></a>使用情况摘要表

| 获取 | 设置 | 目标 | 属性描述符类型 | 属性值类型 |
|--|--|--|--|--|
| 是 | 是 | 设备 | [**KSPROPERTY_EXTXPORT_S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s) | Embedded **RawAVC** 结构 |

 (操作数据) 的属性值是**RawAVC** \_ \_ 用于描述要运行的原始 AV/C 命令的 KSPROPERTY EXTXPORT S 结构的嵌入 RawAVC 成员。

## <a name="remarks"></a>备注

此属性仅可用于可支持 AV/C 命令的设备，以及[**KSPROPERTY \_ EXTDEVICE \_ 端口**](ksproperty-extdevice-port.md) \_ \_ 在[**KSPROPERTY \_ EXTDEVICE \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extdevice_s)结构的**DevPort**成员中返回开发端口1394的设备。

适用于 IEEE 1394 设备的驱动程序开发人员可以选择支持其驱动程序中的此属性，以便扩展标准接口不支持的设备传输控件， (例如用户模式 **IAMExtTransport** COM 接口方法 **put \_ 模式** 和 **get \_ 模式**) 。

不需要在 USB 设备上实现对此属性的支持，因为 [Usb 视频类驱动程序](./usb-video-class-driver.md) 提供了此功能。 通常，应用程序可以使用 **IKsControl** COM 接口控制 IEEE 1394 设备。 但是， **IKsControl** COM 接口并不提供支持可通过 USB 和 IEEE 1394 总线移植的磁带搜寻的标准方法。 因此，若要执行磁带搜索，调用方必须使用 **DeviceIoControl** 函数而不是 **IKsControl** COM 接口。 调用方在 1394 AV/C 设备上执行磁带搜索，使用具有绝对跟踪号的原始 AV/C 命令 (ATN) 或要搜索的时间代码。 这是此属性不适用于 USB 设备的主要原因。

有关 USB 和1394设备上的磁带位置搜索之间的差异的详细信息，请参阅 [数字视频应用程序兼容性 (DOC 下载) ](https://go.microsoft.com/fwlink/?linkid=2085071) 白皮书。

## <a name="requirements"></a>要求

| &nbsp; | &nbsp; |
| --- | --- |
| **标头** | Ksmedia (包含 Ksmedia)  |

## <a name="see-also"></a>另请参阅

[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY \_ EXTXPORT \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s)