---
title: COPP 状态事件
description: COPP 状态事件
ms.assetid: e9d6bb04-9abd-4864-b359-3c8331843968
keywords:
- 复制保护 WDK COPP，状态
- 视频复制保护 WDK COPP，状态
- COPP WDK DirectX VA，status
- 受保护的视频 WDK COPP，状态
- 状态信息 WDK COPP
- 状态事件 WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e5dfefb3c0ea2222f383b81c971a134387c61ae
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064359"
---
# <a name="copp-status-events"></a>COPP 状态事件


## <span id="ddk_copp_status_events_gg"></span><span id="DDK_COPP_STATUS_EVENTS_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。

外部事件可以更改应用于连接器的保护性质，甚至可以修改连接器的类型。 当驱动程序收到对其 [*COPPQueryStatus*](./coppquerystatus.md) 函数的调用时，视频微型端口驱动程序必须将这些事件报告给 COPP 应用程序。 在事件发生后，视频微型端口驱动程序必须通过仅在下一次调用 *COPPQueryStatus* 时返回指定的标志来报告以下外部事件：

-   连接完整性：如果计算机和显示设备之间的连接已拔出，则视频微型端口驱动程序应 \_ 在[**DXVA \_ COPPStatusData**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusdata)结构、 [**DXVA \_ COPPStatusDisplayData**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusdisplaydata)结构、DXVA [** \_ COPPStatusHDCPKeyData**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatushdcpkeydata)结构或[**DXVA \_ COPPStatusSignalingCmdData**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatussignalingcmddata)结构的**dwFlags**成员中设置 COPP LinkLost 标志。

-   连接器重新配置：如果用户导致物理连接器的配置发生更改，则视频微型端口驱动程序应 \_ 在 DXVA **dwFlags** \_ COPPStatusData、DXVA \_ COPPSTATUSDISPLAYDATA、DXVA \_ COPPStatusHDCPKeyData 或 DXVA \_ COPPSTATUSSIGNALINGCMDDATA 结构的 dwFlags 成员中设置 COPP RenegotiationRequired 标志。

视频微型端口驱动程序返回指向 \_ \_ \_ \_ [**DXVA \_ COPPStatusHDCPKeyData**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusoutput)结构的**DXVA**数组成员中 DXVA COPPStatusData、DXVA COPPStatusDisplayData、COPPStatusSignalingCmdData COPPStatus 或 DXVA COPPStatusOutput 结构的指针。 指向 DXVA COPPStatusOutput 的指针 \_ 通过[*COPPQueryStatus*](./coppquerystatus.md)的*pOutput*参数返回。

例如，请考虑两个 media 播放应用程序： A 和 B，每个应用程序通过 COPP，将计算机连接到显示监视器的连接器的 HDCP 保护级别。 每个应用程序都控制自己唯一的 COPP DirectX VA 设备。 如果连接器已拔出，则下一次应用程序启动 [*COPPQueryStatus*](./coppquerystatus.md) 请求到其 COPP 设备时，视频微型端口驱动程序应返回 COPP \_ LinkLost 标志。

假设应用程序 A 是在其 COPP 设备上发起对 [*COPPQueryStatus*](./coppquerystatus.md) 的调用的第一个。 然后，应用程序 A 会接收 COPP \_ LinkLost 标志，并相应地进行操作。 如果应用程序 A 启动后续的 *COPPQueryStatus* 调用，则它不应收到 COPP \_ LinkLost 标志，除非连接器再次被拔出。 当应用程序 B 在其 COPP 设备上启动对 *COPPQueryStatus* 的调用时，它会接收 COPP \_ LinkLost 标志并相应地进行操作。 同样，应用程序 B 不应再次收到 COPP \_ LinkLost 标志，直到连接器再次被拔出。

 

