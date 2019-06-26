---
title: 调用 FilterUnloadCallback 例程时
description: 调用 FilterUnloadCallback 例程时
ms.assetid: 22a3a73e-28be-4483-a7a6-73525e74503d
keywords:
- FilterUnloadCallback
- 非强制卸载 WDK 文件系统微筛选器
- 强制卸载 WDK 文件系统微筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 486e4fdc67301b528378a1bc63a573d3e2a21101
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385308"
---
# <a name="when-the-filterunloadcallback-routine-is-called"></a>调用 FilterUnloadCallback 例程时


## <span id="ddk_when_the_filterunloadcallback_routine_is_called_if"></span><span id="DDK_WHEN_THE_FILTERUNLOADCALLBACK_ROUTINE_IS_CALLED_IF"></span>


筛选器管理器调用微筛选器驱动程序[ **FilterUnloadCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_filter_unload_callback)例程卸载前倒带微筛选器驱动程序通过以下方式之一：

-   *非强制卸载*。 用户模式应用程序已调用时发生这种类型的卸载[ **FilterUnload** ](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterunload)或内核模式驱动程序调用[ **FltUnloadFilter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltunloadfilter). 它也会发生时您键入**fltmc unload**在命令提示符处。

-   *强制卸载*。 通过键入发出服务停止请求时，会发生这种类型的卸载**sc stop**或**net stop**在命令提示符处。 (有关详细信息**sc stop**并**net stop**命令，单击**帮助和支持**开始菜单上。)它也会发生时在用户模式应用程序调用 Microsoft Win32 **control 服务**函数，向服务传递\_控件\_停止控制代码作为*dwControl*参数。 （有关 Win32 服务功能的详细信息，请参阅 Microsoft Windows SDK 文档）。

对于非强制卸载如果微筛选器驱动程序*FilterUnloadCallback*例程将返回一个错误或警告的 NTSTATUS 值，如状态\_FLT\_不要\_不\_拆离方法，筛选器管理器不会卸载微筛选器驱动程序。

为要强制卸载，筛选器管理器卸载微筛选器驱动程序在微筛选器驱动程序的后*FilterUnloadCallback*调用例程时，即使*FilterUnloadCallback*例程返回错误或警告 NTSTATUS 值，如状态\_FLT\_不要\_不\_分离。

若要禁用强制卸载微筛选器驱动程序，微筛选器驱动程序设置 FLTFL\_注册\_不要\_不\_支持\_服务\_中的停止标志**标志**的成员[ **FLT\_注册**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_registration)微筛选器驱动程序将作为参数传递的结构[ **FltRegisterFilter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltregisterfilter)在其**DriverEntry**例程。 当设置此标志时，筛选器管理器通常会处理非强制卸载请求。 但是，强制卸载请求将失败。 筛选器管理器不会调用微筛选器驱动程序*FilterUnloadCallback*例程失败的卸载请求。

请注意，如果微筛选器驱动程序**DriverEntry**例程将返回警告或错误 NTSTATUS 值*FilterUnloadCallback*不调用例程; 筛选器管理器只需卸载微筛选器驱动程序。

*FilterUnloadCallback*例程不在系统关闭时调用。 必须执行关闭处理微筛选器驱动程序应注册 IRP preoperation 回调例程\_MJ\_关闭操作。

 

 




