---
title: COPP 的示例函数
description: COPP 的示例函数
ms.assetid: 73c9cf1c-c20d-456c-8029-5316fd8979d5
keywords:
- 复制保护 WDK COPP，示例函数
- 视频复制保护 WDK COPP，示例函数
- COPP WDK DirectX va，因此示例函数
- 受保护视频 WDK COPP，示例函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2b1d92c1c18c7adb0c7742c8d6e540f7971136e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365616"
---
# <a name="sample-functions-for-copp"></a>COPP 的示例函数


## <span id="ddk_sample_functions_for_copp_gg"></span><span id="DDK_SAMPLE_FUNCTIONS_FOR_COPP_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 和更高版本，和 Windows XP SP2 及更高版本。**

示例 COPP 函数演示如何实现 COPP 处理功能。 这些示例函数将映射到[动作补偿回调函数](motion-compensation-callbacks.md)中定义[ **DD\_MOTIONCOMPCALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)结构。 您可以实现每个示例函数和相应的 COPP I/O 控制 (IOCTL) 请求，然后使用运动补偿代码模板和视频的微型端口驱动程序模板以完成实现。 有关详细信息，请参阅[DirectX VA 设备的示例代码](example-code-for-directx-va-devices.md)。

### <a name="span-idcoppsamplefunctionsspanspan-idcoppsamplefunctionsspanspan-idcoppsamplefunctionsspancopp-sample-functions"></a><span id="COPP_Sample_Functions"></span><span id="copp_sample_functions"></span><span id="COPP_SAMPLE_FUNCTIONS"></span>COPP 示例函数

下表中的示例 COPP 函数调用使用 COPP 设备。 有关 COPP 设备的详细信息，请参阅[COPP 设备定义模板代码](copp-device-definition-template-code.md)并[定义 COPP 设备类](defining-the-copp-device-class.md)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">成员函数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/coppopenvideosession" data-raw-source="[&lt;em&gt;COPPOpenVideoSession&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/coppopenvideosession)"><em>COPPOpenVideoSession</em></a></p></td>
<td align="left"><p>初始化当前的视频会话使用的 COPP 设备。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/coppgetcertificatelength" data-raw-source="[&lt;em&gt;COPPGetCertificateLength&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/coppgetcertificatelength)"><em>COPPGetCertificateLength</em></a></p></td>
<td align="left"><p>检索大小 （字节） 使用图形硬件的证书。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/coppkeyexchange" data-raw-source="[&lt;em&gt;COPPKeyExchange&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/coppkeyexchange)"><em>COPPKeyExchange</em></a></p></td>
<td align="left"><p>检索用于图形硬件的数字证书。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/coppsequencestart" data-raw-source="[&lt;em&gt;COPPSequenceStart&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/coppsequencestart)"><em>COPPSequenceStart</em></a></p></td>
<td align="left"><p>将当前的视频会话设置为受保护模式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/coppcommand" data-raw-source="[&lt;em&gt;COPPCommand&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/coppcommand)"><em>COPPCommand</em></a></p></td>
<td align="left"><p>与 COPP 设备相关联的物理连接器上设置的保护级别。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/coppquerystatus" data-raw-source="[&lt;em&gt;COPPQueryStatus&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/coppquerystatus)"><em>COPPQueryStatus</em></a></p></td>
<td align="left"><p>检索与 COPP 设备相关联的受保护视频会话状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/coppclosevideosession" data-raw-source="[&lt;em&gt;COPPCloseVideoSession&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/coppclosevideosession)"><em>COPPCloseVideoSession</em></a></p></td>
<td align="left"><p>关闭 COPP 设备对象，并指示驱动程序来释放与 COPP 设备相关联的硬件资源。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idmappingsamplefunctionstoddmotioncompcallbacksspanspan-idmappingsamplefunctionstoddmotioncompcallbacksspanspan-idmappingsamplefunctionstoddmotioncompcallbacksspanmapping-sample-functions-to-ddmotioncompcallbacks"></a><span id="Mapping_Sample_Functions_to_DD_MOTIONCOMPCALLBACKS"></span><span id="mapping_sample_functions_to_dd_motioncompcallbacks"></span><span id="MAPPING_SAMPLE_FUNCTIONS_TO_DD_MOTIONCOMPCALLBACKS"></span>示例函数映射到 DD\_MOTIONCOMPCALLBACKS

