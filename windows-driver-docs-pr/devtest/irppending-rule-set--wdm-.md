---
title: IrpPending 规则集 (WDM)
description: 使用这些规则验证驱动程序是否正确 pends i/o 请求数据包 (IRP) 。
ms.assetid: C4B5976B-7655-4FD1-B415-98C256873EBC
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: d7f2ecbe66ddd72032cbd8ea5792509caa3fd247
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103518"
---
# <a name="irppending-rule-set-wdm"></a>IrpPending 规则集 (WDM)


使用这些规则验证驱动程序是否正确 pends i/o 请求数据包 (IRP) 。

## <a name="in-this-section"></a>在本节中


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="wdm-markdevicepower.md" data-raw-source="[&lt;strong&gt;MarkDevicePower&lt;/strong&gt;](wdm-markdevicepower.md)"><strong>MarkDevicePower</strong></a></p></td>
<td align="left"><p><a href="wdm-markdevicepower.md" data-raw-source="[&lt;strong&gt;MarkDevicePower&lt;/strong&gt;](wdm-markdevicepower.md)"><strong>MarkDevicePower</strong></a>规则指定将 IRP_MN_SET_POWER 用于 SystemPowerState IRP 的 IRP_MJ_POWER 挂起。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-markinginterlockedqueuedirps.md" data-raw-source="[&lt;strong&gt;MarkingInterlockedQueuedIrps&lt;/strong&gt;](wdm-markinginterlockedqueuedirps.md)"><strong>MarkingInterlockedQueuedIrps</strong></a></p></td>
<td align="left"><p><a href="wdm-markinginterlockedqueuedirps.md" data-raw-source="[&lt;strong&gt;MarkingInterlockedQueuedIrps&lt;/strong&gt;](wdm-markinginterlockedqueuedirps.md)"><strong>MarkingInterlockedQueuedIrps</strong></a>规则指定，驱动程序将 IRP 正确地标记为 "挂起"，然后将其以联锁方式排队以进行进一步处理。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-markingqueuedirps.md" data-raw-source="[&lt;strong&gt;MarkingQueuedIrps&lt;/strong&gt;](wdm-markingqueuedirps.md)"><strong>MarkingQueuedIrps</strong></a></p></td>
<td align="left"><p><a href="wdm-markingqueuedirps.md" data-raw-source="[&lt;strong&gt;MarkingQueuedIrps&lt;/strong&gt;](wdm-markingqueuedirps.md)"><strong>MarkingQueuedIrps</strong></a>规则指定，驱动程序为 IRP 调用<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending" data-raw-source="[&lt;strong&gt;IoMarkIrpPending&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)"><strong>也</strong></a>，该 IRP 需要在持有自旋锁的情况下进行进一步处理。 仅当驱动程序将 IRP 添加到驱动程序管理的队列时，此规则才适用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-markirppending.md" data-raw-source="[&lt;strong&gt;MarkIrpPending&lt;/strong&gt;](wdm-markirppending.md)"><strong>MarkIrpPending</strong></a></p></td>
<td align="left"><p><a href="wdm-markirppending.md" data-raw-source="[&lt;strong&gt;MarkIrpPending&lt;/strong&gt;](wdm-markirppending.md)"><strong>MarkIrpPending</strong></a>规则指定每当驱动程序调度例程调用<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending" data-raw-source="[&lt;strong&gt;IoMarkIrpPending&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)"><strong>也</strong></a>时，驱动程序将在调度例程结束时返回 STATUS_PENDING。 有关免费规范，请参阅 <a href="wdm-markirppending2.md" data-raw-source="[&lt;strong&gt;MarkIrpPending2&lt;/strong&gt;](wdm-markirppending2.md)"><strong>MarkIrpPending2</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-markirppending2.md" data-raw-source="[&lt;strong&gt;MarkIrpPending2&lt;/strong&gt;](wdm-markirppending2.md)"><strong>MarkIrpPending2</strong></a></p></td>
<td align="left"><p><a href="wdm-markirppending2.md" data-raw-source="[&lt;strong&gt;MarkIrpPending2&lt;/strong&gt;](wdm-markirppending2.md)"><strong>MarkIrpPending2</strong></a>规则指定如果派单例程返回 STATUS_PENDING，它将调用<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending" data-raw-source="[&lt;strong&gt;IoMarkIrpPending&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)"><strong>也</strong></a>或将 IRP 传递到较低的驱动程序。 有关免费规范，请参阅 <a href="wdm-markirppending.md" data-raw-source="[&lt;strong&gt;MarkIrpPending&lt;/strong&gt;](wdm-markirppending.md)"><strong>MarkIrpPending</strong></a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-markpower.md" data-raw-source="[&lt;strong&gt;MarkPower&lt;/strong&gt;](wdm-markpower.md)"><strong>MarkPower</strong></a></p></td>
<td align="left"><p><a href="wdm-markpower.md" data-raw-source="[&lt;strong&gt;MarkPower&lt;/strong&gt;](wdm-markpower.md)"><strong>MarkPower</strong></a>规则指定将 IRP_MN_SET_POWER 用于<strong>SystemPowerState</strong> IRP 的 IRP_MJ_POWER 挂起。 此规则仅适用于 FDO 和 FIDO 驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-markpowerdown.md" data-raw-source="[&lt;strong&gt;MarkPowerDown&lt;/strong&gt;](wdm-markpowerdown.md)"><strong>MarkPowerDown</strong></a></p></td>
<td align="left"><p><a href="wdm-markpowerdown.md" data-raw-source="[&lt;strong&gt;MarkPowerDown&lt;/strong&gt;](wdm-markpowerdown.md)"><strong>MarkPowerDown</strong></a>规则指定具有<strong>SystemPowerState</strong> IRP 的 IRP_MN_SET_POWER 的 IRP_MJ_POWER 从 S0 转到 [S1 .。。S5] 已挂起。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-markqueryrelations.md" data-raw-source="[&lt;strong&gt;MarkQueryRelations&lt;/strong&gt;](wdm-markqueryrelations.md)"><strong>MarkQueryRelations</strong></a></p></td>
<td align="left"><p><a href="wdm-markqueryrelations.md" data-raw-source="[&lt;strong&gt;MarkQueryRelations&lt;/strong&gt;](wdm-markqueryrelations.md)"><strong>MarkQueryRelations</strong></a>规则指定驱动程序应挂起 IRP_MN_QUERY_DEVICE_RELATIONS IRP。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-markstartdevice.md" data-raw-source="[&lt;strong&gt;MarkStartDevice&lt;/strong&gt;](wdm-markstartdevice.md)"><strong>MarkStartDevice</strong></a></p></td>
<td align="left"><p><a href="wdm-markstartdevice.md" data-raw-source="[&lt;strong&gt;MarkStartDevice&lt;/strong&gt;](wdm-markstartdevice.md)"><strong>MarkStartDevice</strong></a>规则指定驱动程序正确 PENDS IRP_MN_START_DEVICE IRP。 此规则仅适用于 FDO 和 FIDO 驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-pendedcompletedrequest.md" data-raw-source="[&lt;strong&gt;PendedCompletedRequest&lt;/strong&gt;](wdm-pendedcompletedrequest.md)"><strong>PendedCompletedRequest</strong></a></p></td>
<td align="left"><p><a href="wdm-pendedcompletedrequest.md" data-raw-source="[&lt;strong&gt;PendedCompletedRequest&lt;/strong&gt;](wdm-pendedcompletedrequest.md)"><strong>PendedCompletedRequest</strong></a>规则指定，如果驱动程序在传入 irp 上调用了<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)"><strong>IoCompleteRequest</strong></a> ，则驱动程序的调度例程不会在 IRP 上返回 STATUS_PENDING。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-pendedcompletedrequest2.md" data-raw-source="[&lt;strong&gt;PendedCompletedRequest2&lt;/strong&gt;](wdm-pendedcompletedrequest2.md)"><strong>PendedCompletedRequest2</strong></a></p></td>
<td align="left"><p><a href="wdm-pendedcompletedrequest2.md" data-raw-source="[&lt;strong&gt;PendedCompletedRequest2&lt;/strong&gt;](wdm-pendedcompletedrequest2.md)"><strong>PendedCompletedRequest2</strong></a>规则指定调用<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)"><strong>IoCallDriver</strong></a>或<a href="/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)"><strong>PoCallDriver</strong></a>后需要等待，因为调度例程可以完成挂起的 IRP。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-pendedcompletedrequest3.md" data-raw-source="[&lt;strong&gt;PendedCompletedRequest3&lt;/strong&gt;](wdm-pendedcompletedrequest3.md)"><strong>PendedCompletedRequest3</strong></a></p></td>
<td align="left"><p><a href="wdm-pendedcompletedrequest3.md" data-raw-source="[&lt;strong&gt;PendedCompletedRequest3&lt;/strong&gt;](wdm-pendedcompletedrequest3.md)"><strong>PendedCompletedRequest3</strong></a>规则指定挂起的 IRP 不应通过调用<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)"><strong>IoCompleteRequest</strong></a>来完成。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-pendedcompletedrequestex.md" data-raw-source="[&lt;strong&gt;PendedCompletedRequestEx&lt;/strong&gt;](wdm-pendedcompletedrequestex.md)"><strong>PendedCompletedRequestEx</strong></a></p></td>
<td align="left"><p><a href="wdm-pendedcompletedrequestex.md" data-raw-source="[&lt;strong&gt;PendedCompletedRequestEx&lt;/strong&gt;](wdm-pendedcompletedrequestex.md)"><strong>PendedCompletedRequestEx</strong></a>规则指定，驱动程序不应为挂起的 IRP 调用<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)"><strong>IoCompleteRequest</strong></a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-startdevicewait.md" data-raw-source="[&lt;strong&gt;StartDeviceWait&lt;/strong&gt;](wdm-startdevicewait.md)"><strong>StartDeviceWait</strong></a></p></td>
<td align="left"><p><a href="wdm-startdevicewait.md" data-raw-source="[&lt;strong&gt;StartDeviceWait&lt;/strong&gt;](wdm-startdevicewait.md)"><strong>StartDeviceWait</strong></a>规则指定驱动程序不应在启动设备 IRP 的上下文中调用<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject" data-raw-source="[&lt;strong&gt;KeWaitForSingleObject&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject)"><strong>KeWaitForSingleObject</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-startdevicewait2.md" data-raw-source="[&lt;strong&gt;StartDeviceWait2&lt;/strong&gt;](wdm-startdevicewait2.md)"><strong>StartDeviceWait2</strong></a></p></td>
<td align="left"><p><a href="wdm-startdevicewait2.md" data-raw-source="[&lt;strong&gt;StartDeviceWait2&lt;/strong&gt;](wdm-startdevicewait2.md)"><strong>StartDeviceWait2</strong></a>规则指定驱动程序不应在启动设备 IRP 的上下文中调用<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject" data-raw-source="[&lt;strong&gt;KeWaitForSingleObject&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject)"><strong>KeWaitForSingleObject</strong></a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-startdevicewait3.md" data-raw-source="[&lt;strong&gt;StartDeviceWait3&lt;/strong&gt;](wdm-startdevicewait3.md)"><strong>StartDeviceWait3</strong></a></p></td>
<td align="left"><p><a href="wdm-startdevicewait3.md" data-raw-source="[&lt;strong&gt;StartDeviceWait3&lt;/strong&gt;](wdm-startdevicewait3.md)"><strong>StartDeviceWait3</strong></a>规则指定驱动程序不应在启动设备 IRP 的上下文中调用<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject" data-raw-source="[&lt;strong&gt;KeWaitForSingleObject&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject)"><strong>KeWaitForSingleObject</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-startdevicewait4.md" data-raw-source="[&lt;strong&gt;StartDeviceWait4&lt;/strong&gt;](wdm-startdevicewait4.md)"><strong>StartDeviceWait4</strong></a></p></td>
<td align="left"><p><a href="wdm-startdevicewait4.md" data-raw-source="[&lt;strong&gt;StartDeviceWait4&lt;/strong&gt;](wdm-startdevicewait4.md)"><strong>StartDeviceWait4</strong></a>规则指定驱动程序不应在启动设备 IRP 的上下文中调用<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject" data-raw-source="[&lt;strong&gt;KeWaitForSingleObject&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject)"><strong>KeWaitForSingleObject</strong></a> 。</p></td>
</tr>
</tbody>
</table>

 

**选择 IrpPending 规则集**

1.  选择你的驱动程序项目 () 在 Microsoft Visual Studio 中。 在 " **驱动程序** " 菜单中，单击 " **启动静态驱动程序验证程序 ...**"。

2.  单击 " **规则** " 选项卡。在 " **规则集**" 下，选择 **IrpPending**。

    若要从 Visual Studio 开发人员命令提示符窗口中选择默认规则集，请使用 **/check**选项指定**IrpPending。 sdv** 。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:IrpPending.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅 [使用静态驱动程序验证器查找驱动程序中的缺陷](./using-static-driver-verifier-to-find-defects-in-drivers.md) 和 [静态驱动程序验证程序命令 (MSBuild) ](./-static-driver-verifier-commands--msbuild-.md)。

