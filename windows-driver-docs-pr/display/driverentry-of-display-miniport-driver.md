---
title: 显示微型端口驱动程序函数的 DriverEntry
description: DriverEntry 函数提供 Microsoft DirectX 图形内核子系统，其中包含一组指向由显示微型端口驱动程序实现的函数的指针。
ms.assetid: 64b4e9d5-eb6e-48ab-95bf-a237ec32a54b
keywords:
- DriverEntry 函数显示设备
topic_type:
- apiref
api_name:
- DriverEntry
api_location:
- NtosKrnl.exe
api_type:
- DllExport
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: c3172528cbd203a2154f1c45ea6c3a75005e95f0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838983"
---
# <a name="driverentry-of-display-miniport-driver-function"></a>显示微型端口驱动程序函数的 DriverEntry


**DriverEntry**函数提供 Microsoft DirectX 图形内核子系统，其中包含一组指向由显示微型端口驱动程序实现的函数的指针。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
NTSTATUS DriverEntry(
  _In_ PDRIVER_OBJECT  DriverObject,
  _In_ PUNICODE_STRING RegistryPath
);
```

<a name="parameters"></a>参数
----------

*DriverObject* \[在\] 指向[**驱动程序\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_driver_object)结构的指针，该对象结构表示由（显示微型端口、显示端口）驱动程序对构成的驱动程序。

*RegistryPath* \[在\] 指向[**UNICODE\_字符串**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/ns-wudfwdm-_unicode_string)结构的指针，该字符串结构提供驱动程序的注册表项的路径。

<a name="return-value"></a>返回值
------------

**DriverEntry**调用[**DxgkInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nf-dispmprt-dxgkinitialize) ，并且必须返回**DxgkInitialize**返回的值。

<a name="remarks"></a>备注
-------

**DriverEntry**必须执行以下步骤：

1.  [ **\_数据结构中\_初始化分配驱动程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_driver_initialization_data)，并将其**版本**成员设置为 DISPMPRT 中定义的 DXGKDDI\_接口\_版本。

2.  使用指向以下函数（由显示微型端口驱动程序实现）的指针填充驱动程序的其余成员[ **\_初始化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_driver_initialization_data)结构。

    -   [*DxgkDdiAcquireSwizzlingRange*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_acquireswizzlingrange)
    -   [*DxgkDdiAddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_add_device)
    -   [*DxgkDdiBuildPagingBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)
    -   [*DxgkDdiCalibrateGpuClock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_calibrategpuclock) （DXGKDDI\_接口\_版本 &gt;= DXGKDDI\_接口\_版本\_WDDM1\_3）
    -   [*DxgkDdiCancelCommand*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_cancelcommand) （DXGKDDI\_接口\_版本 &gt;= DXGKDDI\_接口\_版本\_WIN8）
    -   [*DxgkDdiCheckMultiPlaneOverlaySupport*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_checkmultiplaneoverlaysupport) （DXGKDDI\_接口\_版本 &gt;= DXGKDDI\_接口\_版本\_WIN8）
    -   [*DxgkDdiCloseAllocation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_closeallocation)
    -   [*DxgkDdiCollectDbgInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_collectdbginfo)
    -   [*DxgkDdiCommitVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_commitvidpn)
    -   [*DxgkDdiControlEtwLogging*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_control_etw_logging)
    -   [*DxgkDdiControlInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_controlinterrupt)
    -   [*DxgkDdiCreateAllocation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)
    -   [*DxgkDdiCreateContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createcontext)
    -   [*DxgkDdiCreateDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createdevice)
    -   [*DxgkDdiCreateOverlay*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createoverlay)
    -   [*DxgkDdiDescribeAllocation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_describeallocation)
    -   [*DxgkDdiDestroyAllocation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_destroyallocation)
    -   [*DxgkDdiDestroyContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_destroycontext)
    -   [*DxgkDdiDestroyDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_destroydevice)
    -   [*DxgkDdiDestroyOverlay*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_destroyoverlay)
    -   [*DxgkDdiDispatchIoRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_dispatch_io_request)
    -   [*DxgkDdiDpcRoutine*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_dpc_routine)
    -   [*DxgkDdiEnumVidPnCofuncModality*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_enumvidpncofuncmodality)
    -   [*DxgkDdiEscape*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_escape)
    -   [*DxgkDdiFlipOverlay*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_flipoverlay)
    -   [*DxgkDdiFormatHistoryBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_formathistorybuffer) （DXGKDDI\_接口\_版本 &gt;= DXGKDDI\_接口\_版本\_WIN8）
    -   [*DxgkDdiGetChildContainerId*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_get_child_container_id) （DXGKDDI\_接口\_版本 &gt;= DXGKDDI\_接口\_版本\_WIN8）
    -   [*DxgkDdiGetNodeMetadata*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_getnodemetadata) （DXGKDDI\_接口\_版本 &gt;= DXGKDDI\_接口\_版本\_WIN8）
    -   [*DxgkDdiGetScanLine*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_getscanline)
    -   [*DxgkDdiGetStandardAllocationDriverData*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_getstandardallocationdriverdata)
    -   [*DxgkDdiInterruptRoutine*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_interrupt_routine)
    -   [*DxgkDdiIsSupportedVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_issupportedvidpn)
    -   [*DxgkDdiLinkDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_link_device)
    -   [*DxgkDdiNotifyAcpiEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_notify_acpi_event) （可选）
    -   [*DxgkDdiNotifySurpriseRemoval*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_notify_surprise_removal) （DXGKDDI\_接口\_版本 &gt;= DXGKDDI\_接口\_版本\_WIN8）
    -   [*DxgkDdiOpenAllocation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_openallocationinfo)
    -   [*DxgkDdiPatch*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_patch)
    -   [*DxgkDdiPowerRuntimeControlRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddipowerruntimecontrolrequest) （DXGKDDI\_接口\_版本 &gt;= DXGKDDI\_接口\_版本\_WIN8）
    -   [*DxgkDdiPreemptCommand*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_preemptcommand)
    -   [*DxgkDdiPresent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_present)
    -   [*DxgkDdiQueryAdapterInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo)
    -   [*DxgkDdiQueryChildRelations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_child_relations)
    -   [*DxgkDdiQueryChildStatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_child_status)
    -   [*DxgkDdiQueryCurrentFence*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_querycurrentfence)
    -   [*DxgkDdiQueryDependentEngineGroup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_querydependentenginegroup) （DXGKDDI\_接口\_版本 &gt;= DXGKDDI\_接口\_版本\_WIN8）
    -   [*DxgkDdiQueryDeviceDescriptor*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_device_descriptor)
    -   [*DxgkDdiQueryEngineStatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryenginestatus) （DXGKDDI\_接口\_版本 &gt;= DXGKDDI\_接口\_版本\_WIN8）
    -   [*DxgkDdiQueryInterface*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_interface)
    -   [*DxgkDdiQueryVidPnHWCapability*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryvidpnhwcapability) （DXGKDDI\_接口\_版本 &gt;= DXGKDDI\_接口\_版本\_WIN7）
    -   [*DxgkDdiRecommendFunctionalVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendfunctionalvidpn)
    -   [*DxgkDdiRecommendMonitorModes*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendmonitormodes)
    -   [*DxgkDdiRecommendVidPnTopology*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendvidpntopology)
    -   [*DxgkDdiReleaseSwizzlingRange*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_releaseswizzlingrange)
    -   [*DxgkDdiRemoveDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_remove_device)
    -   [*DxgkDdiRender*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_render)
    -   [*DxgkDdiRenderKm*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm) （DXGKDDI\_接口\_版本 &gt;= DXGKDDI\_接口\_版本\_WIN7）
    -   [*DxgkDdiResetDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_reset_device)
    -   [*DxgkDdiResetEngine*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_resetengine) （DXGKDDI\_接口\_版本 &gt;= DXGKDDI\_接口\_版本\_WIN8）
    -   [*DxgkDdiResetFromTimeout*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_resetfromtimeout)
    -   [*DxgkDdiRestartFromTimeout*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_restartfromtimeout)
    -   [*DxgkDdiSetDisplayPrivateDriverFormat*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setdisplayprivatedriverformat)
    -   [*DxgkDdiSetPalette*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setpalette)
    -   [*DxgkDdiSetPointerPosition*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setpointerposition)
    -   [*DxgkDdiSetPointerShape*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setpointershape)
    -   [*DxgkDdiSetPowerComponentFState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddisetpowercomponentfstate) （DXGKDDI\_接口\_版本 &gt;= DXGKDDI\_接口\_版本\_WIN8）
    -   [*DxgkDdiSetPowerState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_set_power_state)
    -   [*DxgkDdiSetVidPnSourceAddress*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff560767(v=vs.85))
    -   [*DxgkDdiSetVidPnSourceVisibility*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setvidpnsourcevisibility)
    -   [*DxgkDdiStartDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_start_device)
    -   [*DxgkDdiStopCapture*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_stopcapture)
    -   [*DxgkDdiStopDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_stop_device)
    -   [*DxgkDdiStopDeviceAndReleasePostDisplayOwnership*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_stop_device_and_release_post_display_ownership) （DXGKDDI\_接口\_版本 &gt;= DXGKDDI\_接口\_版本\_WIN8）
    -   [*DxgkDdiSubmitCommand*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand)
    -   [*DxgkDdiSystemDisplayEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_system_display_enable) （DXGKDDI\_接口\_版本 &gt;= DXGKDDI\_接口\_版本\_WIN8）
    -   [*DxgkDdiSystemDisplayWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_system_display_write) （DXGKDDI\_接口\_版本 &gt;= DXGKDDI\_接口\_版本\_WIN8）
    -   [*DxgkDdiUnload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_unload)
    -   [*DxgkDdiUpdateActiveVidPnPresentPath*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_updateactivevidpnpresentpath)
    -   [*DxgkDdiUpdateOverlay*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_updateoverlay)


3.  将*DriverObject*、 *RegistryPath*和填充的[**驱动程序\_初始化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_driver_initialization_data)结构传递到[**DxgkInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nf-dispmprt-dxgkinitialize)。

4.  返回[**DxgkInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nf-dispmprt-dxgkinitialize)返回的值。

**DriverEntry**返回后， [ **\_数据结构的驱动程序\_初始化**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_driver_initialization_data)不需要保留在内存中。

**DriverEntry**应进行分页。

对于 "仅限内核模式显示驱动程序（KMDOD）" 接口， [KMDDOD_INITIALIZATION_DATA](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_kmddod_initialization_data)结构列出了可由 KMDOD 实现的所有函数。 除[DxgkDdiPresentDisplayOnly](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_presentdisplayonly)函数之外的所有函数也可以通过完整的显示微型端口驱动程序来实现。  仅限内核模式显示驱动程序（KMDOD）的 DriverEntry 函数通过填写 KMDDOD_INITIALIZATION_DATA 结构的所有成员，然后将该结构传递到[DxgkInitializeDisplayOnlyDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nf-dispmprt-dxgkinitializedisplayonlydriver)函数。

请注意，如果 KMDOD 不支持 VSync 控件功能，它不应实现某些功能，请参阅使用 VSync 控件节省能源。

以下结构和枚举还用于内核模式仅显示驱动程序：

* [D3DKMT_MOVE_RECT](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmt_move_rect)
* [D3DKMT_PRESENT_DISPLAY_ONLY_FLAGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_d3dkmt_present_display_only_flags)
* [DXGK_PRESENT_DISPLAY_ONLY_PROGRESS_ID](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ne-d3dkmddi-_dxgk_present_display_only_progress_id)
* [DXGKARG_PRESENT_DISPLAYONLY](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_present_displayonly)
* [DXGKARGCB_PRESENT_DISPLAYONLY_PROGRESS](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkargcb_present_displayonly_progress)


<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>目标平台</p></td>
<td align="left">桌面</td>
</tr>
<tr class="even">
<td align="left"><p>版本</p></td>
<td align="left"><p>在 Windows Vista 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>库</p></td>
<td align="left">Ntoskrnl.exe</td>
</tr>
<tr class="even">
<td align="left"><p>DLL</p></td>
<td align="left">Ntoskrnl.exe</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**DxgkInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nf-dispmprt-dxgkinitialize)

[*DxgkDdiUnload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_unload)

 

 






