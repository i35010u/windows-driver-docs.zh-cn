---
Description: Guidance for the Hardware Vendor
title: 硬件供应商的指南
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56f5dddc0b11c2139c132d0ac410d11b980c2316
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525367"
---
# <a name="guidance-for-the-hardware-vendor"></a>硬件供应商的指南


如果制造便携式设备，并需要与 Windows 建立连接，您具有以下选项：

-   对于与非类协议的设备，提供 WPD 驱动程序。 例如，如果你的设备上 RS232 使用自定义协议与计算机进行通信，必须提供 WPD 驱动程序，以便 WPD 应用程序可以访问该设备。
-   对于便携式音乐播放机设备，实现类协议，例如 MTP 设备上。 这将使你能够与 WPD，而无需提供一个驱动程序 （因为 Microsoft 提供了一个） 兼容的设备。
-   对于数字静态相机实现 PTP/MTP 类协议。 MTP PTP，通过提供增强功能，因此较好的选择。 但是，出于兼容性原因，建议您 MTP 的实现是与 PTP 向后的兼容。
-   移动电话和其他多功能设备，实现类协议，如 MTP，在设备上。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[**WPD 驱动程序概述**](wpd-drivers-overview.md)

 

 





