---
title: 报告受保护输出的状态
description: 报告受保护输出的状态
ms.assetid: 9945ae9c-1c11-4266-8a5c-d0ffe5ba4b5f
keywords:
- OPM WDK 显示，受保护的输出状态
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 086cb6cea9cd1f1447cc2c6d17735f3ff588f728
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067268"
---
# <a name="reporting-status-of-a-protected-output"></a>报告受保护输出的状态


外部事件可以更改应用于连接器的保护性质，甚至可以修改连接器的类型。 当驱动程序收到对其 [**DxgkDdiOPMGetInformation**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_information) 或 [**DxgkDdiOPMGetCOPPCompatibleInformation**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_copp_compatible_information) 函数的调用时，显示微型端口驱动程序必须将这些事件报告给 OPM 应用程序。 显示微型端口驱动程序必须在事件发生后，通过仅在下一次调用*DxgkDdiOPMGetInformation*或*DxgkDdiOPMGetCOPPCompatibleInformation*时从[**DXGKMDT \_ OPM \_ 状态**](/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_status)枚举返回指定的状态标志，来报告以下外部事件：

<span id="Connection_working_properly"></span><span id="connection_working_properly"></span><span id="CONNECTION_WORKING_PROPERLY"></span>连接工作正常  
如果计算机与显示设备之间的连接工作正常，则显示微型端口驱动程序应 \_ \_ \_ 在[**DXGKMDT \_ OPM \_ 标准 \_ 信息**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_standard_information)的**ulStatusFlags**成员中设置 DXGKMDT OPM 状态正常状态标志， [**DXGKMDT OPM \_ \_ 实际 \_ 输出 \_ 格式**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_actual_output_format)、 [**DXGKMDT \_ OPM \_ ACP \_ 和 CGMSA 发出 \_ \_ 信号**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_acp_and_cgmsa_signaling)，或[**DXGKMDT \_ OPM \_ 连接 \_ HDCP \_ 设备 \_ 信息**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_connected_hdcp_device_information)结构。

<span id="Connection_integrity"></span><span id="connection_integrity"></span><span id="CONNECTION_INTEGRITY"></span>连接完整性  
如果计算机和显示设备断开连接，则显示微型端口驱动程序应 \_ \_ \_ \_ 在 DXGKMDT OPM 标准信息的 **ulStatusFlags** 成员中设置 DXGKMDT OPM 状态链接丢失状态标志， \_ \_ \_ DXGKMDT \_ OPM \_ 实际 \_ 输出 \_ 格式、DXGKMDT \_ OPM \_ ACP \_ 和 CGMSA 发出 \_ \_ 信号，或 DXGKMDT \_ OPM \_ 连接 \_ HDCP \_ 设备 \_ 信息结构。

<span id="Connector_reconfigurations"></span><span id="connector_reconfigurations"></span><span id="CONNECTOR_RECONFIGURATIONS"></span>连接器重新连接  
如果最终用户导致物理连接器的配置发生更改，则显示微型端口驱动程序应 \_ \_ \_ \_ 在 DXGKMDT OPM 标准信息的 **ulStatusFlags** 成员中设置 DXGKMDT OPM 状态重新协商要求的状态标志， \_ DXGKMDT OPM \_ \_ \_ \_ 实际 \_ 输出 \_ 格式、DXGKMDT \_ OPM \_ ACP \_ 和 \_ CGMSA \_ 信号，或 DXGKMDT \_ OPM \_ 连接 \_ HDCP \_ 设备 \_ 信息结构。

<span id="Tampering"></span><span id="tampering"></span><span id="TAMPERING"></span>篡改  
如果出现篡改图形适配器或适配器的显示微型端口驱动程序的情况，则显示微型端口驱动程序应 \_ \_ \_ \_ 在 DXGKMDT OPM 标准信息的 **ulStatusFlags** 成员中设置 DXGKMDT OPM 状态篡改检测状态标志，DXGKMDT OPM \_ \_ \_ \_ \_ 实际 \_ 输出 \_ 格式、DXGKMDT \_ OPM \_ ACP \_ 和 \_ CGMSA 发出 \_ 信号，或 DXGKMDT \_ OPM \_ 连接 \_ HDCP \_ 设备 \_ 信息结构。

