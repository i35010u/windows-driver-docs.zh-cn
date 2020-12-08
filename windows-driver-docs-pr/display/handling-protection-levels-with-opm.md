---
title: 使用 OPM 处理保护级别
description: 使用 OPM 处理保护级别
keywords:
- 保护级别 WDK 显示，类型为
- 保护级别 WDK 显示，ACP
- 保护级别 WDK 显示，模拟复制保护
- 保护级别 WDK 显示，CGMS-A
- 保护级别 WDK 显示，内容生成管理系统模拟
- 保护级别 WDK 显示，高带宽数字内容保护
- 保护级别 WDK 显示，HDCP
- 保护级别 WDK 显示，DisplayPort 内容保护
- 保护级别 WDK 显示，DPCP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87d32213beaad048a7b478180f8bf7ae0afed1ac
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796262"
---
# <a name="handling-protection-levels-with-opm"></a>使用 OPM 处理保护级别

每个输出保护类型 (例如， [模拟复制保护 (ACP) ](https://business.tivo.com/services/acp-technology)、 [内容生成管理系统模拟 (CGMS-A) ](cgms-a-standards.md)、 [高带宽数字内容保护 (HDCP) ](https://www.digital-cp.com/hdcp-specifications)和 [DisplayPort](https://go.microsoft.com/fwlink/p/?linkid=71382) 内容保护 (DPCP) # A9 具有与其关联的保护级别。

图形适配器不需要支持任何输出保护类型。 但是，图形适配器必须准确地报告它支持的每个图形适配器输出的保护类型以及每个输出的当前设置保护级别。

ACP 和 CGMS-A 保护模拟电视信号。 目前，OPM 可以使用 ACP 和 CGMS 来保护来自复合输出、S-视频输出或组件输出的信号。 有关不同的 ACP 和 CGMS 保护级别的信息，请参阅 [**DXGKMDT_OPM_ACP_PROTECTION_LEVEL**](/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_acp_protection_level) 和 [**DXGKMDT_OPM_CGMSA**](/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_cgmsa) 枚举。

HDCP 保护数字视频信号。 目前，OPM 可以使用 HDCP 来保护 (DVI) 和 High-Definition 多媒体接口 (HDMI) 连接器输出中的数字视频接口的数据。 有关 HDCP 保护级别的信息，请参阅 [**DXGKMDT_OPM_HDCP_PROTECTION_LEVEL**](/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_hdcp_protection_level) 枚举。

DPCP 保护来自 DisplayPort 输出连接器的数字视频信号。

以下各节描述了在为特定物理输出连接器创建了多个受保护的输出时，保护级别上施加的优先级，以及用于确定物理输出连接器保护级别的算法：

[将优先顺序分配到保护级别](assigning-precedence-to-protection-levels.md)

[确定物理输出的保护级别](determining-the-protection-level-for-a-physical-output.md)
