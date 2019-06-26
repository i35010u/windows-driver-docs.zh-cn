---
title: SrbProcessing 规则集 (Storport)
description: 使用这些规则来验证您的驱动程序正确处理 SRB 请求。
ms.assetid: A3BF2AA3-207F-4D74-94B0-6CA215341340
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7e8ae8f3f29eaa38b3cfdf817a31a214dc51496d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374401"
---
# <a name="srbprocessing-rule-set-storport"></a>SrbProcessing 规则集 (Storport)


使用这些规则来验证您的驱动程序正确处理 SRB 请求。

## <a name="in-this-section"></a>本节内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="storport-spduplex.md" data-raw-source="[&lt;strong&gt;SpDuplex&lt;/strong&gt;](storport-spduplex.md)"><strong>SpDuplex</strong></a></p></td>
<td align="left"><p>此规则将验证此微型端口是否在<strong>全双工</strong>模式。 根据 StorPort 微型端口模型构建任何驱动程序必须位于<strong>全双工</strong>模式。 <strong>半双工</strong>仅用于移植到 StorPort 现有 SCSI 驱动程序时。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-spnowait.md" data-raw-source="[&lt;strong&gt;SpNoWait&lt;/strong&gt;](storport-spnowait.md)"><strong>SpNoWait</strong></a></p></td>
<td align="left"><p>此规则验证等待或数据分配不会执行内部<strong>StartIo</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-spreturnvalue.md" data-raw-source="[&lt;strong&gt;SpReturnValue&lt;/strong&gt;](storport-spreturnvalue.md)"><strong>SpReturnValue</strong></a></p></td>
<td align="left"><p>此规则验证的驱动程序的实现<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_find_adapter" data-raw-source="[&lt;strong&gt;HwStorFindAdapter&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_find_adapter)"> <strong>HwStorFindAdapter</strong> </a>并<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-virtual_hw_find_adapter" data-raw-source="[&lt;strong&gt;VirtualHwStorFindAdapter&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-virtual_hw_find_adapter)"> <strong>VirtualHwStorFindAdapter</strong> </a>返回有效状态。 有效状态是以下值之一：<strong>SP_RETURN_FOUND</strong>， <strong>SP_RETURN_ERROR</strong>， <strong>SP_RETURN_BAD_CONFIG</strong>，或<strong>SP_RETURN_NOT_FOUND</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storportallocatepool.md" data-raw-source="[&lt;strong&gt;StorPortAllocatePool&lt;/strong&gt;](storportallocatepool.md)"><strong>StorPortAllocatePool</strong></a></p></td>
<td align="left"><p>此规则验证微型端口必须尝试调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportfreepool" data-raw-source="[&lt;strong&gt;StorPortFreePool&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportfreepool)"> <strong>StorPortFreePool</strong> </a>已解除分配的缓冲区。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-storportallocatepool2.md" data-raw-source="[&lt;strong&gt;StorPortAllocatePool2&lt;/strong&gt;](storport-storportallocatepool2.md)"><strong>StorPortAllocatePool2</strong></a></p></td>
<td align="left"><p>此规则验证微型端口必须尝试调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportallocatepool" data-raw-source="[&lt;strong&gt;StorPortAllocatePool&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportallocatepool)"> <strong>StorPortAllocatePool</strong> </a>上而不首先释放的分配的缓冲区。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-storportbuildio.md" data-raw-source="[&lt;strong&gt;StorPortBuildIo&lt;/strong&gt;](storport-storportbuildio.md)"><strong>StorPortBuildIo</strong></a></p></td>
<td align="left"><p>此规则验证，如果 StorPort 微型端口<a href="storport-storportbuildio.md" data-raw-source="[&lt;strong&gt;StorPortBuildIo&lt;/strong&gt;](storport-storportbuildio.md)"> <strong>StorPortBuildIo</strong> </a>例程返回<strong>FALSE</strong>，相关 SRB 未传递给<strong>StartIo</strong>. (在这种情况下，微型端口驱动程序必须通过调用完成 SRB <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportnotification" data-raw-source="[&lt;strong&gt;StorPortNotification&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportnotification)"> <strong>StorPortNotification</strong> </a>通知类型为<strong>RequestComplete</strong>从<strong>StorPortBuildIo</strong>或其他某个)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-storportcompleterequest.md" data-raw-source="[&lt;strong&gt;StorPortCompleteRequest&lt;/strong&gt;](storport-storportcompleterequest.md)"><strong>StorPortCompleteRequest</strong></a></p></td>
<td align="left"><p>此规则验证未调用<strong>StorPortCompleteRequest</strong>由微型端口。 使用情况<strong>StorPortCompleteRequest</strong>不建议使用; 微型端口应改为调用<strong>StorPortNotification</strong>与<strong>notificationType = RequestComplete</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-storportenablepassive.md" data-raw-source="[&lt;strong&gt;StorPortEnablePassive&lt;/strong&gt;](storport-storportenablepassive.md)"><strong>StorPortEnablePassive</strong></a></p></td>
<td align="left"><p>此规则验证<strong>StorPortEnablePassiveInitialization</strong>不从调用任何 StorPort 微型端口驱动程序例程以外<strong>HwInitialize</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-storportfindadapter.md" data-raw-source="[&lt;strong&gt;StorPortFindAdapter&lt;/strong&gt;](storport-storportfindadapter.md)"><strong>StorPortFindAdapter</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_find_adapter" data-raw-source="[&lt;strong&gt;HwStorFindAdapter&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_find_adapter)"> <strong>HwStorFindAdapter</strong> </a>例程必须设置<strong>MaximumTransferLength</strong>并<strong>NumberOfPhysicalBreaks</strong> 中的字段<strong>PORT_CONFIGURATION_INFORMATION</strong>结构。 默认情况下，这两个这些字段的值是<strong>SP_UNINITIALIZED_VALUE</strong>。 如果这些字段之一仍设置为<strong>SP_UNINITIALIZED_VALUE</strong>在从退出时<strong>FindAdapter</strong>，驱动程序失败的规则。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-storportnotification2.md" data-raw-source="[&lt;strong&gt;StorPortNotification2&lt;/strong&gt;](storport-storportnotification2.md)"><strong>StorPortNotification2</strong></a></p></td>
<td align="left"><p>此规则验证的调用<strong>StorPortNotification</strong>只允许使用 （即记录） 的通知类型。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-storportpassivefromhwinit.md" data-raw-source="[&lt;strong&gt;StorPortPassiveFromHwInit&lt;/strong&gt;](storport-storportpassivefromhwinit.md)"><strong>StorPortPassiveFromHwInit</strong></a></p></td>
<td align="left"><p><strong>StorPortEnablePassiveInitialization</strong>不应调用内 HW 初始化入口点的 Storport 驱动程序如果可以直接从硬件适配器可以控制入口点调用 HW 初始化入口点。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-storportperfopts.md" data-raw-source="[&lt;strong&gt;StorPortPerfOpts&lt;/strong&gt;](storport-storportperfopts.md)"><strong>StorPortPerfOpts</strong></a></p></td>
<td align="left"><p>此规则验证<strong>PerfConfigData</strong>参数传递给<strong>StorPortInitializePerfOpts</strong>不为 NULL。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-storportstartio.md" data-raw-source="[&lt;strong&gt;StorPortStartIo&lt;/strong&gt;](storport-storportstartio.md)"><strong>StorPortStartIo</strong></a></p></td>
<td align="left"><p>中的微型端口必须永远不会执行等待或数据分配<strong>StartIo</strong>例程。 该驱动程序失败规则，如果它调用<strong>StorPortStallExecution</strong>或涉及耗时的操作的另一个函数。 由于<strong>StartIo</strong>是同步的这些调用通常应该以<strong>BuildIo</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-storporttimer.md" data-raw-source="[&lt;strong&gt;StorPortTimer&lt;/strong&gt;](storport-storporttimer.md)"><strong>StorPortTimer</strong></a></p></td>
<td align="left"><p><strong>HW_TIMER</strong>如果调用，必须定义例程<strong>StorPortNotification(RequestTimerCall)</strong>进行。</p></td>
</tr>
</tbody>
</table>

 

**若要选择 SrbProcessing 规则集**

1.  Microsoft Visual Studio 中选择您的驱动程序项目 (.vcxProj)。 从**驱动程序**菜单上，单击**启动 Static Driver Verifier...** .

2.  单击**规则**选项卡。下**规则集**，选择**SrbProcessing**。

    若要选择的默认规则集从 Visual Studio 开发人员命令提示符窗口，请指定**SrbProcessing.sdv**与 **/check**选项。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:SrbProcessing.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅[以找到缺陷驱动程序中使用 Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)并[Static Driver Verifier 命令 (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)。

 

 





