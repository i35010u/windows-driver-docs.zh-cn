---
title: COPP 的示例函数
description: COPP 的示例函数
ms.assetid: 73c9cf1c-c20d-456c-8029-5316fd8979d5
keywords:
- 复制保护 WDK COPP，示例函数
- 视频复制保护 WDK COPP，示例函数
- COPP WDK DirectX VA，示例函数
- 受保护的视频 WDK COPP，示例函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7012aff2be4e39eef55a2e14776aaa51ebbdac14
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066348"
---
# <a name="sample-functions-for-copp"></a>COPP 的示例函数


## <span id="ddk_sample_functions_for_copp_gg"></span><span id="DDK_SAMPLE_FUNCTIONS_FOR_COPP_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。**

示例 COPP 函数演示如何实现 COPP 处理功能。 这些示例函数映射到[**DD \_ MOTIONCOMPCALLBACKS**](/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)结构中定义的[运动补偿回调函数](motion-compensation-callbacks.md)。 可以 (IOCTL) 请求实现每个示例函数和相应的 COPP i/o 控制，然后使用运动补偿代码模板和视频微型端口驱动程序模板来完成实现。 有关详细信息，请参阅 [DIRECTX VA 设备的示例代码](example-code-for-directx-va-devices.md)。

### <a name="span-idcopp_sample_functionsspanspan-idcopp_sample_functionsspanspan-idcopp_sample_functionsspancopp-sample-functions"></a><span id="COPP_Sample_Functions"></span><span id="copp_sample_functions"></span><span id="COPP_SAMPLE_FUNCTIONS"></span>COPP 示例函数

下表中的示例 COPP 函数是使用 COPP 设备调用的。 有关 COPP 设备的详细信息，请参阅 [COPP 设备定义模板代码](copp-device-definition-template-code.md) 和 [定义 COPP 设备类](defining-the-copp-device-class.md)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">成员函数</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/coppopenvideosession" data-raw-source="[&lt;em&gt;COPPOpenVideoSession&lt;/em&gt;](./coppopenvideosession.md)"><em>COPPOpenVideoSession</em></a></p></td>
<td align="left"><p>初始化用于当前视频会话的 COPP 设备。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/coppgetcertificatelength" data-raw-source="[&lt;em&gt;COPPGetCertificateLength&lt;/em&gt;](./coppgetcertificatelength.md)"><em>COPPGetCertificateLength</em></a></p></td>
<td align="left"><p>检索图形硬件使用的证书的大小（以字节为单位）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/coppkeyexchange" data-raw-source="[&lt;em&gt;COPPKeyExchange&lt;/em&gt;](./coppkeyexchange.md)"><em>COPPKeyExchange</em></a></p></td>
<td align="left"><p>检索图形硬件使用的数字证书。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/coppsequencestart" data-raw-source="[&lt;em&gt;COPPSequenceStart&lt;/em&gt;](./coppsequencestart.md)"><em>COPPSequenceStart</em></a></p></td>
<td align="left"><p>将当前视频会话设置为受保护模式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/coppcommand" data-raw-source="[&lt;em&gt;COPPCommand&lt;/em&gt;](./coppcommand.md)"><em>COPPCommand</em></a></p></td>
<td align="left"><p>设置与 COPP 设备关联的物理连接器的保护级别。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/coppquerystatus" data-raw-source="[&lt;em&gt;COPPQueryStatus&lt;/em&gt;](./coppquerystatus.md)"><em>COPPQueryStatus</em></a></p></td>
<td align="left"><p>检索与 COPP 设备关联的受保护视频会话的状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/coppclosevideosession" data-raw-source="[&lt;em&gt;COPPCloseVideoSession&lt;/em&gt;](./coppclosevideosession.md)"><em>COPPCloseVideoSession</em></a></p></td>
<td align="left"><p>关闭 COPP 设备对象，并指示驱动程序释放与 COPP 设备关联的硬件资源。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idmapping_sample_functions_to_dd_motioncompcallbacksspanspan-idmapping_sample_functions_to_dd_motioncompcallbacksspanspan-idmapping_sample_functions_to_dd_motioncompcallbacksspanmapping-sample-functions-to-dd_motioncompcallbacks"></a><span id="Mapping_Sample_Functions_to_DD_MOTIONCOMPCALLBACKS"></span><span id="mapping_sample_functions_to_dd_motioncompcallbacks"></span><span id="MAPPING_SAMPLE_FUNCTIONS_TO_DD_MOTIONCOMPCALLBACKS"></span>将示例函数映射到 DD \_ MOTIONCOMPCALLBACKS

