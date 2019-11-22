---
title: 报告受保护输出的状态
description: 报告受保护输出的状态
ms.assetid: 9945ae9c-1c11-4266-8a5c-d0ffe5ba4b5f
keywords:
- OPM WDK 显示，受保护的输出状态
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a0547458402743eca135b179cece5caf6155bfd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829601"
---
# <a name="reporting-status-of-a-protected-output"></a>报告受保护输出的状态


外部事件可以更改应用于连接器的保护性质，甚至可以修改连接器的类型。 当驱动程序收到对其[**DxgkDdiOPMGetInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_information)或[**DxgkDdiOPMGetCOPPCompatibleInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_copp_compatible_information)函数的调用时，显示微型端口驱动程序必须将这些事件报告给 OPM 应用程序。 显示微型端口驱动程序必须报告以下外部事件，只需在事件发生后对*DxgkDdiOPMGetInformation*或*DxgkDdiOPMGetCOPPCompatibleInformation*的下一次调用返回[**DXGKMDT\_OPM\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_status)枚举：

<span id="Connection_working_properly"></span><span id="connection_working_properly"></span><span id="CONNECTION_WORKING_PROPERLY"></span>连接工作正常  
如果计算机与显示设备之间的连接工作正常，则显示微型端口驱动程序应将 "DXGKMDT\_OPM"\_状态\_"正常状态" 标志设置为 "\_DXGKMDT" 的**ulStatusFlags**成员中的 "正常状态" 标记[ **\_标准\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_standard_information)， [**OPM\_DXGKMDT\_实际\_输出\_格式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_actual_output_format)， [**OPM\_DXGKMDT\_OPM\_和\_ACP\_信号**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_acp_and_cgmsa_signaling)或[**DXGKMDT\_OPM\_连接\_HDCP\_设备\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_connected_hdcp_device_information)结构。

<span id="Connection_integrity"></span><span id="connection_integrity"></span><span id="CONNECTION_INTEGRITY"></span>连接完整性  
如果计算机和显示设备已断开连接，则显示微型端口驱动程序应将 "DXGKMDT\_OPM\_STATUS\_" 链接\_"DXGKMDT\_OPM 的**ulStatusFlags**成员中的" 丢失状态 "标志设置为" DXGKMDT\_OPM\_实际\_输出\_格式，DXGKMDT\_OPM\_ACP\_和\_CGMSA\_信号或 DXGKMDT\_OPM\_连接\_HDCP\_设备\_信息结构。\_\_

<span id="Connector_reconfigurations"></span><span id="connector_reconfigurations"></span><span id="CONNECTOR_RECONFIGURATIONS"></span>连接器重新连接  
如果最终用户导致物理连接器的配置发生更改，则显示微型端口驱动程序应将 "DXGKMDT\_\_OPM" 状态设置为 "DXGKMDT\_OPM 的**ulStatusFlags**成员中\_重新协商\_必需的状态标志"，DXGKMDT\_OPM\_实际\_输出\_格式，DXGKMDT\_OPM\_ACP\_和\_CGMSA\_信号或 DXGKMDT\_OPM\_连接\_HDCP\_设备\_信息结构。\_\_

<span id="Tampering"></span><span id="tampering"></span><span id="TAMPERING"></span>篡改  
如果出现篡改图形适配器或适配器的显示微型端口驱动程序的情况，则显示微型端口驱动程序应将 "DXGKMDT\_\_\_OPM" 设置为 "DXGKMDT\_OPM 的 UlStatusFlags 成员中\_检测到的状态标志" 设置为 " "，DXGKMDT\_OPM\_实际\_输出\_格式，DXGKMDT\_OPM\_ACP\_和\_CGMSA\_信号或 DXGKMDT\_OPM\_连接\_HDCP\_设备\_信息结构。\_\_

<span id="Revoked_HDCP_device"></span><span id="revoked_hdcp_device"></span><span id="REVOKED_HDCP_DEVICE"></span>已吊销 HDCP 设备  
如果已吊销的高带宽数字内容保护（HDCP）设备直接或间接连接到连接器，且已启用 HDCP，则显示微型端口驱动程序应将 DXGKMDT\_OPM\_\_状态设置为 "已撤消\_HDCP\_设备在 DXGKMDT\_OPM 的**ulStatusFlags**成员中\_附加状态标志\_标准\_信息或 DXGKMDT\_OPM\_实际\_输出\_格式结构。 如果未启用 HDCP，则无需驱动程序设置此状态标志。 驱动程序仅通过对其[**DxgkDdiOPMGetInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_information)函数的调用来设置此状态值，以确定是否已启用 HDCP。

显示微型端口驱动程序返回指向 DXGKMDT\_OPM 的指针\_标准\_信息、DXGKMDT\_OPM\_实际\_输出\_格式、DXGKMDT\_OPM\_ACP\_和\_CGMSA\_信号，或 DXGKMDT\_OPM\_连接\_HDCP\_\_\_\_\_ [**信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_requested_information)结构。 指向 DXGKMDT\_OPM 的指针\_请求的\_信息通过*DxgkDdiOPMGetInformation*或*DxgkDdiOPMGetCOPPCompatibleInformation*的*RequestedInformation*参数返回。

例如，请考虑两个媒体播放应用程序： A 和 B。每个应用程序通过 OPM，将计算机连接到显示监视器的连接器的 HDCP 保护级别进行控制。 每个应用程序都控制其自己的唯一受保护的输出。 如果连接器已拔出，则下一次应用程序启动*DxgkDdiOPMGetInformation*或*DxgkDdiOPMGetCOPPCompatibleInformation*对其受保护的输出的请求时，显示微型端口驱动程序应返回 DXGKMDT\_OPM\_状态\_链接\_丢失状态标志。

假设应用程序 A 是在其受保护的输出中启动对*DxgkDdiOPMGetInformation*或*DxgkDdiOPMGetCOPPCompatibleInformation*的调用。 然后，应用程序 A 会接收 DXGKMDT\_OPM\_状态\_链接\_丢失标志，并相应地采取措施。 如果应用程序 A 启动后续的*DxgkDdiOPMGetInformation*或*DxgkDdiOPMGetCOPPCompatibleInformation*调用，则它不应收到 DXGKMDT\_OPM\_状态\_LINK\_丢失标志，除非连接器再次被拔出。 当应用程序 B 在其受保护的输出中启动对*DxgkDdiOPMGetInformation*或*DxgkDdiOPMGetCOPPCompatibleInformation*的调用时，它将接收 DXGKMDT\_OPM\_状态\_链接\_丢失标志并将其作用并. 同样，应用程序 B 不应收到 DXGKMDT\_OPM\_状态\_链接\_丢失标志，直到连接器再次拔出。

 

 





