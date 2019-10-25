---
title: 加载和卸载
description: 加载和卸载
ms.assetid: e7a4e405-5361-4217-a279-2b54a10ebce2
keywords:
- 筛选器管理器 WDK 文件系统微筛选器，加载/卸载驱动程序
- 微筛选器驱动程序 WDK，驱动程序加载
- 文件系统筛选器驱动程序 WDK，驱动程序加载
- 驱动程序加载 WDK 文件系统
- 正在加载驱动程序 WDK 文件系统
- 卸载驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 880d54a6d60d73d846e06c5a0b9306024de81aa1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841137"
---
# <a name="loading-and-unloading"></a>加载和卸载


当系统运行时，可以随时加载微筛选器驱动程序。 如果微筛选器驱动程序的[INF 文件](creating-an-inf-file-for-a-minifilter-driver.md)指定了 SERVICE\_BOOT 的驱动程序启动类型\_启动、服务\_系统\_启动或服务\_自动\_启动，则会根据现有负载加载微筛选器驱动程序文件系统筛选器驱动程序的订单组定义，以支持与旧版筛选器驱动程序的互操作性。 当系统运行时，可以通过服务启动请求（sc start、net start 或服务 Api）或通过显式加载请求（fltmc load、 [**FltLoadFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltloadfilter)或[**FilterLoad**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterload)）来加载微筛选器驱动程序。

当加载微筛选器驱动程序时，将调用微筛选器驱动程序的[DriverEntry](writing-a-driverentry-routine-for-a-minifilter-driver.md)例程，使微筛选器驱动程序可以执行将应用于微筛选器驱动程序的所有实例的初始化操作。 在其**DriverEntry**例程内，微筛选器驱动程序调用[**FltRegisterFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter)来向筛选器管理器注册回调例程[ **，并通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltstartfiltering)筛选器管理器驱动程序已准备好启动附加到卷并筛选 i/o 请求。

微筛选器驱动程序实例是在用于安装微筛选器驱动程序的[INF 文件](creating-an-inf-file-for-a-minifilter-driver.md)中定义的。 微筛选器驱动程序的 INF 文件必须定义一个默认实例，并且它可以定义其他实例。 这些定义适用于所有卷。 每个实例定义都包括实例名称、高度和标志，指示是否可以自动附加、手动或同时附加此实例。 默认实例用于定购微筛选器驱动程序，以便筛选器管理器按正确的顺序调用微筛选器驱动程序的装载和实例安装回调例程。 如果调用方未指定实例名称，则默认实例还与显式附件请求一起使用。

筛选器管理器会自动向微筛选器驱动程序发出有关可用卷的通知，方法是在装入卷后，在第一次创建操作上调用其[*InstanceSetupCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_setup_callback)例程。 当筛选器管理器在系统启动时枚举现有的卷时， [**FltStartFiltering**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltstartfiltering)返回之前，会发生这种情况。 它也可能在运行时、装入卷或显式附件请求（fltmc attach、 [**FltAttachVolume**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltattachvolume)或[**FilterAttach**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterattach)）时出现。

卸载微筛选器驱动程序时，将会断开微筛选器驱动程序实例、该实例附加到的卷正在卸除，或作为显式分离请求（fltmc 分离、 [**FltDetachVolume**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdetachvolume)或[**FilterDetach**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterdetach)）的结果。 如果微筛选器驱动程序注册[*InstanceQueryTeardownCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_query_teardown_callback)例程，则可以通过调用**FilterDetach**或**FltDetachVolume**来使显式分离请求失败。 拆卸过程如下所示：

-   如果微筛选器驱动程序注册了[*InstanceTeardownStartCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_teardown_callback)回调例程，则筛选器管理器将在拆卸过程开始时调用它。 在这种情况下，微筛选器驱动程序应完成所有挂起的操作，取消或完成其他工作，如微筛选器驱动程序生成的 i/o 请求，并停止对新工作项进行排队。

-   在实例拆卸过程中，任何当前正在执行的 preoperation 或 postoperation 回调例程将继续正常处理，正在等待 postoperation 回调的任何 i/o 请求都可以 "耗尽" 或取消，并且由微筛选器驱动程序将继续正常处理直到它们完成。

-   如果微筛选器驱动程序注册了[*InstanceTeardownCompleteCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_teardown_callback)例程，则筛选器管理器将在所有未完成的 i/o 操作完成后调用此例程。 在这种情况下，微筛选器驱动程序会关闭仍处于打开状态的任何文件。

-   释放对实例的所有未完成引用后，筛选器管理器将删除剩余的上下文，并且该实例会完全断开。

当系统运行时，可以通过服务停止请求（sc stop、net stop 或 service Api）或通过显式卸载请求（fltmc unload、 [**FltUnloadFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltunloadfilter)或[**FilterUnload**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterunload)）卸载微筛选器驱动程序。

