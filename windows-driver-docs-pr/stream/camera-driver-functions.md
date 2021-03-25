---
title: 适用于 Windows 10 的通用照相机驱动程序功能
description: 提供有关适用于 Windows 10 的通用照相机驱动程序功能的信息。
ms.date: 03/23/2021
ms.localizationpriority: medium
ms.custom: contperf-fy21q3
ms.openlocfilehash: 4f5198f260038b0da63b56c3fb4828a65b6b6abb
ms.sourcegitcommit: 2a27786ed72024f064bbfef20933b0d0b429d4b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105106153"
---
# <a name="universal-camera-driver-functions-for-windows-10"></a>适用于 Windows 10 的通用照相机驱动程序功能

适用于 Windows 10 的相机驱动程序接口已聚合到所有设备，并使用通用照相机驱动程序模型。

以下主题提供有关适用于 Windows 10 的通用照相机驱动程序功能的信息：

| 标题 | 说明 |
|--|--|
| [KsAcquireCachedMdl](/windows-hardware/drivers/ddi/ks/nf-ks-ksacquirecachedmdl) | 此函数用于获取由 KS 端口驱动程序缓存的 MDL。 内核模式驱动程序使用函数来获取由 Avstream 驱动程序生成的管道提供的示例的 MDL。 |
| [KsDeviceRegisterThermalDispatch](/windows-hardware/drivers/ddi/ks/nf-ks-ksdeviceregisterthermaldispatch) | Avstream 微型端口驱动程序使用此函数为带有 KS 端口驱动程序的热量通知注册回调。 |
| [KsGenerateThermalEvent](/windows-hardware/drivers/ddi/ks/nf-ks-ksgeneratethermalevent) | 此函数由 (微型端口驱动程序) 的客户端使用，该驱动程序不想订阅热量管理器，而是想要自行进行热量管理。 |
| [KsInitializeDeviceProfile](/windows-hardware/drivers/ddi/ks/nf-ks-ksinitializedeviceprofile) | 必须由所有微型端口驱动程序调用 KsInitializeDeviceProfile API，以初始化配置文件存储并发布设备配置文件。 |
| [KsPersistDeviceProfile](/windows-hardware/drivers/ddi/ks/nf-ks-kspersistdeviceprofile) | KsPersistDeviceProfile API 将配置文件信息提交到持久存储区。 |
| [KsPublishDeviceProfile](/windows-hardware/drivers/ddi/ks/nf-ks-kspublishdeviceprofile) | 调用 KsPublishDeviceProfile API 来发布设备配置文件信息。 |
| [KsReleaseCachedMdl](/windows-hardware/drivers/ddi/ks/nf-ks-ksreleasecachedmdl) | KsReleaseCachedMdl 函数用于释放 KsAcquireCachedMdl 调用获取的 MDL。 |

## <a name="see-also"></a>另请参阅

[适用于 Windows 10 的通用相机驱动程序设计指南](windows-10-technical-preview-camera-drivers-design-guide.md)

[适用于 Windows 10 的通用照相机驱动程序控件](camera-driver-controls.md)

[适用于 Windows 10 的通用照相机驱动程序枚举](camera-driver-enumerations.md)

[适用于 Windows 10 的通用照相机驱动程序结构](camera-driver-structures.md)

[流媒体设备驱动程序参考](/windows-hardware/drivers/ddi/_stream/index)
