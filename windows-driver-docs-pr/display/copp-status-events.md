---
title: COPP 状态事件
description: COPP 状态事件
ms.assetid: e9d6bb04-9abd-4864-b359-3c8331843968
keywords:
- 复制保护 WDK COPP，状态
- 视频复制保护 WDK COPP，状态
- COPP WDK DirectX va，因此状态
- 受保护视频 WDK COPP 状态
- WDK COPP 的状态信息
- 状态事件 WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5b78dbafc4a5a923982a57983d1dd3062055d2b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569319"
---
# <a name="copp-status-events"></a>COPP 状态事件


## <span id="ddk_copp_status_events_gg"></span><span id="DDK_COPP_STATUS_EVENTS_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 和更高版本，和 Windows XP SP2 及更高版本。

外部事件可以更改的特性应用于连接器或甚至修改类型的连接器的保护。 微型端口驱动程序必须报告这些事件对 COPP 应用程序时驱动程序接收到调用其[ *COPPQueryStatus* ](https://msdn.microsoft.com/library/windows/hardware/ff539652)函数。 微型端口驱动程序必须报告以下外部事件，通过仅在下一步调用返回指定的标志*COPPQueryStatus*事件发生后：

-   连接完整性：如果在计算机和显示设备之间的连接变得拔出，微型端口驱动程序应设置 COPP\_LinkLost 标志**dwFlags**的成员[ **DXVA\_COPPStatusData** ](https://msdn.microsoft.com/library/windows/hardware/ff563154)结构[ **DXVA\_COPPStatusDisplayData** ](https://msdn.microsoft.com/library/windows/hardware/ff563157)结构[ **DXVA\_COPPStatusHDCPKeyData** ](https://msdn.microsoft.com/library/windows/hardware/ff563896)结构，则[ **DXVA\_COPPStatusSignalingCmdData** ](https://msdn.microsoft.com/library/windows/hardware/ff563905)结构。

-   连接器主要副本重新配置：如果用户导致要更改的物理连接器配置，微型端口驱动程序应设置 COPP\_RenegotiationRequired 标志**dwFlags** DXVA 成员\_COPPStatusData，DXVA\_COPPStatusDisplayData、 DXVA\_COPPStatusHDCPKeyData 或 DXVA\_COPPStatusSignalingCmdData 结构。

微型端口驱动程序返回一个指向 DXVA\_COPPStatusData、 DXVA\_COPPStatusDisplayData、 DXVA\_COPPStatusHDCPKeyData 或 DXVA\_中COPPStatusSignalingCmdData结构**COPPStatus**的数组成员[ **DXVA\_COPPStatusOutput** ](https://msdn.microsoft.com/library/windows/hardware/ff563903)结构。 指向 DXVA\_通过返回 COPPStatusOutput *pOutput*参数[ *COPPQueryStatus*](https://msdn.microsoft.com/library/windows/hardware/ff539652)。

例如，考虑两个媒体播放应用程序，A 和 B，每个控制，通过 COPP，将计算机附加到显示监视器的连接器的 HDCP 保护级别。 每个应用程序控制其自己唯一的 COPP DirectX VA 设备。 如果有连接器变得拔出，则下一次任一应用程序启动[ *COPPQueryStatus* ](https://msdn.microsoft.com/library/windows/hardware/ff539652)请求到其 COPP 设备时，微型端口驱动程序应返回 COPP\_LinkLost 标志。

假定应用程序 A 是第一个向发起呼叫[ *COPPQueryStatus* ](https://msdn.microsoft.com/library/windows/hardware/ff539652)其 COPP 设备上。 应用程序，然后接收 COPP\_LinkLost 标志，并做出相应。 如果应用程序 A 启动的后续*COPPQueryStatus*调用，它不应在收到 COPP\_LinkLost 标志，除非该连接器将再次变为拔出。 当应用程序 B 启动对调用*COPPQueryStatus*其 COPP 在设备上，它接收 COPP\_LinkLost 标志，并做出相应。 同样，应用程序 B 不应收到 COPP\_连接器才能再次 LinkLost 标志将再次变为拔出。

 

 





