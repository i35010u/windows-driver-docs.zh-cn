---
title: PortCls D3 退出延迟要求
description: 本主题讨论 Windows 端口类驱动程序 (PortCls) 如何使用新的 Windows 8 界面来操作 D3 睡眠状态的退出延迟要求。
ms.assetid: 3CEFF85B-5A2E-4F85-BCAC-00F1773A8F4D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6806439ae169eedb85983a071f8346a1c54f53b1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362562"
---
# <a name="portcls-d3-exit-latency-requirement"></a>PortCls D3 退出延迟要求


本主题讨论 Windows 端口类驱动程序 (PortCls) 如何使用新的 Windows 8 界面来操作 D3 睡眠状态的退出延迟要求。

可以放宽当系统进入之外 （如睡眠或连接的待机） 可完全正常工作，以返回到 D0 （全面发挥作用） 的音频适配器所需的退出延迟平台的电源状态。 这使得音频的适配器，以使用睡眠状态深于 D3，即使这些更深层次的状态可能会导致更长退出延迟 （退出时间）。

PortCls 可以现在使用新的电源管理接口来生成新 D3 退出延迟容差，，然后将其告知动态音频微型端口驱动程序。 这些容差表示为[ **PC\_退出\_延迟**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ne-portcls-_pc_exit_latency)枚举值。

有关新的电源管理界面的详细信息，请参阅[ **IAdapterPowerManagement3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iadapterpowermanagement3)

 

 




