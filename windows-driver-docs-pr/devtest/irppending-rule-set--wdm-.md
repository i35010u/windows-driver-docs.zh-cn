---
title: IrpPending 规则集 (WDM)
description: 使用这些规则来验证您的驱动程序正确地等待 I/O 请求数据包 (IRP)。
ms.assetid: C4B5976B-7655-4FD1-B415-98C256873EBC
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: e50f74bd400c2ec49ea708443edf56b395694a06
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373691"
---
# <a name="irppending-rule-set-wdm"></a>IrpPending 规则集 (WDM)


使用这些规则来验证您的驱动程序正确地等待 I/O 请求数据包 (IRP)。

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
<td align="left"><p><a href="wdm-markdevicepower.md" data-raw-source="[&lt;strong&gt;MarkDevicePower&lt;/strong&gt;](wdm-markdevicepower.md)"><strong>MarkDevicePower</strong></a></p></td>
<td align="left"><p><a href="wdm-markdevicepower.md" data-raw-source="[&lt;strong&gt;MarkDevicePower&lt;/strong&gt;](wdm-markdevicepower.md)"> <strong>MarkDevicePower</strong> </a>规则指定与转到 S0 SystemPowerState IRP 的 IRP_MN_SET_POWER IRP_MJ_POWER 是挂起。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-markinginterlockedqueuedirps.md" data-raw-source="[&lt;strong&gt;MarkingInterlockedQueuedIrps&lt;/strong&gt;](wdm-markinginterlockedqueuedirps.md)"><strong>MarkingInterlockedQueuedIrps</strong></a></p></td>
<td align="left"><p><a href="wdm-markinginterlockedqueuedirps.md" data-raw-source="[&lt;strong&gt;MarkingInterlockedQueuedIrps&lt;/strong&gt;](wdm-markinginterlockedqueuedirps.md)"> <strong>MarkingInterlockedQueuedIrps</strong> </a>规则指定的驱动程序正确将 IRP 标记为挂起之前它对其进行排队以进行进一步的处理方式互锁。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-markingqueuedirps.md" data-raw-source="[&lt;strong&gt;MarkingQueuedIrps&lt;/strong&gt;](wdm-markingqueuedirps.md)"><strong>MarkingQueuedIrps</strong></a></p></td>
<td align="left"><p><a href="wdm-markingqueuedirps.md" data-raw-source="[&lt;strong&gt;MarkingQueuedIrps&lt;/strong&gt;](wdm-markingqueuedirps.md)"> <strong>MarkingQueuedIrps</strong> </a>规则指定驱动程序调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending" data-raw-source="[&lt;strong&gt;IoMarkIrpPending&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending)"> <strong>IoMarkIrpPending</strong> </a>为需要进一步处理 IRP仅在自旋锁。 此规则仅适用于该驱动程序将 IRP 添加到驱动程序管理的队列。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-markirppending.md" data-raw-source="[&lt;strong&gt;MarkIrpPending&lt;/strong&gt;](wdm-markirppending.md)"><strong>MarkIrpPending</strong></a></p></td>
<td align="left"><p><a href="wdm-markirppending.md" data-raw-source="[&lt;strong&gt;MarkIrpPending&lt;/strong&gt;](wdm-markirppending.md)"> <strong>MarkIrpPending</strong> </a>规则指定只要，驱动程序调度例程调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending" data-raw-source="[&lt;strong&gt;IoMarkIrpPending&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending)"> <strong>IoMarkIrpPending</strong></a>，驱动程序将返回STATUS_PENDING 调度例程结束时。 请参阅<a href="wdm-markirppending2.md" data-raw-source="[&lt;strong&gt;MarkIrpPending2&lt;/strong&gt;](wdm-markirppending2.md)"> <strong>MarkIrpPending2</strong> </a>免费赠送的规范。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-markirppending2.md" data-raw-source="[&lt;strong&gt;MarkIrpPending2&lt;/strong&gt;](wdm-markirppending2.md)"><strong>MarkIrpPending2</strong></a></p></td>
<td align="left"><p><a href="wdm-markirppending2.md" data-raw-source="[&lt;strong&gt;MarkIrpPending2&lt;/strong&gt;](wdm-markirppending2.md)"> <strong>MarkIrpPending2</strong> </a>规则指定调度例程返回 STATUS_PENDING，是否它已调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending" data-raw-source="[&lt;strong&gt;IoMarkIrpPending&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending)"> <strong>IoMarkIrpPending</strong> </a>或传递到较低的驱动程序 IRP。 请参阅<a href="wdm-markirppending.md" data-raw-source="[&lt;strong&gt;MarkIrpPending&lt;/strong&gt;](wdm-markirppending.md)"> <strong>MarkIrpPending</strong> </a>免费赠送的规范。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-markpower.md" data-raw-source="[&lt;strong&gt;MarkPower&lt;/strong&gt;](wdm-markpower.md)"><strong>MarkPower</strong></a></p></td>
<td align="left"><p><a href="wdm-markpower.md" data-raw-source="[&lt;strong&gt;MarkPower&lt;/strong&gt;](wdm-markpower.md)"> <strong>MarkPower</strong> </a>规则指定与为 IRP_MN_SET_POWER IRP_MJ_POWER <strong>SystemPowerState</strong> IRP 转到 S0 都会被挂起。 此规则仅适用于 FDO 和 FIDO 驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-markpowerdown.md" data-raw-source="[&lt;strong&gt;MarkPowerDown&lt;/strong&gt;](wdm-markpowerdown.md)"><strong>MarkPowerDown</strong></a></p></td>
<td align="left"><p><a href="wdm-markpowerdown.md" data-raw-source="[&lt;strong&gt;MarkPowerDown&lt;/strong&gt;](wdm-markpowerdown.md)"> <strong>MarkPowerDown</strong> </a>规则指定与为 IRP_MN_SET_POWER IRP_MJ_POWER <strong>SystemPowerState</strong> IRP 从 s0 转到 [S1...S5] 是挂起。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-markqueryrelations.md" data-raw-source="[&lt;strong&gt;MarkQueryRelations&lt;/strong&gt;](wdm-markqueryrelations.md)"><strong>MarkQueryRelations</strong></a></p></td>
<td align="left"><p><a href="wdm-markqueryrelations.md" data-raw-source="[&lt;strong&gt;MarkQueryRelations&lt;/strong&gt;](wdm-markqueryrelations.md)"> <strong>MarkQueryRelations</strong> </a>规则指定驱动程序应挂起 IRP_MN_QUERY_DEVICE_RELATIONS IRP。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-markstartdevice.md" data-raw-source="[&lt;strong&gt;MarkStartDevice&lt;/strong&gt;](wdm-markstartdevice.md)"><strong>MarkStartDevice</strong></a></p></td>
<td align="left"><p><a href="wdm-markstartdevice.md" data-raw-source="[&lt;strong&gt;MarkStartDevice&lt;/strong&gt;](wdm-markstartdevice.md)"> <strong>MarkStartDevice</strong> </a>规则指定的驱动程序等待执行了 IRP_MN_START_DEVICE IRP 正确。 此规则仅适用于 FDO 和 FIDO 驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-pendedcompletedrequest.md" data-raw-source="[&lt;strong&gt;PendedCompletedRequest&lt;/strong&gt;](wdm-pendedcompletedrequest.md)"><strong>PendedCompletedRequest</strong></a></p></td>
<td align="left"><p><a href="wdm-pendedcompletedrequest.md" data-raw-source="[&lt;strong&gt;PendedCompletedRequest&lt;/strong&gt;](wdm-pendedcompletedrequest.md)"> <strong>PendedCompletedRequest</strong> </a>规则指定的驱动程序的调度例程不返回 STATUS_PENDING 上 IRP 是否驱动程序已调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)"> <strong>IoCompleteRequest</strong> </a>上传入的 IRP。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-pendedcompletedrequest2.md" data-raw-source="[&lt;strong&gt;PendedCompletedRequest2&lt;/strong&gt;](wdm-pendedcompletedrequest2.md)"><strong>PendedCompletedRequest2</strong></a></p></td>
<td align="left"><p><a href="wdm-pendedcompletedrequest2.md" data-raw-source="[&lt;strong&gt;PendedCompletedRequest2&lt;/strong&gt;](wdm-pendedcompletedrequest2.md)"> <strong>PendedCompletedRequest2</strong> </a>规则指定在调用后等待是所需<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)"> <strong>IoCallDriver</strong> </a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver)"><strong>PoCallDriver</strong> </a>因为调度例程无法完成挂起的 IRP。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-pendedcompletedrequest3.md" data-raw-source="[&lt;strong&gt;PendedCompletedRequest3&lt;/strong&gt;](wdm-pendedcompletedrequest3.md)"><strong>PendedCompletedRequest3</strong></a></p></td>
<td align="left"><p><a href="wdm-pendedcompletedrequest3.md" data-raw-source="[&lt;strong&gt;PendedCompletedRequest3&lt;/strong&gt;](wdm-pendedcompletedrequest3.md)"> <strong>PendedCompletedRequest3</strong> </a>规则指定应通过调用完成挂起的 IRP <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)"> <strong>IoCompleteRequest</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-pendedcompletedrequestex.md" data-raw-source="[&lt;strong&gt;PendedCompletedRequestEx&lt;/strong&gt;](wdm-pendedcompletedrequestex.md)"><strong>PendedCompletedRequestEx</strong></a></p></td>
<td align="left"><p><a href="wdm-pendedcompletedrequestex.md" data-raw-source="[&lt;strong&gt;PendedCompletedRequestEx&lt;/strong&gt;](wdm-pendedcompletedrequestex.md)"> <strong>PendedCompletedRequestEx</strong> </a>规则指定驱动程序不应调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)"> <strong>IoCompleteRequest</strong> </a>挂起 IRP 的。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-startdevicewait.md" data-raw-source="[&lt;strong&gt;StartDeviceWait&lt;/strong&gt;](wdm-startdevicewait.md)"><strong>StartDeviceWait</strong></a></p></td>
<td align="left"><p><a href="wdm-startdevicewait.md" data-raw-source="[&lt;strong&gt;StartDeviceWait&lt;/strong&gt;](wdm-startdevicewait.md)"> <strong>StartDeviceWait</strong> </a>规则指定驱动程序不应调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitforsingleobject" data-raw-source="[&lt;strong&gt;KeWaitForSingleObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitforsingleobject)"> <strong>KeWaitForSingleObject</strong> </a>开始设备上下文中IRP。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-startdevicewait2.md" data-raw-source="[&lt;strong&gt;StartDeviceWait2&lt;/strong&gt;](wdm-startdevicewait2.md)"><strong>StartDeviceWait2</strong></a></p></td>
<td align="left"><p><a href="wdm-startdevicewait2.md" data-raw-source="[&lt;strong&gt;StartDeviceWait2&lt;/strong&gt;](wdm-startdevicewait2.md)"> <strong>StartDeviceWait2</strong> </a>规则指定驱动程序不应调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitforsingleobject" data-raw-source="[&lt;strong&gt;KeWaitForSingleObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitforsingleobject)"> <strong>KeWaitForSingleObject</strong> </a>开始设备上下文中IRP。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-startdevicewait3.md" data-raw-source="[&lt;strong&gt;StartDeviceWait3&lt;/strong&gt;](wdm-startdevicewait3.md)"><strong>StartDeviceWait3</strong></a></p></td>
<td align="left"><p><a href="wdm-startdevicewait3.md" data-raw-source="[&lt;strong&gt;StartDeviceWait3&lt;/strong&gt;](wdm-startdevicewait3.md)"> <strong>StartDeviceWait3</strong> </a>规则指定驱动程序不应调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitforsingleobject" data-raw-source="[&lt;strong&gt;KeWaitForSingleObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitforsingleobject)"> <strong>KeWaitForSingleObject</strong> </a>开始设备上下文中IRP。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-startdevicewait4.md" data-raw-source="[&lt;strong&gt;StartDeviceWait4&lt;/strong&gt;](wdm-startdevicewait4.md)"><strong>StartDeviceWait4</strong></a></p></td>
<td align="left"><p><a href="wdm-startdevicewait4.md" data-raw-source="[&lt;strong&gt;StartDeviceWait4&lt;/strong&gt;](wdm-startdevicewait4.md)"> <strong>StartDeviceWait4</strong> </a>规则指定驱动程序不应调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitforsingleobject" data-raw-source="[&lt;strong&gt;KeWaitForSingleObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitforsingleobject)"> <strong>KeWaitForSingleObject</strong> </a>开始设备上下文中IRP。</p></td>
</tr>
</tbody>
</table>

 

**若要选择 IrpPending 规则集**

1.  Microsoft Visual Studio 中选择您的驱动程序项目 (.vcxProj)。 从**驱动程序**菜单上，单击**启动 Static Driver Verifier...** .

2.  单击**规则**选项卡。下**规则集**，选择**IrpPending**。

    若要选择的默认规则集从 Visual Studio 开发人员命令提示符窗口，请指定**IrpPending.sdv**与 **/check**选项。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:IrpPending.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅[以找到缺陷驱动程序中使用 Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)并[Static Driver Verifier 命令 (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)。

 

 