本节中的示例函数通过使用 COPP IOCTL 映射到运动补偿回调函数，如下所示：也就是说，每个示例函数都在其各自的 COPP IOCTL 内调用，每个 COPP IOCTL 都将传递到其各自的运动补偿回调函数中的 [**EngDeviceIoControl**](/windows/desktop/api/winddi/nf-winddi-engdeviceiocontrol) 函数。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数</th>
<th align="left">IOCTL</th>
<th align="left">DD_MOTIONCOMPCALLBACKS 成员</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/coppopenvideosession" data-raw-source="[&lt;em&gt;COPPOpenVideoSession&lt;/em&gt;](./coppopenvideosession.md)"><em>COPPOpenVideoSession</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/" data-raw-source="[&lt;strong&gt;IOCTL_COPP_OpenDevice&lt;/strong&gt;](./index.md)"><strong>IOCTL_COPP_OpenDevice</strong></a></p></td>
<td align="left"><p><strong>CreateMoComp</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/coppgetcertificatelength" data-raw-source="[&lt;em&gt;COPPGetCertificateLength&lt;/em&gt;](./coppgetcertificatelength.md)"><em>COPPGetCertificateLength</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/ioctl-copp-getcertificatelength" data-raw-source="[&lt;strong&gt;IOCTL_COPP_GetCertificateLength&lt;/strong&gt;](./ioctl-copp-getcertificatelength.md)"><strong>IOCTL_COPP_GetCertificateLength</strong></a></p></td>
<td align="left"><p><strong>RenderMoComp</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/coppkeyexchange" data-raw-source="[&lt;em&gt;COPPKeyExchange&lt;/em&gt;](./coppkeyexchange.md)"><em>COPPKeyExchange</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/ioctl-copp-keyexchange" data-raw-source="[&lt;strong&gt;IOCTL_COPP_KeyExchange&lt;/strong&gt;](./ioctl-copp-keyexchange.md)"><strong>IOCTL_COPP_KeyExchange</strong></a></p></td>
<td align="left"><p><strong>RenderMoComp</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/coppsequencestart" data-raw-source="[&lt;em&gt;COPPSequenceStart&lt;/em&gt;](./coppsequencestart.md)"><em>COPPSequenceStart</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/ioctl-copp-startsequence" data-raw-source="[&lt;strong&gt;IOCTL_COPP_StartSequence&lt;/strong&gt;](./ioctl-copp-startsequence.md)"><strong>IOCTL_COPP_StartSequence</strong></a></p></td>
<td align="left"><p><strong>RenderMoComp</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/coppcommand" data-raw-source="[&lt;em&gt;COPPCommand&lt;/em&gt;](./coppcommand.md)"><em>COPPCommand</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/ioctl-copp-command" data-raw-source="[&lt;strong&gt;IOCTL_COPP_Command&lt;/strong&gt;](./ioctl-copp-command.md)"><strong>IOCTL_COPP_Command</strong></a></p></td>
<td align="left"><p><strong>RenderMoComp</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/coppquerystatus" data-raw-source="[&lt;em&gt;COPPQueryStatus&lt;/em&gt;](./coppquerystatus.md)"><em>COPPQueryStatus</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/ioctl-copp-status" data-raw-source="[&lt;strong&gt;IOCTL_COPP_Status&lt;/strong&gt;](./ioctl-copp-status.md)"><strong>IOCTL_COPP_Status</strong></a></p></td>
<td align="left"><p><strong>RenderMoComp</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/coppclosevideosession" data-raw-source="[&lt;em&gt;COPPCloseVideoSession&lt;/em&gt;](./coppclosevideosession.md)"><em>COPPCloseVideoSession</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/" data-raw-source="[&lt;strong&gt;IOCTL_COPP_CloseDevice&lt;/strong&gt;](./index.md)"><strong>IOCTL_COPP_CloseDevice</strong></a></p></td>
<td align="left"><p><strong>DestroyMoComp</strong></p></td>
</tr>
</tbody>
</table>

 

 

