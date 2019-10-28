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
ms.openlocfilehash: 888c408ce51ded2a2d88ffe6018f63e34661e793
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838907"
---
# <a name="handling-protection-levels-with-opm"></a>使用 OPM 处理保护级别


每种输出保护类型（例如，模拟复制保护（ACP）、[内容生成管理系统模拟（CGMS）](cgms-a-standards.md)、高带宽数字内容保护（HDCP）和 DisplayPort 内容保护（DPCP））都具有保护级别与其关联。 有关 ACP 的详细信息，请参阅[Rovi （以前称为 Macrovision）](https://go.microsoft.com/fwlink/p/?linkid=71273)网站。 有关 HDCP 的详细信息，请参阅[Hdcp 规范修订版本 1.1](https://go.microsoft.com/fwlink/p/?linkid=38728)。 有关 DisplayPort 的详细信息，请参阅[DisplayPort](https://go.microsoft.com/fwlink/p/?linkid=71382) Web 文章。

图形适配器不需要支持任何输出保护类型。 但是，图形适配器必须准确地报告它支持的每个图形适配器输出的保护类型以及每个输出的当前设置保护级别。

ACP 和 CGMS-A 保护模拟电视信号。 目前，OPM 可以使用 ACP 和 CGMS 来保护来自复合输出、S-视频输出或组件输出的信号。 有关不同的 ACP 和 CGMS 保护级别的信息，请参阅[**DXGKMDT\_OPM\_ACP\_保护\_级别**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_acp_protection_level)和[**DXGKMDT\_OPM\_CGMSA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_cgmsa)枚举。

HDCP 保护数字视频信号。 目前，OPM 可以使用 HDCP 来保护来自数字视频接口（DVI）和高清晰多媒体接口（HDMI）连接器输出的数据。 有关 HDCP 保护级别的信息，请参阅[**DXGKMDT\_OPM\_HDCP\_保护\_级别**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_hdcp_protection_level)枚举。

DPCP 保护来自 DisplayPort 输出连接器的数字视频信号。

以下各节描述了在为特定物理输出连接器创建了多个受保护的输出时，保护级别上施加的优先级，以及用于确定物理输出连接器保护级别的算法：

[将优先级分配到保护级别](assigning-precedence-to-protection-levels.md)

[确定物理输出的保护级别](determining-the-protection-level-for-a-physical-output.md)

 

 





