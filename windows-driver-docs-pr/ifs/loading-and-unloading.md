---
title: 加载和卸载
description: 加载和卸载
ms.assetid: e7a4e405-5361-4217-a279-2b54a10ebce2
keywords:
- 筛选器管理器 WDK 文件系统微筛选器，加载/卸载驱动程序
- 微筛选器驱动程序 WDK，加载的驱动程序
- 文件系统微筛选器驱动程序 WDK，加载的驱动程序
- 正在加载 WDK 文件系统驱动程序
- 加载驱动程序 WDK 文件系统
- 正在卸载驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53ddf6fb60b1bd233fcab4bbbe482919bdec6b13
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324407"
---
# <a name="loading-and-unloading"></a>加载和卸载


系统运行时，可以在任何时候加载微筛选器驱动程序。 如果微筛选器驱动程序[INF 文件](creating-an-inf-file-for-a-minifilter-driver.md)指定驱动程序启动的服务类型\_引导\_开始，服务\_系统\_开始或服务\_自动\_根据文件系统筛选器驱动程序，以支持旧的筛选器驱动程序与互操作性的现有加载顺序组定义中加载开始，微筛选器驱动程序。 通过服务启动请求 （sc 开始，net start 或服务 Api），或通过显式加载请求运行系统时，可以加载微筛选器驱动程序 (fltmc 负载[ **FltLoadFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff543366)或[ **FilterLoad**](https://msdn.microsoft.com/library/windows/hardware/ff541504))。

微筛选器驱动程序[DriverEntry](writing-a-driverentry-routine-for-a-minifilter-driver.md)例程微筛选器驱动程序在加载时调用，以便微筛选器驱动程序可以执行将适用于微筛选器驱动程序的所有实例的初始化。 在其**DriverEntry**例程，微筛选器驱动程序调用[ **FltRegisterFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff544305)向筛选器管理器注册回调例程和[**FltStartFiltering** ](https://msdn.microsoft.com/library/windows/hardware/ff544569)用于通知筛选器管理器微筛选器驱动程序已准备好开始将附加到的卷和筛选输入/输出请求。

在中定义的微筛选器驱动程序实例[INF 文件](creating-an-inf-file-for-a-minifilter-driver.md)用于安装微筛选器驱动程序。 微筛选器驱动程序的 INF 文件必须定义一个默认实例，并且它可以定义其他实例。 这些定义应用跨所有卷。 每个实例定义包括实例名称、 其海拔高度，并且这些标志指示是否可以自动、 手动附加实例或两者。 到订单微筛选器驱动程序使用，默认实例，以便筛选器管理器会以正确的顺序调用微筛选器驱动程序装载和实例安装回调例程。 默认实例还用于显式附件请求时调用方不指定实例名称。

筛选器管理器会自动通知有关可用卷的微筛选器驱动程序通过调用其[ *InstanceSetupCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff551096)例程在第一天后装载卷创建操作。 这可能是之前[ **FltStartFiltering** ](https://msdn.microsoft.com/library/windows/hardware/ff544569)返回时，当筛选器管理器枚举在系统启动时的现有卷。 也可能是在运行时，已装入卷或显式附件请求的结果 (fltmc 附加[ **FltAttachVolume**](https://msdn.microsoft.com/library/windows/hardware/ff541772)，或[ **FilterAttach**](https://msdn.microsoft.com/library/windows/hardware/ff540442)).

微筛选器驱动程序实例，则将调用卸载微筛选器驱动程序时，正在卸载实例附加到该卷，或显式分离请求的结果 (fltmc 分离，请[ **FltDetachVolume**](https://msdn.microsoft.com/library/windows/hardware/ff542041)，或[ **FilterDetach**](https://msdn.microsoft.com/library/windows/hardware/ff540475))。 如果微筛选器驱动程序注册[ *InstanceQueryTeardownCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff551095)例程，它可能发生故障的显式分离请求通过调用**FilterDetach**或**FltDetachVolume**。 清除将继续，如下所示：

-   如果微筛选器驱动程序已注册[ *InstanceTeardownStartCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff551098)回调例程，筛选器管理器调用它在拆解过程开始。 在此例程中，微筛选器驱动程序应完成所有挂起的操作、 取消或完成其他工作，例如微筛选器驱动程序和停止队列的新工作项生成的 I/O 请求。

-   在实例拆卸过程任何当前正在执行的 preoperation 或 postoperation 回调例程继续正常处理、 postoperation 回调可以"排除"或已取消，等待任何 I/O 请求和生成的任何 I/O 请求微筛选器驱动程序继续正常处理，直到完成。

-   如果微筛选器驱动程序已注册[ *InstanceTeardownCompleteCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff551098)例程，筛选器管理器后，将调用此例程已完成所有未完成 I/O 操作。 在此例程中，微筛选器驱动程序将关闭仍打开任何文件。

-   别忘了发布到的实例未完成的引用、 筛选器管理器中删除剩余的上下文和实例完全被撤销。

在运行时系统，可以通过服务停止请求 （sc stop、 net stop 或服务 Api），或通过显式卸载请求卸载微筛选器驱动程序 (fltmc unload [ **FltUnloadFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff544602)，或[ **FilterUnload**](https://msdn.microsoft.com/library/windows/hardware/ff541516))。

微筛选器驱动程序[ *FilterUnloadCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff551085)卸载微筛选器驱动程序时调用例程。 此例程会关闭任何打开的通信的服务器端口，调用[ **FltUnregisterFilter**](https://msdn.microsoft.com/library/windows/hardware/ff544606)，并执行任何所需的清除。 注册此例程是可选的。 但是，如果微筛选器驱动程序不会注册*FilterUnloadCallback*例程，微筛选器驱动程序不能卸载。 有关此例程的详细信息，请参阅[编写 FilterUnloadCallback 例程](writing-a-filterunloadcallback-routine.md)。

### <a name="span-idfiltermanagerroutinesforloadingandunloadingminifilterdriversspanspan-idfiltermanagerroutinesforloadingandunloadingminifilterdriversspanspan-idfiltermanagerroutinesforloadingandunloadingminifilterdriversspanfilter-manager-routines-for-loading-and-unloading-minifilter-drivers"></a><span id="Filter_Manager_Routines_for_Loading_and_Unloading_Minifilter_Drivers"></span><span id="filter_manager_routines_for_loading_and_unloading_minifilter_drivers"></span><span id="FILTER_MANAGER_ROUTINES_FOR_LOADING_AND_UNLOADING_MINIFILTER_DRIVERS"></span>用于加载和卸载微筛选器驱动程序筛选器管理器例程

筛选器管理器提供了以下支持例程的显式加载和卸载请求，可以从用户模式或内核模式发出：

[**FilterLoad**](https://msdn.microsoft.com/library/windows/hardware/ff541504)

[**FilterUnload**](https://msdn.microsoft.com/library/windows/hardware/ff541516)

[**FltLoadFilter**](https://msdn.microsoft.com/library/windows/hardware/ff543366)

[**FltUnloadFilter**](https://msdn.microsoft.com/library/windows/hardware/ff544602)

下面的例程用于注册和注销回调例程，例如设置和清除：

[**FltRegisterFilter**](https://msdn.microsoft.com/library/windows/hardware/ff544305)

[**FltStartFiltering**](https://msdn.microsoft.com/library/windows/hardware/ff544569)

[**FltUnregisterFilter**](https://msdn.microsoft.com/library/windows/hardware/ff544606)

### <a name="span-idminifilterdrivercallbackroutinesforinstancesetupteardownandunloadspanspan-idminifilterdrivercallbackroutinesforinstancesetupteardownandunloadspanspan-idminifilterdrivercallbackroutinesforinstancesetupteardownandunloadspanminifilter-driver-callback-routines-for-instance-setup-teardown-and-unload"></a><span id="Minifilter_Driver_Callback_Routines_for_Instance_Setup__Teardown__and_Unload"></span><span id="minifilter_driver_callback_routines_for_instance_setup__teardown__and_unload"></span><span id="MINIFILTER_DRIVER_CALLBACK_ROUTINES_FOR_INSTANCE_SETUP__TEARDOWN__AND_UNLOAD"></span>微筛选器驱动程序回调例程，例如安装、 Teardown 和卸载

下面的微筛选器驱动程序回调例程都存储在[ **FLT\_注册**](https://msdn.microsoft.com/library/windows/hardware/ff544811)作为参数传递的结构[ **FltRegisterFilter**](https://msdn.microsoft.com/library/windows/hardware/ff544305):

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551096" data-raw-source="[&lt;em&gt;InstanceSetupCallback&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551096)"><em>InstanceSetupCallback</em></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551096" data-raw-source="[&lt;strong&gt;PFLT_INSTANCE_SETUP_CALLBACK&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551096)"><strong>PFLT_INSTANCE_SETUP_CALLBACK</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551095" data-raw-source="[&lt;em&gt;InstanceQueryTeardownCallback&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551095)"><em>InstanceQueryTeardownCallback</em></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551095" data-raw-source="[&lt;strong&gt;PFLT_INSTANCE_QUERY_TEARDOWN_CALLBACK&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551095)"><strong>PFLT_INSTANCE_QUERY_TEARDOWN_CALLBACK</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551098" data-raw-source="[&lt;em&gt;InstanceTeardownStartCallback&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551098)"><em>InstanceTeardownStartCallback</em></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551098" data-raw-source="[&lt;strong&gt;PFLT_INSTANCE_TEARDOWN_CALLBACK&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551098)"><strong>PFLT_INSTANCE_TEARDOWN_CALLBACK</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551098" data-raw-source="[&lt;em&gt;InstanceTeardownCompleteCallback&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551098)"><em>InstanceTeardownCompleteCallback</em></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551098" data-raw-source="[&lt;strong&gt;PFLT_INSTANCE_TEARDOWN_CALLBACK&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551098)"><strong>PFLT_INSTANCE_TEARDOWN_CALLBACK</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551085" data-raw-source="[&lt;em&gt;FilterUnloadCallback&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551085)"><em>FilterUnloadCallback</em></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551085" data-raw-source="[&lt;strong&gt;PFLT_FILTER_UNLOAD_CALLBACK&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551085)"><strong>PFLT_FILTER_UNLOAD_CALLBACK</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 




