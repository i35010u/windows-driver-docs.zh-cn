---
title: SrbProcessing 规则集 (Storport)
description: 使用这些规则验证驱动程序是否正确地处理 SRB 请求。
ms.assetid: A3BF2AA3-207F-4D74-94B0-6CA215341340
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: f82071e196be56f3230c551042c4966b31de6597
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839322"
---
# <a name="srbprocessing-rule-set-storport"></a>SrbProcessing 规则集 (Storport)


使用这些规则验证驱动程序是否正确地处理 SRB 请求。

## <a name="in-this-section"></a>本部分内容


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
<td align="left"><p>此规则验证此小型端口<strong>是否处于全双工模式。</strong> 根据 StorPort 微型端口型号构建的任何驱动程序都必须处于<strong>全双工模式。</strong> 仅应在将现有 SCSI 驱动程序移植到 StorPort 时使用<strong>半双工</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-spnowait.md" data-raw-source="[&lt;strong&gt;SpNoWait&lt;/strong&gt;](storport-spnowait.md)"><strong>SpNoWait</strong></a></p></td>
<td align="left"><p>此规则验证是否在<strong>StartIo</strong>内不执行 "等待" 或 "数据分配"。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-spreturnvalue.md" data-raw-source="[&lt;strong&gt;SpReturnValue&lt;/strong&gt;](storport-spreturnvalue.md)"><strong>SpReturnValue</strong></a></p></td>
<td align="left"><p>此规则验证驱动程序的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter" data-raw-source="[&lt;strong&gt;HwStorFindAdapter&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter)"><strong>HwStorFindAdapter</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-virtual_hw_find_adapter" data-raw-source="[&lt;strong&gt;VirtualHwStorFindAdapter&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-virtual_hw_find_adapter)"><strong>VirtualHwStorFindAdapter</strong></a>实现是否返回有效状态。 有效状态为以下状态之一： <strong>SP_RETURN_FOUND</strong>、 <strong>SP_RETURN_ERROR</strong>、 <strong>SP_RETURN_BAD_CONFIG</strong>或<strong>SP_RETURN_NOT_FOUND</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storportallocatepool.md" data-raw-source="[&lt;strong&gt;StorPortAllocatePool&lt;/strong&gt;](storportallocatepool.md)"><strong>StorPortAllocatePool</strong></a></p></td>
<td align="left"><p>此规则验证微型端口是否不能尝试对已释放的缓冲区调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportfreepool" data-raw-source="[&lt;strong&gt;StorPortFreePool&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportfreepool)"><strong>StorPortFreePool</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-storportallocatepool2.md" data-raw-source="[&lt;strong&gt;StorPortAllocatePool2&lt;/strong&gt;](storport-storportallocatepool2.md)"><strong>StorPortAllocatePool2</strong></a></p></td>
<td align="left"><p>此规则验证微型端口不能尝试对已分配的缓冲区调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportallocatepool" data-raw-source="[&lt;strong&gt;StorPortAllocatePool&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportallocatepool)"><strong>StorPortAllocatePool</strong></a> ，而无需先将其解除分配。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-storportbuildio.md" data-raw-source="[&lt;strong&gt;StorPortBuildIo&lt;/strong&gt;](storport-storportbuildio.md)"><strong>StorPortBuildIo</strong></a></p></td>
<td align="left"><p>此规则验证如果 StorPort 微型端口的<a href="storport-storportbuildio.md" data-raw-source="[&lt;strong&gt;StorPortBuildIo&lt;/strong&gt;](storport-storportbuildio.md)"><strong>StorPortBuildIo</strong></a>例程返回<strong>FALSE</strong>，则不会将相关 SRB 传递到<strong>StartIo</strong>。 （在这种情况下，微型端口驱动程序必须通过<strong>StorPortBuildIo</strong>或其他地方的<strong>RequestComplete</strong>通知类型）调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportnotification" data-raw-source="[&lt;strong&gt;StorPortNotification&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportnotification)"><strong>StorPortNotification</strong></a>来完成 SRB。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-storportcompleterequest.md" data-raw-source="[&lt;strong&gt;StorPortCompleteRequest&lt;/strong&gt;](storport-storportcompleterequest.md)"><strong>StorPortCompleteRequest</strong></a></p></td>
<td align="left"><p>此规则验证小型小型端口是否不会对<strong>StorPortCompleteRequest</strong>进行调用。 不建议使用<strong>StorPortCompleteRequest</strong> ;微型端口应改为调用具有<strong>notificationType = RequestComplete</strong>的<strong>StorPortNotification</strong> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-storportenablepassive.md" data-raw-source="[&lt;strong&gt;StorPortEnablePassive&lt;/strong&gt;](storport-storportenablepassive.md)"><strong>StorPortEnablePassive</strong></a></p></td>
<td align="left"><p>此规则验证不会从<strong>HwInitialize</strong>以外的任何 StorPort 微型端口驱动程序例程中调用<strong>StorPortEnablePassiveInitialization</strong> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-storportfindadapter.md" data-raw-source="[&lt;strong&gt;StorPortFindAdapter&lt;/strong&gt;](storport-storportfindadapter.md)"><strong>StorPortFindAdapter</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter" data-raw-source="[&lt;strong&gt;HwStorFindAdapter&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter)"><strong>HwStorFindAdapter</strong></a>例程必须在<strong>PORT_CONFIGURATION_INFORMATION</strong>结构中设置<strong>MaximumTransferLength</strong>和<strong>NumberOfPhysicalBreaks</strong>字段。 默认情况下，这两个字段的值为<strong>SP_UNINITIALIZED_VALUE</strong>。 如果在退出<strong>FindAdapter</strong>时，这些字段中的任一字段仍设置为<strong>SP_UNINITIALIZED_VALUE</strong> ，则驱动程序将无法满足规则。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-storportnotification2.md" data-raw-source="[&lt;strong&gt;StorPortNotification2&lt;/strong&gt;](storport-storportnotification2.md)"><strong>StorPortNotification2</strong></a></p></td>
<td align="left"><p>此规则验证对<strong>StorPortNotification</strong>的调用是否仅使用允许的（即记录的）通知类型。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-storportpassivefromhwinit.md" data-raw-source="[&lt;strong&gt;StorPortPassiveFromHwInit&lt;/strong&gt;](storport-storportpassivefromhwinit.md)"><strong>StorPortPassiveFromHwInit</strong></a></p></td>
<td align="left"><p>如果可以直接从 HW 适配器控件入口点调用硬件初始化入口点，则不应在 Storport 驱动程序的 HW 初始化入口点中调用<strong>StorPortEnablePassiveInitialization</strong> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-storportperfopts.md" data-raw-source="[&lt;strong&gt;StorPortPerfOpts&lt;/strong&gt;](storport-storportperfopts.md)"><strong>StorPortPerfOpts</strong></a></p></td>
<td align="left"><p>此规则验证传递到<strong>StorPortInitializePerfOpts</strong>的<strong>PerfConfigData</strong>参数是否不为 NULL。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-storportstartio.md" data-raw-source="[&lt;strong&gt;StorPortStartIo&lt;/strong&gt;](storport-storportstartio.md)"><strong>StorPortStartIo</strong></a></p></td>
<td align="left"><p>永远不能在微型端口的<strong>StartIo</strong>例程中执行等待或数据分配。 如果该驱动程序调用<strong>StorPortStallExecution</strong>或其他涉及耗时操作的函数，则该驱动程序将无法使用该规则。 由于<strong>StartIo</strong>已同步，因此这些调用通常应在<strong>BuildIo</strong>中完成。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-storporttimer.md" data-raw-source="[&lt;strong&gt;StorPortTimer&lt;/strong&gt;](storport-storporttimer.md)"><strong>StorPortTimer</strong></a></p></td>
<td align="left"><p>如果对<strong>StorPortNotification （RequestTimerCall）</strong>进行调用，则必须定义<strong>HW_TIMER</strong>例程。</p></td>
</tr>
</tbody>
</table>

 

**选择 SrbProcessing 规则集**

1.  在 Microsoft Visual Studio 中选择驱动程序项目（. .Vcxproj）。 在 "**驱动程序**" 菜单中，单击 "**启动静态驱动程序验证程序 ...** "。

2.  单击 "**规则**" 选项卡。在 "**规则集**" 下，选择**SrbProcessing**。

    若要从 Visual Studio 开发人员命令提示符窗口中选择默认规则集，请使用 **/check**选项指定**SrbProcessing。 sdv** 。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:SrbProcessing.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅[使用静态驱动程序验证器查找驱动程序中的缺陷](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)和[静态驱动程序验证程序命令（MSBuild）](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)。

 

 





