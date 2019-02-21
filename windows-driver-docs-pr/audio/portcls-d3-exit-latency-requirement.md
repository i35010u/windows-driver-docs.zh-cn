---
title: PortCls D3 退出滞后时间要求
description: 本主题讨论 Windows 端口类驱动程序 (PortCls) 如何使用新的 Windows 8 界面来操作 D3 睡眠状态的退出延迟要求。
ms.assetid: 3CEFF85B-5A2E-4F85-BCAC-00F1773A8F4D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2844edd1faf7efb1f6e2d871266c30314b584b2f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534240"
---
# <a name="portcls-d3-exit-latency-requirement"></a>PortCls D3 退出滞后时间要求


本主题讨论 Windows 端口类驱动程序 (PortCls) 如何使用新的 Windows 8 界面来操作 D3 睡眠状态的退出延迟要求。

可以放宽当系统进入之外 （如睡眠或连接的待机） 可完全正常工作，以返回到 D0 （全面发挥作用） 的音频适配器所需的退出延迟平台的电源状态。 这使得音频的适配器，以使用睡眠状态深于 D3，即使这些更深层次的状态可能会导致更长退出延迟 （退出时间）。

PortCls 可以现在使用新的电源管理接口来生成新 D3 退出延迟容差，，然后将其告知动态音频微型端口驱动程序。 这些容差表示为[ **PC\_退出\_延迟**](https://msdn.microsoft.com/library/windows/hardware/dn265130)枚举值。

有关新的电源管理界面的详细信息，请参阅[ **IAdapterPowerManagement3**](https://msdn.microsoft.com/library/windows/hardware/jj200330)

 

 




