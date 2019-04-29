---
title: 安全数字 (SD) 设备的标识符
description: 安全数字 (SD) 设备的标识符
ms.assetid: d5e112b7-29ed-4950-858c-81fe0d19a902
keywords:
- 设备标识字符串 WDK、 SD 设备
- SD 设备-设备标识字符串 WDK
- 标识符 WDK 设备，SD 设备
- SD 设备 Id WDK 设备安装
- 安全数字设备 Id WDK 设备安装
- 设备 Id WDK 设备安装
- 硬件 Id WDK 设备安装
- 兼容 Id WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91ba0562c4f2d84b2e81d3453ae6c9e28c8e85b0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362993"
---
# <a name="identifiers-for-secure-digital-sd-devices"></a>安全数字 (SD) 设备的标识符


当 SD 总线驱动程序主机控制器套接字中检测到 SD 设备时，它会检查要构造的设备和其函数的 Id 的设备和硬件的卡片的设备配置。 对于 SD 卡组合和多功能 SDIO 设备，总线驱动程序创建一个 PDO 和每个相应的函数的硬件 ID。

由于 SD 内存设备的内部配置是明显不同于 SDIO 设备，SD 总线驱动程序将为 SDIO 设备使用两种不同的硬件 ID 格式、 对 SD 内存设备的一个，另一个。

### <a href="" id="sd-device-ids"></a> SD 设备 id

SD 内存设备的设备 ID 使用以下格式：

SD\\VID_v(2)&OID_o(4)&PID_p(0-5)&REV_n(1).m(1)

其中：

-   *v(2)* 是分配标识卡的制造商 SD 卡关联 (SDA) 由两位十六进制 ID。

-   *o(4)* 是四位十六进制 ID，由 SDA，标识卡的原始设备制造商 (OEM) 和/或卡内容还分配。

-   *p(0-5)* 是一个供应商提供的 ASCII 字符串，0 到 5 的五个字符，指示产品名称和 n(1).m(1) 是两位数，供应商提供，具有两个数字 (例如，6.2) 之间的十进制修订号。

SDIO 设备的设备 ID 使用以下格式：

SD\\VID_v(4)&PID_p(4)

其中：

-   *v(4)* 是由 PCMCIA 和 JEIDA 分配的四位十六进制供应商代码。

-   *p(4)* 是四位十六进制产品和/或修订号供应商将分配给设备。

SD 总线驱动程序从设备的卡信息结构 (CIS) 区域中的 CISTPL_MANFID 元组中提取供应商和产品代码。

### <a href="" id="sd-hardware-ids"></a> SD 硬件 Id

为 SD 内存设备的总线驱动程序提供了两个硬件 Id： 一个与设备 ID 相同，另一个是相同的设备 id，但不包含版本信息。 ID 为修订版本的信息使用以下格式：

SD\\VID_v(2)&OID_o(4)&PID_p(0-5)

其中，为具有设备 ID:

-   *v(2)* 是分配标识卡的制造商 SD 卡关联 (SDA) 由两位十六进制 ID。

-   *o(4)* 是四位十六进制 ID，由 SDA，标识卡的原始设备制造商 (OEM) 和/或卡内容还分配。

-   *p(0-5)* 是一个供应商提供的 ASCII 字符串，0 到 5 的五个字符，用于指示产品名称。

为 SDIO 设备 SD 总线驱动程序提供了单个硬件 ID 都相同设备 id。

### <a href="" id="sd-compatible-ids"></a> SD 兼容 Id

除了设备和硬件 Id，SD 总线驱动程序将生成在某些情况下兼容 ID。

对于 SD 内存设备，总线驱动程序将始终生成以下兼容 ID:

SD\\CLASS_STORAGE

对于 SDIO 设备 SD 总线驱动程序将生成以下兼容 ID 提供的函数基本寄存器 (FBR) 中的值不为零：

SD\\CLASS_c(2)

其中*c(2)* 是两位数的十六进制设备接口代码。

 

 





