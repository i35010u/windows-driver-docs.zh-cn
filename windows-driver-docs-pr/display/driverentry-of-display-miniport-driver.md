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
ms.openlocfilehash: 16f7b2c43dc21a2cf24a0cde9349b926a20805c7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569229"
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

*DriverObject* \[中\]指向的指针[**驱动程序\_对象**](https://msdn.microsoft.com/library/windows/hardware/ff544174)结构，它表示该驱动程序 （显示微型端口，显示的格式端口） 驱动程序对。

*RegistryPath* \[中\]指向的指针[ **UNICODE\_字符串**](https://msdn.microsoft.com/library/windows/hardware/ff564879)结构能够提供驱动程序的注册表项的路径。

<a name="return-value"></a>返回值
------------

**DriverEntry**调用[ **DxgkInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff560824)并且必须返回返回的值**DxgkInitialize**。

<a name="remarks"></a>备注
-------

**DriverEntry**必须执行以下步骤：

1.  分配[**驱动程序\_初始化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff556169)结构，并设置其**版本**成员添加到 DXGKDDI\_接口\_Dispmprt.h 中定义的版本。

2.  填写其余的成员[**驱动程序\_初始化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff556169)与由显示微型端口实现的以下函数的指针的结构驱动程序。

    -   [*DxgkDdiAcquireSwizzlingRange*](https://msdn.microsoft.com/library/windows/hardware/ff559582)
    -   [*DxgkDdiAddDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559586)
    -   [*DxgkDdiBuildPagingBuffer*](https://msdn.microsoft.com/library/windows/hardware/ff559587)
    -   [*DxgkDdiCalibrateGpuClock*](https://msdn.microsoft.com/library/windows/hardware/dn467321) (DXGKDDI\_INTERFACE\_VERSION &gt;= DXGKDDI\_INTERFACE\_VERSION\_WDDM1\_3)
    -   [*DxgkDdiCancelCommand*](https://msdn.microsoft.com/library/windows/hardware/hh451344) (DXGKDDI\_INTERFACE\_VERSION &gt;= DXGKDDI\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiCheckMultiPlaneOverlaySupport*](https://msdn.microsoft.com/library/windows/hardware/dn282642) (DXGKDDI\_INTERFACE\_VERSION &gt;= DXGKDDI\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiCloseAllocation*](https://msdn.microsoft.com/library/windows/hardware/ff559592)
    -   [*DxgkDdiCollectDbgInfo*](https://msdn.microsoft.com/library/windows/hardware/ff559595)
    -   [*DxgkDdiCommitVidPn*](https://msdn.microsoft.com/library/windows/hardware/ff559597)
    -   [*DxgkDdiControlEtwLogging*](https://msdn.microsoft.com/library/windows/hardware/ff559599)
    -   [*DxgkDdiControlInterrupt*](https://msdn.microsoft.com/library/windows/hardware/ff559602)
    -   [*DxgkDdiCreateAllocation*](https://msdn.microsoft.com/library/windows/hardware/ff559606)
    -   [*DxgkDdiCreateContext*](https://msdn.microsoft.com/library/windows/hardware/ff559612)
    -   [*DxgkDdiCreateDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559615)
    -   [*DxgkDdiCreateOverlay*](https://msdn.microsoft.com/library/windows/hardware/ff559616)
    -   [*DxgkDdiDescribeAllocation*](https://msdn.microsoft.com/library/windows/hardware/ff559620)
    -   [*DxgkDdiDestroyAllocation*](https://msdn.microsoft.com/library/windows/hardware/ff559630)
    -   [*DxgkDdiDestroyContext*](https://msdn.microsoft.com/library/windows/hardware/ff559636)
    -   [*DxgkDdiDestroyDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559639)
    -   [*DxgkDdiDestroyOverlay*](https://msdn.microsoft.com/library/windows/hardware/ff559642)
    -   [*DxgkDdiDispatchIoRequest*](https://msdn.microsoft.com/library/windows/hardware/ff559643)
    -   [*DxgkDdiDpcRoutine*](https://msdn.microsoft.com/library/windows/hardware/ff559645)
    -   [*DxgkDdiEnumVidPnCofuncModality*](https://msdn.microsoft.com/library/windows/hardware/ff559649)
    -   [*DxgkDdiEscape*](https://msdn.microsoft.com/library/windows/hardware/ff559653)
    -   [*DxgkDdiFlipOverlay*](https://msdn.microsoft.com/library/windows/hardware/ff559655)
    -   [*DxgkDdiFormatHistoryBuffer*](https://msdn.microsoft.com/library/windows/hardware/dn439360) (DXGKDDI\_INTERFACE\_VERSION &gt;= DXGKDDI\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiGetChildContainerId*](https://msdn.microsoft.com/library/windows/hardware/hh451349) (DXGKDDI\_INTERFACE\_VERSION &gt;= DXGKDDI\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiGetNodeMetadata*](https://msdn.microsoft.com/library/windows/hardware/dn265415) (DXGKDDI\_INTERFACE\_VERSION &gt;= DXGKDDI\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiGetScanLine*](https://msdn.microsoft.com/library/windows/hardware/ff559668)
    -   [*DxgkDdiGetStandardAllocationDriverData*](https://msdn.microsoft.com/library/windows/hardware/ff559673)
    -   [*DxgkDdiInterruptRoutine*](https://msdn.microsoft.com/library/windows/hardware/ff559680)
    -   [*DxgkDdiIsSupportedVidPn*](https://msdn.microsoft.com/library/windows/hardware/ff559684)
    -   [*DxgkDdiLinkDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559687)
    -   [*DxgkDdiNotifyAcpiEvent*](https://msdn.microsoft.com/library/windows/hardware/ff559695) (optional)
    -   [*DxgkDdiNotifySurpriseRemoval*](https://msdn.microsoft.com/library/windows/hardware/hh780297) (DXGKDDI\_INTERFACE\_VERSION &gt;= DXGKDDI\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiOpenAllocation*](https://msdn.microsoft.com/library/windows/hardware/ff559699)
    -   [*DxgkDdiPatch*](https://msdn.microsoft.com/library/windows/hardware/ff559737)
    -   [*DxgkDdiPowerRuntimeControlRequest*](https://msdn.microsoft.com/library/windows/hardware/hh451396) (DXGKDDI\_INTERFACE\_VERSION &gt;= DXGKDDI\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiPreemptCommand*](https://msdn.microsoft.com/library/windows/hardware/ff559741)
    -   [*DxgkDdiPresent*](https://msdn.microsoft.com/library/windows/hardware/ff559743)
    -   [*DxgkDdiQueryAdapterInfo*](https://msdn.microsoft.com/library/windows/hardware/ff559746)
    -   [*DxgkDdiQueryChildRelations*](https://msdn.microsoft.com/library/windows/hardware/ff559750)
    -   [*DxgkDdiQueryChildStatus*](https://msdn.microsoft.com/library/windows/hardware/ff559754)
    -   [*DxgkDdiQueryCurrentFence*](https://msdn.microsoft.com/library/windows/hardware/ff559758)
    -   [*DxgkDdiQueryDependentEngineGroup*](https://msdn.microsoft.com/library/windows/hardware/hh451407) (DXGKDDI\_INTERFACE\_VERSION &gt;= DXGKDDI\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiQueryDeviceDescriptor*](https://msdn.microsoft.com/library/windows/hardware/ff559761)
    -   [*DxgkDdiQueryEngineStatus*](https://msdn.microsoft.com/library/windows/hardware/hh451411) (DXGKDDI\_INTERFACE\_VERSION &gt;= DXGKDDI\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiQueryInterface*](https://msdn.microsoft.com/library/windows/hardware/ff559764)
    -   [*DxgkDdiQueryVidPnHWCapability*](https://msdn.microsoft.com/library/windows/hardware/ff559771) (DXGKDDI\_INTERFACE\_VERSION &gt;= DXGKDDI\_INTERFACE\_VERSION\_WIN7)
    -   [*DxgkDdiRecommendFunctionalVidPn*](https://msdn.microsoft.com/library/windows/hardware/ff559775)
    -   [*DxgkDdiRecommendMonitorModes*](https://msdn.microsoft.com/library/windows/hardware/ff559780)
    -   [*DxgkDdiRecommendVidPnTopology*](https://msdn.microsoft.com/library/windows/hardware/ff559782)
    -   [*DxgkDdiReleaseSwizzlingRange*](https://msdn.microsoft.com/library/windows/hardware/ff559786)
    -   [*DxgkDdiRemoveDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559789)
    -   [*DxgkDdiRender*](https://msdn.microsoft.com/library/windows/hardware/ff559793)
    -   [*DxgkDdiRenderKm*](https://msdn.microsoft.com/library/windows/hardware/ff559800) (DXGKDDI\_INTERFACE\_VERSION &gt;= DXGKDDI\_INTERFACE\_VERSION\_WIN7)
    -   [*DxgkDdiResetDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559808)
    -   [*DxgkDdiResetEngine*](https://msdn.microsoft.com/library/windows/hardware/hh451418) (DXGKDDI\_INTERFACE\_VERSION &gt;= DXGKDDI\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiResetFromTimeout*](https://msdn.microsoft.com/library/windows/hardware/ff559815)
    -   [*DxgkDdiRestartFromTimeout*](https://msdn.microsoft.com/library/windows/hardware/ff559820)
    -   [*DxgkDdiSetDisplayPrivateDriverFormat*](https://msdn.microsoft.com/library/windows/hardware/ff560751)
    -   [*DxgkDdiSetPalette*](https://msdn.microsoft.com/library/windows/hardware/ff560754)
    -   [*DxgkDdiSetPointerPosition*](https://msdn.microsoft.com/library/windows/hardware/ff560757)
    -   [*DxgkDdiSetPointerShape*](https://msdn.microsoft.com/library/windows/hardware/ff560762)
    -   [*DxgkDdiSetPowerComponentFState*](https://msdn.microsoft.com/library/windows/hardware/hh451422) (DXGKDDI\_INTERFACE\_VERSION &gt;= DXGKDDI\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiSetPowerState*](https://msdn.microsoft.com/library/windows/hardware/ff560764)
    -   [*DxgkDdiSetVidPnSourceAddress*](https://msdn.microsoft.com/library/windows/hardware/ff560767)
    -   [*DxgkDdiSetVidPnSourceVisibility*](https://msdn.microsoft.com/library/windows/hardware/ff560771)
    -   [*DxgkDdiStartDevice*](https://msdn.microsoft.com/library/windows/hardware/ff560775)
    -   [*DxgkDdiStopCapture*](https://msdn.microsoft.com/library/windows/hardware/ff560776)
    -   [*DxgkDdiStopDevice*](https://msdn.microsoft.com/library/windows/hardware/ff560781)
    -   [*DxgkDdiStopDeviceAndReleasePostDisplayOwnership*](https://msdn.microsoft.com/library/windows/hardware/hh451415) (DXGKDDI\_INTERFACE\_VERSION &gt;= DXGKDDI\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiSubmitCommand*](https://msdn.microsoft.com/library/windows/hardware/ff560790)
    -   [*DxgkDdiSystemDisplayEnable*](https://msdn.microsoft.com/library/windows/hardware/hh451426) (DXGKDDI\_INTERFACE\_VERSION &gt;= DXGKDDI\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiSystemDisplayWrite*](https://msdn.microsoft.com/library/windows/hardware/hh451429) (DXGKDDI\_INTERFACE\_VERSION &gt;= DXGKDDI\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiUnload*](https://msdn.microsoft.com/library/windows/hardware/ff560801)
    -   [*DxgkDdiUpdateActiveVidPnPresentPath*](https://msdn.microsoft.com/library/windows/hardware/ff560803)
    -   [*DxgkDdiUpdateOverlay*](https://msdn.microsoft.com/library/windows/hardware/ff560804)


3.  传递*DriverObject*， *RegistryPath*，并已填充中[**驱动程序\_初始化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff556169)结构[ **DxgkInitialize**](https://msdn.microsoft.com/library/windows/hardware/ff560824)。

4.  返回由返回的值[ **DxgkInitialize**](https://msdn.microsoft.com/library/windows/hardware/ff560824)。

[**驱动程序\_初始化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff556169)结构不需要保留在之后的内存中**DriverEntry**返回。

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
<td align="left"><p>版本</p></td>
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


[**DxgkInitialize**](https://msdn.microsoft.com/library/windows/hardware/ff560824)

[*DxgkDdiUnload*](https://msdn.microsoft.com/library/windows/hardware/ff560801)

 

 






