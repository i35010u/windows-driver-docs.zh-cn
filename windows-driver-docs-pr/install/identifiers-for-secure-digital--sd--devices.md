---
title: 安全数字 (SD) 设备的标识符
description: 安全数字 (SD) 设备的标识符
keywords:
- 设备标识字符串 WDK，SD 设备
- 标识字符串 WDK 设备，SD 设备
- 标识符 WDK 设备，SD 设备
- SD 设备 Id WDK 设备安装
- 安全数字设备 Id WDK 设备安装
- 设备 Id WDK 设备安装
- 硬件 Id WDK 设备安装
- 兼容 Id WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7ccdfc7569781998e0c82f9fac2bf84f89d3cb8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829911"
---
# <a name="identifiers-for-secure-digital-sd-devices"></a>安全数字 (SD) 设备的标识符


当 SD 总线驱动程序检测到主机控制器套接字中的 SD 设备时，它会检查卡的设备配置，以便为设备和其功能构建设备和硬件 Id。 对于 SD 组合卡和多功能 SDIO 设备，总线驱动程序会为每个各自的函数创建一个 PDO 和一个硬件 ID。

由于 SD memory 设备的内部配置与 SDIO 设备的内部配置截然不同，因此 SD bus 驱动程序使用两种不同的硬件 ID 格式，一个用于 SD 内存设备，另一个用于 SDIO 设备。

### <a name="sd-device-ids"></a><a href="" id="sd-device-ids"></a> SD 设备 id

SD memory 设备的设备 ID 使用以下格式：

SD \\ VID_v (2) # B0 OID_o (4) # B1 PID_p (0-5) # B2 REV_n (1)  (1) 

其中：

-   *(2)* 是由 SD 卡协会分配的两位十六进制 ID， (标识卡制造商的 SDA) 。

-   *o (4)* 是由 SDA 分配的四位十六进制 ID，用于标识卡的原始设备制造商 (OEM) 和/或卡内容。

-   *p (0-5)* 是供应商提供的 ASCII 字符串，长度为0到 5 5 个字符，指示产品名称，n (1) . m (1) 是两个数字，由供应商提供，修订号，在两个数字之间有一个小数点 (例如 6.2) 。

SDIO 设备的设备 ID 使用以下格式：

SD \\ VID_v (4) # B0 PID_p (4) 

其中：

-   *(4)* 是由 PCMCIA 和 JEIDA 分配的四位十六进制供应商代码。

-   *p (4)* 是供应商分配给设备的四位十六进制产品和/或修订号。

SD bus 驱动程序从设备卡信息结构 (CIS) 区域中的 CISTPL_MANFID 元组中提取供应商和产品代码。

### <a name="sd-hardware-ids"></a><a href="" id="sd-hardware-ids"></a> SD 硬件 Id

对于 SD memory 设备，总线驱动程序提供了两个硬件 Id：一个与设备 ID 相同，另一个与设备 ID 相同，但没有修订信息。 具有修订信息的 ID 使用以下格式：

SD \\ VID_v (2) # B0 OID_o (4) # B1 PID_p (0-5) 

其中，与设备 ID 相同：

-   *(2)* 是由 SD 卡协会分配的两位十六进制 ID， (标识卡制造商的 SDA) 。

-   *o (4)* 是由 SDA 分配的四位十六进制 ID，用于标识卡的原始设备制造商 (OEM) 和/或卡内容。

-   *p (0-5)* 是供应商提供的 ASCII 字符串，其中0到 5 5 个字符，指示产品名称。

对于 SDIO 设备，SD bus 驱动程序提供的单个硬件 ID 与设备 ID 完全相同。

### <a name="sd-compatible-ids"></a><a href="" id="sd-compatible-ids"></a> SD 兼容 Id

除了设备和硬件 Id 之外，SD bus 驱动程序在某些情况下会生成一个兼容的 ID。

对于 SD memory 设备，总线驱动程序总是生成以下兼容 ID：

SD \\ CLASS_STORAGE

对于 SDIO 设备，SD bus 驱动程序会生成以下兼容 ID，前提是函数 basic register (FBR) 不为零：

SD \\ CLASS_c (2) 

其中 *c (2)* 是两位数的十六进制设备接口代码。

 

 





