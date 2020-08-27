---
description: 硬件供应商指南
title: 硬件供应商指南
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c38425e307d73a5701fe8a2133fbe921c3b21967
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969108"
---
# <a name="guidance-for-the-hardware-vendor"></a>硬件供应商指南


如果制造便携式设备并需要与 Windows 建立连接，则可以使用以下选项：

-   对于具有非类协议的设备，请提供 WPD 驱动程序。 例如，如果设备使用的自定义协议超过 RS232 来与计算机通信，则必须提供 WPD 驱动程序，以便 WPD 应用程序能够访问设备。
-   对于便携式音乐播放机设备，请在设备上实现类协议，如 MTP。 这将使你的设备与 WPD 兼容，而无需提供驱动程序 (因为 Microsoft 提供了一个) 。
-   对于数字相机，实现类协议，如 PTP/MTP。 MTP 提供了对 PTP 的增强功能，因此是最佳选择。 然而，出于兼容性原因，建议你的 MTP 实现与 PTP 向后兼容。
-   对于移动电话和其他多功能设备，请在设备上实现类协议，如 MTP。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[**WPD 驱动程序概述**](wpd-drivers-overview.md)

 

 





