---
title: 使用 OPM 处理保护级别
description: 使用 OPM 处理保护级别
ms.assetid: 2d3e5d07-8d6f-44fb-985a-96990538ed29
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
ms.openlocfilehash: 5f2ecef8252d46e3983f3e7237496fc0daa74910
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065820"
---
# <a name="handling-protection-levels-with-opm"></a>使用 OPM 处理保护级别


每个输出保护类型 (例如，模拟复制保护 (ACP) 、 [内容生成管理系统模拟 (CGMS-A) ](cgms-a-standards.md)、高带宽数字内容保护 (HDCP) 和 DisplayPort 内容保护 (DPCP) # A9 具有与其关联的保护级别。 有关 ACP 的详细信息，请参阅 [Rovi (以前的 Macrovision) ](https://go.microsoft.com/fwlink/p/?linkid=71273) 网站。 有关 HDCP 的详细信息，请参阅 [Hdcp 规范修订版本 1.1](https://go.microsoft.com/fwlink/p/?linkid=38728)。 有关 DisplayPort 的详细信息，请参阅 [DisplayPort](https://go.microsoft.com/fwlink/p/?linkid=71382) Web 文章。

图形适配器不需要支持任何输出保护类型。 但是，图形适配器必须准确地报告它支持的每个图形适配器输出的保护类型以及每个输出的当前设置保护级别。

ACP 和 CGMS-A 保护模拟电视信号。 目前，OPM 可以使用 ACP 和 CGMS 来保护来自复合输出、S-视频输出或组件输出的信号。 有关不同的 ACP 和 CGMS 保护级别的信息，请参阅 [**DXGKMDT \_ OPM \_ ACP \_ protection \_ LEVEL**](/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_acp_protection_level) 和 DXGKMDT OPM [** \_ \_ CGMSA**](/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_cgmsa) 枚举。

HDCP 保护数字视频信号。 目前，OPM 可以使用 HDCP 来防止数字视频接口 (DVI) 和高清多媒体接口 (HDMI) 连接器输出的数据。 有关 HDCP 保护级别的信息，请参阅 [**DXGKMDT \_ OPM \_ HDCP \_ protection \_ LEVEL**](/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_hdcp_protection_level) 枚举。

DPCP 保护来自 DisplayPort 输出连接器的数字视频信号。

以下各节描述了在为特定物理输出连接器创建了多个受保护的输出时，保护级别上施加的优先级，以及用于确定物理输出连接器保护级别的算法：

[将优先顺序分配到保护级别](assigning-precedence-to-protection-levels.md)

[确定物理输出的保护级别](determining-the-protection-level-for-a-physical-output.md)

 

