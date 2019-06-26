---
title: DriverEntry 的显示微型端口驱动程序函数
description: DriverEntry 函数提供的 Microsoft DirectX 图形内核子系统具有一系列由显示微型端口驱动程序实现的函数的指针。
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
ms.openlocfilehash: 2c1ccf893b087f9c478ad4b45fc47f0370fb58e9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353840"
---
# <a name="driverentry-of-display-miniport-driver-function"></a>DriverEntry 的显示微型端口驱动程序函数


**DriverEntry**函数提供了 Microsoft DirectX 图形内核子系统具有一系列由显示微型端口驱动程序实现的函数的指针。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
NTSTATUS DriverEntry(
  _In_ PDRIVER_OBJECT  DriverObject,
  _In_ PUNICODE_STRING RegistryPath
);
```

<a name="parameters"></a>Parameters
----------

*DriverObject* \[中\]指向的指针[**驱动程序\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_driver_object)结构，它表示该驱动程序 （显示微型端口，显示的格式端口） 驱动程序对。

*RegistryPath* \[中\]指向的指针[ **UNICODE\_字符串**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfwdm/ns-wudfwdm-_unicode_string)结构能够提供驱动程序的注册表项的路径。

<a name="return-value"></a>返回值
------------

**DriverEntry**调用[ **DxgkInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nf-dispmprt-dxgkinitialize)并且必须返回返回的值**DxgkInitialize**。

<a name="remarks"></a>备注
-------

**DriverEntry**必须执行以下步骤：

1.  分配[**驱动程序\_初始化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_driver_initialization_data)结构，并设置其**版本**成员添加到 DXGKDDI\_接口\_Dispmprt.h 中定义的版本。

2.  填写其余的成员[**驱动程序\_初始化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_driver_initialization_data)与由显示微型端口实现的以下函数的指针的结构驱动程序。

    -   [*DxgkDdiAcquireSwizzlingRange*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_acquireswizzlingrange)
    -   [*DxgkDdiAddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_add_device)
    -   [*DxgkDdiBuildPagingBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)
    -   [*DxgkDdiCalibrateGpuClock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_calibrategpuclock) (DXGKDDI\_INTERFACE\_VERSION &gt;= DXGKDDI\_INTERFACE\_VERSION\_WDDM1\_3)
    -   [*DxgkDdiCancelCommand*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_cancelcommand) (DXGKDDI\_INTERFACE\_VERSION &gt;= DXGKDDI\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiCheckMultiPlaneOverlaySupport*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_checkmultiplaneoverlaysupport) (DXGKDDI\_INTERFACE\_VERSION &gt;= DXGKDDI\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiCloseAllocation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_closeallocation)
    -   [*DxgkDdiCollectDbgInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_collectdbginfo)
    -   [*DxgkDdiCommitVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_commitvidpn)
    -   [*DxgkDdiControlEtwLogging*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_control_etw_logging)
    -   [*DxgkDdiControlInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_controlinterrupt)
    -   [*DxgkDdiCreateAllocation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)
    -   [*DxgkDdiCreateContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_createcontext)
    -   [*DxgkDdiCreateDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_createdevice)
    -   [*DxgkDdiCreateOverlay*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_createoverlay)
    -   [*DxgkDdiDescribeAllocation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_describeallocation)
    -   [*DxgkDdiDestroyAllocation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_destroyallocation)
    -   [*DxgkDdiDestroyContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_destroycontext)
    -   [*DxgkDdiDestroyDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_destroydevice)
    -   [*DxgkDdiDestroyOverlay*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_destroyoverlay)
    -   [*DxgkDdiDispatchIoRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_dispatch_io_request)
    -   [*DxgkDdiDpcRoutine*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_dpc_routine)
    -   [*DxgkDdiEnumVidPnCofuncModality*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_enumvidpncofuncmodality)
    -   [*DxgkDdiEscape*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_escape)
    -   [*DxgkDdiFlipOverlay*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_flipoverlay)
    -   [*DxgkDdiFormatHistoryBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_formathistorybuffer) (DXGKDDI\_INTERFACE\_VERSION &gt;= DXGKDDI\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiGetChildContainerId*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_get_child_container_id) (DXGKDDI\_INTERFACE\_VERSION &gt;= DXGKDDI\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiGetNodeMetadata*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_getnodemetadata) (DXGKDDI\_INTERFACE\_VERSION &gt;= DXGKDDI\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiGetScanLine*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_getscanline)
    -   [*DxgkDdiGetStandardAllocationDriverData*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_getstandardallocationdriverdata)
    -   [*DxgkDdiInterruptRoutine*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_interrupt_routine)
    -   [*DxgkDdiIsSupportedVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_issupportedvidpn)
    -   [*DxgkDdiLinkDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_link_device)
    -   [*DxgkDdiNotifyAcpiEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_notify_acpi_event) (optional)
    -   [*DxgkDdiNotifySurpriseRemoval*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_notify_surprise_removal) (DXGKDDI\_INTERFACE\_VERSION &gt;= DXGKDDI\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiOpenAllocation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_openallocationinfo)
    -   [*DxgkDdiPatch*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_patch)
    -   [*DxgkDdiPowerRuntimeControlRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddipowerruntimecontrolrequest) (DXGKDDI\_INTERFACE\_VERSION &gt;= DXGKDDI\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiPreemptCommand*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_preemptcommand)
    -   [*DxgkDdiPresent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_present)
    -   [*DxgkDdiQueryAdapterInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo)
    -   [*DxgkDdiQueryChildRelations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_query_child_relations)
    -   [*DxgkDdiQueryChildStatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_query_child_status)
    -   [*DxgkDdiQueryCurrentFence*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_querycurrentfence)
    -   [*DxgkDdiQueryDependentEngineGroup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_querydependentenginegroup) (DXGKDDI\_INTERFACE\_VERSION &gt;= DXGKDDI\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiQueryDeviceDescriptor*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_query_device_descriptor)
    -   [*DxgkDdiQueryEngineStatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_queryenginestatus) (DXGKDDI\_INTERFACE\_VERSION &gt;= DXGKDDI\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiQueryInterface*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_query_interface)
    -   [*DxgkDdiQueryVidPnHWCapability*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_queryvidpnhwcapability) (DXGKDDI\_INTERFACE\_VERSION &gt;= DXGKDDI\_INTERFACE\_VERSION\_WIN7)
    -   [*DxgkDdiRecommendFunctionalVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendfunctionalvidpn)
    -   [*DxgkDdiRecommendMonitorModes*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendmonitormodes)
    -   [*DxgkDdiRecommendVidPnTopology*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendvidpntopology)
    -   [*DxgkDdiReleaseSwizzlingRange*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_releaseswizzlingrange)
    -   [*DxgkDdiRemoveDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_remove_device)
    -   [*DxgkDdiRender*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_render)
    -   [*DxgkDdiRenderKm*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm) (DXGKDDI\_INTERFACE\_VERSION &gt;= DXGKDDI\_INTERFACE\_VERSION\_WIN7)
    -   [*DxgkDdiResetDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_reset_device)
    -   [*DxgkDdiResetEngine*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_resetengine) (DXGKDDI\_INTERFACE\_VERSION &gt;= DXGKDDI\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiResetFromTimeout*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_resetfromtimeout)
    -   [*DxgkDdiRestartFromTimeout*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_restartfromtimeout)
    -   [*DxgkDdiSetDisplayPrivateDriverFormat*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_setdisplayprivatedriverformat)
    -   [*DxgkDdiSetPalette*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_setpalette)
    -   [*DxgkDdiSetPointerPosition*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_setpointerposition)
    -   [*DxgkDdiSetPointerShape*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_setpointershape)
    -   [*DxgkDdiSetPowerComponentFState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddisetpowercomponentfstate) (DXGKDDI\_INTERFACE\_VERSION &gt;= DXGKDDI\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiSetPowerState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_set_power_state)
    -   [*DxgkDdiSetVidPnSourceAddress*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff560767(v=vs.85))
    -   [*DxgkDdiSetVidPnSourceVisibility*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_setvidpnsourcevisibility)
    -   [*DxgkDdiStartDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_start_device)
    -   [*DxgkDdiStopCapture*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_stopcapture)
    -   [*DxgkDdiStopDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_stop_device)
    -   [*DxgkDdiStopDeviceAndReleasePostDisplayOwnership*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_stop_device_and_release_post_display_ownership) (DXGKDDI\_INTERFACE\_VERSION &gt;= DXGKDDI\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiSubmitCommand*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand)
    -   [*DxgkDdiSystemDisplayEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_system_display_enable) (DXGKDDI\_INTERFACE\_VERSION &gt;= DXGKDDI\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiSystemDisplayWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_system_display_write) (DXGKDDI\_INTERFACE\_VERSION &gt;= DXGKDDI\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiUnload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_unload)
    -   [*DxgkDdiUpdateActiveVidPnPresentPath*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_updateactivevidpnpresentpath)
    -   [*DxgkDdiUpdateOverlay*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_updateoverlay)


3.  传递*DriverObject*， *RegistryPath*，并已填充中[**驱动程序\_初始化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_driver_initialization_data)结构[ **DxgkInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nf-dispmprt-dxgkinitialize)。

4.  返回由返回的值[ **DxgkInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nf-dispmprt-dxgkinitialize)。

[**驱动程序\_初始化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_driver_initialization_data)结构不需要保留在之后的内存中**DriverEntry**返回。

**DriverEntry**应进行可分页。

内核模式下仅显示驱动程序 (KMDOD) 接口， [KMDDOD_INITIALIZATION_DATA](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_kmddod_initialization_data)结构列出了可以由 KMDOD 实现的所有函数。 所有这些函数中，除[DxgkDdiPresentDisplayOnly](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_presentdisplayonly)函数中，还可以实现完整的显示微型端口驱动程序。  内核模式下仅显示驱动程序 (KMDOD) DriverEntry 函数填写 KMDDOD_INITIALIZATION_DATA 结构的所有成员，然后将传递到该结构提供指向显示端口驱动程序的函数指针[DxgkInitializeDisplayOnlyDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nf-dispmprt-dxgkinitializedisplayonlydriver)函数。

请注意，如果 KMDOD 不支持的 VSync 控制功能，它不应实现某些功能，请参阅保存能源的 VSync 控制。

使用内核模式仅显示驱动程序还使用下面的结构和枚举：

* [D3DKMT_MOVE_RECT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmt_move_rect)
* [D3DKMT_PRESENT_DISPLAY_ONLY_FLAGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_d3dkmt_present_display_only_flags)
* [DXGK_PRESENT_DISPLAY_ONLY_PROGRESS_ID](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ne-d3dkmddi-_dxgk_present_display_only_progress_id)
* [DXGKARG_PRESENT_DISPLAYONLY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_present_displayonly)
* [DXGKARGCB_PRESENT_DISPLAYONLY_PROGRESS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkargcb_present_displayonly_progress)


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
<td align="left">桌面设备</td>
</tr>
<tr class="even">
<td align="left"><p>Version</p></td>
<td align="left"><p>在 Windows Vista 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Library</p></td>
<td align="left">NtosKrnl.lib</td>
</tr>
<tr class="even">
<td align="left"><p>DLL</p></td>
<td align="left">NtosKrnl.exe</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**DxgkInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nf-dispmprt-dxgkinitialize)

[*DxgkDdiUnload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_unload)

 

 






