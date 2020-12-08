---
title: 警告规则集 (KMDF)
description: 了解如何使用 (KDMF) 的规则来验证驱动程序是否可以在不同的上下文中正确处理 Irp，并遵循 Microsoft 推荐的最佳做法。
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8dc770c5442cfa5cfcbd0c84f6c26d702cd8c10c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787573"
---
# <a name="warning-rule-set-kmdf"></a>警告规则集 (KMDF)


使用这些规则来验证驱动程序是否可以在不同的上下文中正确处理 Irp，并遵循 Microsoft 推荐的最佳做法。

## <a name="in-this-section"></a>在本节中


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
<td align="left"><p><a href="kmdf-deferredrequestcompleted.md" data-raw-source="[&lt;strong&gt;DeferredRequestCompleted&lt;/strong&gt;](kmdf-deferredrequestcompleted.md)"><strong>DeferredRequestCompleted</strong></a></p></td>
<td align="left"><p><a href="kmdf-deferredrequestcompleted.md" data-raw-source="[&lt;strong&gt;DeferredRequestCompleted&lt;/strong&gt;](kmdf-deferredrequestcompleted.md)"><strong>DeferredRequestCompleted</strong></a>规则指定，如果向驱动程序的默认 i/o 队列提供的 i/o 请求未在回调函数中完成，但已延迟以便以后处理，则必须在延迟处理回调函数中完成该请求，除非将该请求转发和传递到框架，或除非调用<a href="/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequeststopacknowledge" data-raw-source="[&lt;strong&gt;WdfRequestStopAcknowledge&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequeststopacknowledge)"><strong>WdfRequestStopAcknowledge</strong></a>方法。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-driverattributechanged.md" data-raw-source="[&lt;strong&gt;DriverAttributeChanged&lt;/strong&gt;](kmdf-driverattributechanged.md)"><strong>DriverAttributeChanged</strong></a></p></td>
<td align="left"><p><a href="kmdf-driverattributechanged.md" data-raw-source="[&lt;strong&gt;DriverAttributeChanged&lt;/strong&gt;](kmdf-driverattributechanged.md)"><strong>DriverAttributeChanged</strong></a>规则指定驱动程序不得更改 KMDF 驱动程序的执行级别或同步作用域。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-drvackiostop.md" data-raw-source="[&lt;strong&gt;DrvAckIoStop&lt;/strong&gt;](kmdf-drvackiostop.md)"><strong>DrvAckIoStop</strong></a></p></td>
<td align="left"><p><a href="kmdf-drvackiostop.md" data-raw-source="[&lt;strong&gt;DrvAckIoStop&lt;/strong&gt;](kmdf-drvackiostop.md)"><strong>DrvAckIoStop</strong></a>规则验证驱动程序是否能够识别出挂起的请求，同时驱动程序的电源管理队列正在关闭，驱动程序会相应地确认、完成或取消挂起的请求。 对于自托管 i/o 请求，驱动程序还应从其 <a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoSuspend&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend)"><em>EvtDeviceSelfManagedIoSuspend</em></a> 函数正确处理这些请求。 在关机期间未能处理这些请求的驱动程序将导致 <a href="/windows-hardware/drivers/debugger/bug-check-0x9f--driver-power-state-failure" data-raw-source="[&lt;strong&gt;Bug Check 0x9F: DRIVER_POWER_STATE_FAILURE&lt;/strong&gt;](../debugger/bug-check-0x9f--driver-power-state-failure.md)"><strong>错误检查0x9F： DRIVER_POWER_STATE_FAILURE</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-evtioresumegetparam.md" data-raw-source="[&lt;strong&gt;EvtIoResumeGetParam&lt;/strong&gt;](kmdf-evtioresumegetparam.md)"><strong>EvtIoResumeGetParam</strong></a></p></td>
<td align="left"><p><a href="kmdf-evtioresumegetparam.md" data-raw-source="[&lt;strong&gt;EvtIoResumeGetParam&lt;/strong&gt;](kmdf-evtioresumegetparam.md)"><strong>EvtIoResumeGetParam</strong></a>规则指定在<strong>EvtIoResumeGetParam</strong>回调函数中未调用<a href="/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetparameters" data-raw-source="[&lt;strong&gt;WdfRequestGetParameters&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetparameters)"><strong>WdfRequestGetParameters</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-evtiostopgetparam.md" data-raw-source="[&lt;strong&gt;EvtIoStopGetParam&lt;/strong&gt;](kmdf-evtiostopgetparam.md)"><strong>EvtIoStopGetParam</strong></a></p></td>
<td align="left"><p><a href="kmdf-evtiostopgetparam.md" data-raw-source="[&lt;strong&gt;EvtIoStopGetParam&lt;/strong&gt;](kmdf-evtiostopgetparam.md)"><strong>EvtIoStopGetParam</strong></a>规则检查<a href="/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetparameters" data-raw-source="[&lt;strong&gt;WdfRequestGetParameters&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetparameters)"><strong>WdfRequestGetParameters</strong></a>是否不在<a href="/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)"><em>EvtIoStop</em></a>回调中调用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-evtiostopresume.md" data-raw-source="[&lt;strong&gt;EvtIoStopResume&lt;/strong&gt;](kmdf-evtiostopresume.md)"><strong>EvtIoStopResume</strong></a></p></td>
<td align="left"><p><a href="kmdf-evtiostopresume.md" data-raw-source="[&lt;strong&gt;EvtIoStopResume&lt;/strong&gt;](kmdf-evtiostopresume.md)"><strong>EvtIoStopResume</strong></a>规则指定如果驱动程序注册<a href="/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)"><em>EvtIoStop</em></a>回调函数，然后调用<em>重新排队</em>参数等于<strong>FALSE</strong>的<a href="/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequeststopacknowledge" data-raw-source="[&lt;strong&gt;WdfRequestStopAcknowledge&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequeststopacknowledge)"><strong>WdfRequestStopAcknowledge</strong></a> ，则驱动程序必须注册<a href="/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_resume" data-raw-source="[&lt;em&gt;EvtIoResume&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_resume)"><em>EvtIoResume</em></a>回调函数。 当设备再次进入 D0 状态时，框架会向 <strong>EvtIoResume</strong> 回调函数传递请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-evtsurpriseremovenorequestcomplete.md" data-raw-source="[&lt;strong&gt;EvtSurpriseRemoveNoRequestComplete&lt;/strong&gt;](kmdf-evtsurpriseremovenorequestcomplete.md)"><strong>EvtSurpriseRemoveNoRequestComplete</strong></a></p></td>
<td align="left"><p><a href="kmdf-evtsurpriseremovenorequestcomplete.md" data-raw-source="[&lt;strong&gt;EvtSurpriseRemoveNoRequestComplete&lt;/strong&gt;](kmdf-evtsurpriseremovenorequestcomplete.md)"><strong>EvtSurpriseRemoveNoRequestComplete</strong></a>规则指定 WDF 驱动程序不应使用<a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal" data-raw-source="[&lt;em&gt;EvtDeviceSurpriseRemoval&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal)"><em>EvtDeviceSurpriseRemoval</em></a>回调完成请求，而应使用自托管 i/o 回调函数。 <em>EvtDeviceSurpriseRemoval</em> 回调未与电源线路径同步。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-fdopowerpolicyownerapi.md" data-raw-source="[&lt;strong&gt;FDOPowerPolicyOwnerAPI&lt;/strong&gt;](kmdf-fdopowerpolicyownerapi.md)"><strong>FDOPowerPolicyOwnerAPI</strong></a></p></td>
<td align="left"><p><a href="kmdf-fdopowerpolicyownerapi.md" data-raw-source="[&lt;strong&gt;FDOPowerPolicyOwnerAPI&lt;/strong&gt;](kmdf-fdopowerpolicyownerapi.md)"><strong>FDOPowerPolicyOwnerAPI</strong></a>规则指定如果 FDO driver 让给电源策略所有权，则只能对驱动程序为电源策略所有者的执行路径调用方法<a href="/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyeventcallbacks" data-raw-source="[&lt;strong&gt;WdfDeviceInitSetPowerPolicyEventCallbacks&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyeventcallbacks)"><strong>WdfDeviceInitSetPowerPolicyEventCallbacks</strong></a>、 <a href="/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings" data-raw-source="[&lt;strong&gt;WdfDeviceAssignS0IdleSettings&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)"><strong>WdfDeviceAssignS0IdleSettings</strong></a>和<a href="/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassignsxwakesettings" data-raw-source="[&lt;strong&gt;WdfDeviceAssignSxWakeSettings&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassignsxwakesettings)"><strong>WdfDeviceAssignSxWakeSettings</strong></a> 。 SDV 发出此规则的警告。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-nocancelfromevtsurpriseremove.md" data-raw-source="[&lt;strong&gt;NoCancelFromEvtSurpriseRemove&lt;/strong&gt;](kmdf-nocancelfromevtsurpriseremove.md)"><strong>NoCancelFromEvtSurpriseRemove</strong></a></p></td>
<td align="left"><p><a href="kmdf-nocancelfromevtsurpriseremove.md" data-raw-source="[&lt;strong&gt;NoCancelFromEvtSurpriseRemove&lt;/strong&gt;](kmdf-nocancelfromevtsurpriseremove.md)"><strong>NoCancelFromEvtSurpriseRemove</strong></a>规则指定 WDF 驱动程序不应取消来自<a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal" data-raw-source="[&lt;em&gt;EvtDeviceSurpriseRemoval&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal)"><em>EvtDeviceSurpriseRemoval</em></a>回调函数的请求，而应使用自托管 i/o 回调函数。 <em>EvtDeviceSurpriseRemoval</em> 回调函数未与电源线路径同步。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-pagedcodeatd0.md" data-raw-source="[&lt;strong&gt;PagedCodeAtD0&lt;/strong&gt;](kmdf-pagedcodeatd0.md)"><strong>PagedCodeAtD0</strong></a></p></td>
<td align="left"><p><a href="kmdf-pagedcodeatd0.md" data-raw-source="[&lt;strong&gt;PagedCodeAtD0&lt;/strong&gt;](kmdf-pagedcodeatd0.md)"><strong>PagedCodeAtD0</strong></a>规则指定驱动程序不得将代码标记为可在开机代码路径中的回调函数内进行分页。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-parentobjectcheck.md" data-raw-source="[&lt;strong&gt;ParentObjectCheck&lt;/strong&gt;](kmdf-parentobjectcheck.md)"><strong>ParentObjectCheck</strong></a></p></td>
<td align="left"><p><a href="kmdf-parentobjectcheck.md" data-raw-source="[&lt;strong&gt;ParentObjectCheck&lt;/strong&gt;](kmdf-parentobjectcheck.md)"><strong>ParentObjectCheck</strong></a>规则指定驱动程序应调用<a href="/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycreate" data-raw-source="[&lt;strong&gt;WdfMemoryCreate&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycreate)"><strong>WdfMemoryCreate</strong></a> ，并使用<a href="/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes" data-raw-source="[&lt;strong&gt;WDF_OBJECT_ATTRIBUTES&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)"><strong>WDF_OBJECT_ATTRIBUTES</strong></a>结构指定父对象。 如果驱动程序没有为 framework 内存对象设置父对象，则该框架会将该驱动程序设置为默认父级，因此，除非驱动程序显式删除框架内存对象，否则该驱动程序对象将保留在内存中，直到驱动程序对象卸载。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-reqnotcanceledlocal.md" data-raw-source="[&lt;strong&gt;ReqNotCanceledLocal&lt;/strong&gt;](kmdf-reqnotcanceledlocal.md)"><strong>ReqNotCanceledLocal</strong></a></p></td>
<td align="left"><p><a href="kmdf-reqnotcanceledlocal.md" data-raw-source="[&lt;strong&gt;ReqNotCanceledLocal&lt;/strong&gt;](kmdf-reqnotcanceledlocal.md)"><strong>ReqNotCanceledLocal</strong></a>规则指定如果在默认 i/o 队列回调函数中完成标记为可取消的请求，则必须在完成 i/o 请求之前调用<a href="/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestunmarkcancelable" data-raw-source="[&lt;strong&gt;WdfRequestUnmarkCancelable&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestunmarkcancelable)"><strong>WdfRequestUnmarkCancelable</strong></a>方法。 必须完成 i/o 请求，除非该请求在调用 <strong>WdfRequestUnmarkCancelable</strong>之前取消。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-reqsendfail.md" data-raw-source="[&lt;strong&gt;ReqSendFail&lt;/strong&gt;](kmdf-reqsendfail.md)"><strong>ReqSendFail</strong></a></p></td>
<td align="left"><p><a href="kmdf-reqsendfail.md" data-raw-source="[&lt;strong&gt;ReqSendFail&lt;/strong&gt;](kmdf-reqsendfail.md)"><strong>ReqSendFail</strong></a>规则指定在<a href="/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend" data-raw-source="[&lt;strong&gt;WdfRequestSend&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)"><strong>WdfRequestSend</strong></a>方法可能失败的情况下，驱动程序必须设置正确的完成状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-requestcompletedlocal.md" data-raw-source="[&lt;strong&gt;RequestCompletedLocal&lt;/strong&gt;](kmdf-requestcompletedlocal.md)"><strong>RequestCompletedLocal</strong></a></p></td>
<td align="left"><p><a href="kmdf-requestcompletedlocal.md" data-raw-source="[&lt;strong&gt;RequestCompletedLocal&lt;/strong&gt;](kmdf-requestcompletedlocal.md)"><strong>RequestCompletedLocal</strong></a>规则指定，如果未在任何<a href="/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default" data-raw-source="[&lt;em&gt;EvtIoDefault&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)"><em>EvtIoDefault</em></a>、 <a href="/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read" data-raw-source="[&lt;em&gt;EvtIoRead&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)"><em>EvtIoRead</em></a>、 <a href="/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write" data-raw-source="[&lt;em&gt;EvtIoWrite&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)"><em>EvtIoWrite</em></a>、 <a href="/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control" data-raw-source="[&lt;em&gt;EvtIoDeviceControl&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)"><em>EvtIoDeviceControl</em></a>和<a href="/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control" data-raw-source="[&lt;em&gt;EvtIoInternalDeviceControl&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)"><em>EvtIoInternalDeviceControl</em></a>回调函数中完成 I/o 请求，并且在回调函数内未对请求调用<a href="/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable" data-raw-source="[&lt;strong&gt;WdfRequestMarkCancelable&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable)"><strong>WdfRequestMarkCancelable</strong></a> ，则驱动程序的代码中可能存在请求完成的问题。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-requestforurbxrb.md" data-raw-source="[&lt;strong&gt;RequestForUrbXrb&lt;/strong&gt;](kmdf-requestforurbxrb.md)"><strong>RequestForUrbXrb</strong></a></p></td>
<td align="left"><p>如果客户端驱动程序调用 <a href="/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceCreateWithParameters&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)"><strong>WdfUsbTargetDeviceCreateWithParameters</strong></a> ，并指定 WDF_USB_DEVICE_CREATE_CONFIG 结构中 USBD_CLIENT_CONTRACT_VERSION_602 的客户端协定版本 (为使用适用于 Windows) 8 的 USB 驱动程序堆栈的新功能，则在内部使用 URB 的 DDIs 将仅在以下任何前提条件适用时才使用 <em>URB 上下文</em> ：</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-syncreqsend.md" data-raw-source="[&lt;strong&gt;SyncReqSend&lt;/strong&gt;](kmdf-syncreqsend.md)"><strong>SyncReqSend</strong></a></p></td>
<td align="left"><p><a href="kmdf-syncreqsend.md" data-raw-source="[&lt;strong&gt;SyncReqSend&lt;/strong&gt;](kmdf-syncreqsend.md)"><strong>SyncReqSend</strong></a>规则指定所有同步发送请求都是使用特定于同步的 KMDF 设备驱动程序接口方法来完成的，并且这些方法的超时值设置为非零值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-syncreqsend2.md" data-raw-source="[&lt;strong&gt;SyncReqSend2&lt;/strong&gt;](kmdf-syncreqsend2.md)"><strong>SyncReqSend2</strong></a></p></td>
<td align="left"><p><a href="kmdf-syncreqsend2.md" data-raw-source="[&lt;strong&gt;SyncReqSend2&lt;/strong&gt;](kmdf-syncreqsend2.md)"><strong>SyncReqSend2</strong></a>规则指定同步请求发送的超时值设置为非零值。</p></td>
</tr>
</tbody>
</table>

 

**选择警告规则集**

1.  选择你的驱动程序项目 () 在 Microsoft Visual Studio 中。 在 " **驱动程序** " 菜单中，单击 " **启动静态驱动程序验证程序 ...**"。

2.  单击 " **规则** " 选项卡。在 " **规则集**" 下，选择 " **警告**"。

    若要从 Visual Studio 开发人员命令提示符窗口中选择默认规则集，请指定带有 **/check** 选项的 **sdv** 。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:Warning.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅 [使用静态驱动程序验证器查找驱动程序中的缺陷](./using-static-driver-verifier-to-find-defects-in-drivers.md) 和 [静态驱动程序验证程序命令 (MSBuild) ](./-static-driver-verifier-commands--msbuild-.md)。

