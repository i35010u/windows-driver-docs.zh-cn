---
title: 使用 OPM 处理保护级别
description: 使用 OPM 处理保护级别
ms.assetid: 2d3e5d07-8d6f-44fb-985a-96990538ed29
keywords:
- 保护级别 WDK 显示类型
- 保护级别 WDK 显示 ACP
- 保护级别 WDK 显示，模拟复制保护
- 保护级别 WDK 显示 CGMS A
- 保护级别 WDK 显示内容生成管理系统模拟
- 保护级别 WDK 显示高带宽数字内容保护
- 保护级别 WDK 显示 HDCP
- 保护级别 WDK 显示 DisplayPort 内容保护
- 保护级别 WDK 显示 DPCP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f101195a3dfa4eb8549d9e704b49fd1c98cea70c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340113"
---
# <a name="handling-protection-levels-with-opm"></a>使用 OPM 处理保护级别


每个输出保护类型 (例如，模拟复制保护 (ACP)，[内容生成管理系统模拟 (CGMS A)](cgms-a-standards.md)，高带宽数字内容保护 (HDCP) 和内容保护 DisplayPort (DPCP)) 具有与之关联的保护级别。 有关 ACP 详细信息，请参阅[Rovi (以前称为 Macrovision)](https://go.microsoft.com/fwlink/p/?linkid=71273)网站。 有关 HDCP 详细信息，请参阅[HDCP 规范修订版本 1.1](https://go.microsoft.com/fwlink/p/?linkid=38728)。 有关 DisplayPort 详细信息，请参阅[DisplayPort](https://go.microsoft.com/fwlink/p/?linkid=71382) Web 项目。

图形适配器不需要支持输出保护类型。 但是，图形适配器必须准确地报告它支持的每个图形适配器的输出和当前设置的保护类型为每个输出的保护级别。

ACP 和 CGMS 一个保护模拟电视信号。 目前，OPM 可以使用 ACP 和 CGMS-A 来保护信号从复合输出、 S-视频输出或组件输出。 有关不同的 ACP 和 CGMS 一个保护级别，请参阅[ **DXGKMDT\_OPM\_ACP\_保护\_级别**](https://msdn.microsoft.com/library/windows/hardware/ff560834)和[**DXGKMDT\_OPM\_CGMSA** ](https://msdn.microsoft.com/library/windows/hardware/ff560846)枚举。

HDCP 保护数字视频信号。 目前，OPM 可以使用 HDCP 来保护数据免受数字视频接口 (DVI) 和高清晰度多媒体接口 (HDMI) 连接器的输出。 有关 HDCP 保护级别的信息，请参阅[ **DXGKMDT\_OPM\_HDCP\_保护\_级别**](https://msdn.microsoft.com/library/windows/hardware/ff560878)枚举。

DPCP DisplayPort 输出连接器可防止数字视频信号。

以下部分介绍了如果为特定物理输出连接器以及用于确定物理输出连接器的保护级别的算法创建多个受保护的输出保护级别放置的优先级：

[将优先级分配给保护级别](assigning-precedence-to-protection-levels.md)

[确定物理输出保护级别](determining-the-protection-level-for-a-physical-output.md)

 

 