卸载微筛选器驱动程序时，将调用微筛选器驱动程序的[*FilterUnloadCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_filter_unload_callback)例程。 此例程会关闭任何打开的通信服务器端口，调用[**FltUnregisterFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltunregisterfilter)，并执行任何所需的清理。 注册此例程是可选的。 但是，如果微筛选器驱动程序未注册*FilterUnloadCallback*例程，则无法卸载微筛选器驱动程序。 有关此例程的详细信息，请参阅[编写 FilterUnloadCallback 例程](writing-a-filterunloadcallback-routine.md)。

### <a name="span-idfilter_manager_routines_for_loading_and_unloading_minifilter_driversspanspan-idfilter_manager_routines_for_loading_and_unloading_minifilter_driversspanspan-idfilter_manager_routines_for_loading_and_unloading_minifilter_driversspanfilter-manager-routines-for-loading-and-unloading-minifilter-drivers"></a><span id="Filter_Manager_Routines_for_Loading_and_Unloading_Minifilter_Drivers"></span><span id="filter_manager_routines_for_loading_and_unloading_minifilter_drivers"></span><span id="FILTER_MANAGER_ROUTINES_FOR_LOADING_AND_UNLOADING_MINIFILTER_DRIVERS"></span>用于加载和卸载微筛选器驱动程序的筛选器管理器例程

筛选器管理器为显式加载和卸载请求提供以下支持例程，它们可从用户模式或内核模式发出：

[**FilterLoad**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterload)

[**FilterUnload**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterunload)

[**FltLoadFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltloadfilter)

[**FltUnloadFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltunloadfilter)

以下例程用于注册和取消注册实例设置和拆卸的回调例程：

[**FltRegisterFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter)

[**FltStartFiltering**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltstartfiltering)

[**FltUnregisterFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltunregisterfilter)

### <a name="span-idminifilter_driver_callback_routines_for_instance_setup__teardown__and_unloadspanspan-idminifilter_driver_callback_routines_for_instance_setup__teardown__and_unloadspanspan-idminifilter_driver_callback_routines_for_instance_setup__teardown__and_unloadspanminifilter-driver-callback-routines-for-instance-setup-teardown-and-unload"></a><span id="Minifilter_Driver_Callback_Routines_for_Instance_Setup__Teardown__and_Unload"></span><span id="minifilter_driver_callback_routines_for_instance_setup__teardown__and_unload"></span><span id="MINIFILTER_DRIVER_CALLBACK_ROUTINES_FOR_INSTANCE_SETUP__TEARDOWN__AND_UNLOAD"></span>用于实例设置、拆卸和卸载的微筛选器驱动程序回调例程

以下微筛选器驱动程序回调例程存储在作为参数传递给[**FltRegisterFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter)的[**FLT\_注册**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_registration)结构中：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">回调例程名称</th>
<th align="left">回调例程类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_setup_callback" data-raw-source="[&lt;em&gt;InstanceSetupCallback&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_setup_callback)"><em>InstanceSetupCallback</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_setup_callback" data-raw-source="[&lt;strong&gt;PFLT_INSTANCE_SETUP_CALLBACK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_setup_callback)"><strong>PFLT_INSTANCE_SETUP_CALLBACK</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_query_teardown_callback" data-raw-source="[&lt;em&gt;InstanceQueryTeardownCallback&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_query_teardown_callback)"><em>InstanceQueryTeardownCallback</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_query_teardown_callback" data-raw-source="[&lt;strong&gt;PFLT_INSTANCE_QUERY_TEARDOWN_CALLBACK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_query_teardown_callback)"><strong>PFLT_INSTANCE_QUERY_TEARDOWN_CALLBACK</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_teardown_callback" data-raw-source="[&lt;em&gt;InstanceTeardownStartCallback&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_teardown_callback)"><em>InstanceTeardownStartCallback</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_teardown_callback" data-raw-source="[&lt;strong&gt;PFLT_INSTANCE_TEARDOWN_CALLBACK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_teardown_callback)"><strong>PFLT_INSTANCE_TEARDOWN_CALLBACK</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_teardown_callback" data-raw-source="[&lt;em&gt;InstanceTeardownCompleteCallback&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_teardown_callback)"><em>InstanceTeardownCompleteCallback</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_teardown_callback" data-raw-source="[&lt;strong&gt;PFLT_INSTANCE_TEARDOWN_CALLBACK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_teardown_callback)"><strong>PFLT_INSTANCE_TEARDOWN_CALLBACK</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_filter_unload_callback" data-raw-source="[&lt;em&gt;FilterUnloadCallback&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_filter_unload_callback)"><em>FilterUnloadCallback</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_filter_unload_callback" data-raw-source="[&lt;strong&gt;PFLT_FILTER_UNLOAD_CALLBACK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_filter_unload_callback)"><strong>PFLT_FILTER_UNLOAD_CALLBACK</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 




