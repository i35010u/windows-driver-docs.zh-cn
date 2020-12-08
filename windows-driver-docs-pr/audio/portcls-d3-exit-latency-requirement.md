---
title: PortCls D3 退出延迟要求
description: 本主题讨论 (PortCls) 的 Windows 端口类驱动程序如何使用新的 Windows 8 接口处理 D3 睡眠状态的退出延迟要求。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6edbce118269ce0961159adf88e9e0da03ee298a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800821"
---
# <a name="portcls-d3-exit-latency-requirement"></a>PortCls D3 退出延迟要求


本主题讨论 (PortCls) 的 Windows 端口类驱动程序如何使用新的 Windows 8 接口处理 D3 睡眠状态的退出延迟要求。

当系统进入 "完全正常工作" (以外的平台电源状态时（例如，睡眠或连接待机) ），音频适配器需要的退出延迟时间才能返回到 D0 (完全正常运行) 可以放松。 这使得音频适配器可以使用除 D3 之外的睡眠状态，即使这些更深层的状态可能会导致退出延迟 (退出时间) 。

PortCls 现在可以使用新的电源管理接口生成新的 D3 出口延迟，然后将其动态地传达给音频微型端口驱动程序。 这些公差表示为 [**PC \_ 出口 \_ 延迟**](/windows-hardware/drivers/ddi/portcls/ne-portcls-_pc_exit_latency) 枚举值。

有关新电源管理接口的详细信息，请参阅 [ **IAdapterPowerManagement3**](/windows-hardware/drivers/ddi/portcls/nn-portcls-iadapterpowermanagement3)

 

