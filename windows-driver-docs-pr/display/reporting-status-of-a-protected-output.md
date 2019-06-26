---
title: 报告受保护输出的状态
description: 报告受保护输出的状态
ms.assetid: 9945ae9c-1c11-4266-8a5c-d0ffe5ba4b5f
keywords:
- OPM WDK 显示受保护的状态输出
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81b6c7e0c32192f2867b2377cc7da4c0e80f2b02
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359314"
---
# <a name="reporting-status-of-a-protected-output"></a>报告受保护输出的状态


外部事件可以更改的特性应用于连接器或甚至修改类型的连接器的保护。 显示微型端口驱动程序必须报告这些事件对 OPM 应用程序时驱动程序接收到调用其[ **DxgkDdiOPMGetInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_get_information)或[ **DxgkDdiOPMGetCOPPCompatibleInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_get_copp_compatible_information)函数。 显示微型端口驱动程序必须报告以下外部事件，通过返回从指定的状态标志[ **DXGKMDT\_OPM\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_status)枚举仅在接下来调用到*DxgkDdiOPMGetInformation*或*DxgkDdiOPMGetCOPPCompatibleInformation*事件发生后：

<span id="Connection_working_properly"></span><span id="connection_working_properly"></span><span id="CONNECTION_WORKING_PROPERLY"></span>连接正常工作  
显示微型端口驱动程序在计算机和显示设备之间的连接是否正常工作，应设置 DXGKMDT\_OPM\_状态\_中的正常状态标志**ulStatusFlags**的成员[ **DXGKMDT\_OPM\_标准\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_standard_information)， [ **DXGKMDT\_OPM\_实际\_输出\_格式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_actual_output_format)， [ **DXGKMDT\_OPM\_ACP\_AND\_CGMSA\_信号**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_acp_and_cgmsa_signaling)，或[ **DXGKMDT\_OPM\_已连接\_HDCP\_设备\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_connected_hdcp_device_information)结构。

<span id="Connection_integrity"></span><span id="connection_integrity"></span><span id="CONNECTION_INTEGRITY"></span>连接完整性  
如果在计算机和显示设备会断开连接，显示微型端口驱动程序应设置 DXGKMDT\_OPM\_状态\_链接\_丢失中的状态标志**ulStatusFlags**隶属 DXGKMDT\_OPM\_标准\_信息、 DXGKMDT\_OPM\_实际\_输出\_格式、 DXGKMDT\_OPM\_ACP\_AND\_CGMSA\_信号或 DXGKMDT\_OPM\_已连接\_HDCP\_设备\_信息结构.

<span id="Connector_reconfigurations"></span><span id="connector_reconfigurations"></span><span id="CONNECTOR_RECONFIGURATIONS"></span>连接器重新配置  
如果最终用户会导致物理的连接器，若要更改的配置，显示微型端口驱动程序应设置 DXGKMDT\_OPM\_状态\_重新协商\_中的必需的状态标志**ulStatusFlags**隶属 DXGKMDT\_OPM\_标准\_信息、 DXGKMDT\_OPM\_实际\_输出\_格式，DXGKMDT\_OPM\_ACP\_AND\_CGMSA\_信号或 DXGKMDT\_OPM\_已连接\_HDCP\_设备\_信息结构。

<span id="Tampering"></span><span id="tampering"></span><span id="TAMPERING"></span>篡改  
如果发生了篡改图形适配器或适配器的显示微型端口驱动程序，显示微型端口驱动程序应设置 DXGKMDT\_OPM\_状态\_篡改\_中检测到的状态标志**ulStatusFlags** DXGKMDT 成员\_OPM\_标准\_信息、 DXGKMDT\_OPM\_实际\_输出\_格式、 DXGKMDT\_OPM\_ACP\_AND\_CGMSA\_信号或 DXGKMDT\_OPM\_已连接\_HDCP\_设备\_信息结构。

<span id="Revoked_HDCP_device"></span><span id="revoked_hdcp_device"></span><span id="REVOKED_HDCP_DEVICE"></span>已吊销的 HDCP 设备  
如果已吊销的高带宽数字内容保护 (HDCP) 设备直接或间接附加连接器，并且如果启用了 HDCP，显示微型端口驱动程序应设置 DXGKMDT\_OPM\_状态\_已撤消\_HDCP\_设备\_中的附加状态标志**ulStatusFlags** DXGKMDT 成员\_OPM\_标准\_信息或 DXGKMDT\_OPM\_实际\_输出\_格式结构。 如果未启用 HDCP，驱动程序不需要设置此状态标志。 驱动程序设置此状态值仅通过调用其[ **DxgkDdiOPMGetInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_get_information)函数来确定是否启用了 HDCP。

显示微型端口驱动程序返回一个指向 DXGKMDT\_OPM\_标准\_信息、 DXGKMDT\_OPM\_实际\_输出\_格式，DXGKMDT\_OPM\_ACP\_AND\_CGMSA\_信号或 DXGKMDT\_OPM\_已连接\_HDCP\_设备\_信息结构中**abRequestedInformation**的成员[ **DXGKMDT\_OPM\_请求\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_requested_information)结构。 指向 DXGKMDT\_OPM\_请求\_通过返回的信息*RequestedInformation*参数*DxgkDdiOPMGetInformation*或*DxgkDdiOPMGetCOPPCompatibleInformation*。

例如，考虑两个媒体播放应用程序，A 和 b。用于控制每个应用程序通过 OPM，将计算机附加到显示监视器的连接器的 HDCP 保护级别。 每个应用程序控制其自己唯一的受保护的输出。 如果有连接器变得拔出下, 一次任一应用程序将启动*DxgkDdiOPMGetInformation*或*DxgkDdiOPMGetCOPPCompatibleInformation*请求到其受保护的输出，显示微型端口驱动程序应返回 DXGKMDT\_OPM\_状态\_链接\_丢失的状态标志。

假定应用程序 A 是第一个向发起呼叫*DxgkDdiOPMGetInformation*或*DxgkDdiOPMGetCOPPCompatibleInformation*在其受保护的输出。 应用程序，然后接收 DXGKMDT\_OPM\_状态\_链接\_相应地丢失标志和行为。 如果应用程序 A 启动的后续*DxgkDdiOPMGetInformation*或*DxgkDdiOPMGetCOPPCompatibleInformation*调用，它不应在收到 DXGKMDT\_OPM\_状态\_链接\_丢失标志，除非该连接器将再次变为拔出。 当应用程序 B 启动对调用*DxgkDdiOPMGetInformation*或*DxgkDdiOPMGetCOPPCompatibleInformation*在其受保护的输出，它接收 DXGKMDT\_OPM\_状态\_链接\_相应地丢失标志和行为。 同样，应用程序 B 不应收到 DXGKMDT\_OPM\_状态\_链接\_丢失的标志再次直到连接器将再次变为拔出。

 

 