<span id="Revoked_HDCP_device"></span><span id="revoked_hdcp_device"></span><span id="REVOKED_HDCP_DEVICE"></span>已吊销 HDCP 设备  
如果已吊销的高带宽数字内容保护 (HDCP) 设备直接或间接连接到连接器，且已启用 HDCP，则显示微型端口驱动程序应 \_ \_ \_ \_ \_ \_ 在**ulStatusFlags** DXGKMDT \_ OPM \_ STANDARD \_ INFORMATION 或 DXGKMDT \_ OPM \_ 实际 \_ 输出 \_ 格式结构的 ulStatusFlags 成员中设置 DXGKMDT OPM 状态 "已吊销 HDCP 设备附加状态" 标志。 如果未启用 HDCP，则无需驱动程序设置此状态标志。 驱动程序仅通过对其 [**DxgkDdiOPMGetInformation**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_information) 函数的调用来设置此状态值，以确定是否已启用 HDCP。

显示微型端口驱动程序返回一个指针，该指针指向 DXGKMDT \_ OPM \_ STANDARD \_ 信息、DXGKMDT \_ OPM \_ 实际 \_ 输出 \_ 格式、DXGKMDT \_ OPM \_ ACP \_ 和 \_ CGMSA \_ 信号，或 DXGKMDT OPM \_ 请求的 \_ \_ 信息结构的 abRequestedInformation 成员中的 DXGKMDT OPM 连接 HDCP \_ 设备 \_ 信息结构。 [** \_ \_ \_ **](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_requested_information) **abRequestedInformation** 指向 DXGKMDT \_ OPM 请求信息的指针将 \_ \_ 通过*DxgkDdiOPMGetInformation*或*DxgkDdiOPMGetCOPPCompatibleInformation*的*RequestedInformation*参数返回。

例如，请考虑两个媒体播放应用程序： A 和 B。每个应用程序通过 OPM，将计算机连接到显示监视器的连接器的 HDCP 保护级别进行控制。 每个应用程序都控制其自己的唯一受保护的输出。 如果连接器已拔出，则下一次应用程序启动 *DxgkDdiOPMGetInformation* 或 *DxgkDdiOPMGetCOPPCompatibleInformation* 对其受保护的输出的请求时，显示微型端口驱动程序应返回 DXGKMDT \_ OPM \_ 状态 \_ 链接 \_ 丢失状态标志。

假设应用程序 A 是在其受保护的输出中启动对 *DxgkDdiOPMGetInformation* 或 *DxgkDdiOPMGetCOPPCompatibleInformation* 的调用。 然后，应用程序 A 会接收到 DXGKMDT \_ OPM \_ 状态 \_ 链接 \_ 丢失标志，并相应地采取措施。 如果应用程序 A 启动后续的 *DxgkDdiOPMGetInformation* 或 *DxgkDdiOPMGetCOPPCompatibleInformation* 调用，则它不应收到 DXGKMDT \_ OPM \_ 状态 \_ 链接 \_ 丢失标志，除非连接器再次被拔出。 当应用程序 B 对其受保护的输出启动对 *DxgkDdiOPMGetInformation* 或 *DxgkDdiOPMGetCOPPCompatibleInformation* 的调用时，它会收到 DXGKMDT \_ OPM \_ 状态 \_ 链接 \_ 丢失标志，并相应地进行操作。 同样，应用程序 B 不应再次收到 DXGKMDT \_ OPM \_ 状态 \_ 链接 \_ 丢失标志，直到连接器再次被拔出。

 