到运动补偿回调函数，如下所示; 使用 COPP IOCTL，此部分映射中的示例函数这就是说，每个示例函数调用中其各自的 COPP IOCTL，而每个 COPP IOCTL 传递给[ **EngDeviceIoControl** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeviceiocontrol)中其各自的运动补偿回调函数函数。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/coppopenvideosession" data-raw-source="[&lt;em&gt;COPPOpenVideoSession&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/coppopenvideosession)"><em>COPPOpenVideoSession</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/" data-raw-source="[&lt;strong&gt;IOCTL_COPP_OpenDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/)"><strong>IOCTL_COPP_OpenDevice</strong></a></p></td>
<td align="left"><p><strong>CreateMoComp</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/coppgetcertificatelength" data-raw-source="[&lt;em&gt;COPPGetCertificateLength&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/coppgetcertificatelength)"><em>COPPGetCertificateLength</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/ioctl-copp-getcertificatelength" data-raw-source="[&lt;strong&gt;IOCTL_COPP_GetCertificateLength&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/ioctl-copp-getcertificatelength)"><strong>IOCTL_COPP_GetCertificateLength</strong></a></p></td>
<td align="left"><p><strong>RenderMoComp</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/coppkeyexchange" data-raw-source="[&lt;em&gt;COPPKeyExchange&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/coppkeyexchange)"><em>COPPKeyExchange</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/ioctl-copp-keyexchange" data-raw-source="[&lt;strong&gt;IOCTL_COPP_KeyExchange&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/ioctl-copp-keyexchange)"><strong>IOCTL_COPP_KeyExchange</strong></a></p></td>
<td align="left"><p><strong>RenderMoComp</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/coppsequencestart" data-raw-source="[&lt;em&gt;COPPSequenceStart&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/coppsequencestart)"><em>COPPSequenceStart</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/ioctl-copp-startsequence" data-raw-source="[&lt;strong&gt;IOCTL_COPP_StartSequence&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/ioctl-copp-startsequence)"><strong>IOCTL_COPP_StartSequence</strong></a></p></td>
<td align="left"><p><strong>RenderMoComp</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/coppcommand" data-raw-source="[&lt;em&gt;COPPCommand&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/coppcommand)"><em>COPPCommand</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/ioctl-copp-command" data-raw-source="[&lt;strong&gt;IOCTL_COPP_Command&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/ioctl-copp-command)"><strong>IOCTL_COPP_Command</strong></a></p></td>
<td align="left"><p><strong>RenderMoComp</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/coppquerystatus" data-raw-source="[&lt;em&gt;COPPQueryStatus&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/coppquerystatus)"><em>COPPQueryStatus</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/ioctl-copp-status" data-raw-source="[&lt;strong&gt;IOCTL_COPP_Status&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/ioctl-copp-status)"><strong>IOCTL_COPP_Status</strong></a></p></td>
<td align="left"><p><strong>RenderMoComp</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/coppclosevideosession" data-raw-source="[&lt;em&gt;COPPCloseVideoSession&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/coppclosevideosession)"><em>COPPCloseVideoSession</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/" data-raw-source="[&lt;strong&gt;IOCTL_COPP_CloseDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/)"><strong>IOCTL_COPP_CloseDevice</strong></a></p></td>
<td align="left"><p><strong>DestroyMoComp</strong></p></td>
</tr>
</tbody>
</table>

 

 

 





