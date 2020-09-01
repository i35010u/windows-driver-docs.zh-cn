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
ms.openlocfilehash: e7e1a9a4b685bb55060337d1b85e37f0bb395077
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064948"
---
# <a name="when-the-filterunloadcallback-routine-is-called"></a>调用 FilterUnloadCallback 例程时


## <span id="ddk_when_the_filterunloadcallback_routine_is_called_if"></span><span id="DDK_WHEN_THE_FILTERUNLOADCALLBACK_ROUTINE_IS_CALLED_IF"></span>


在卸载微筛选器驱动程序之前，筛选器管理器会调用微筛选器驱动程序的 [**FilterUnloadCallback**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_filter_unload_callback) 例程，方法如下：

-   *非强制卸载*。 当用户模式应用程序调用 [**FilterUnload**](/windows/desktop/api/fltuser/nf-fltuser-filterunload) 或内核模式驱动程序调用 [**FltUnloadFilter**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltunloadfilter)时，会发生这种类型的卸载。 在命令提示符下键入 **fltmc unload** 也会出现这种情况。

-   *强制卸载*。 当你在命令提示符下键入 **sc stop** 或 **net stop** 发出服务停止请求时，将发生这种类型的卸载。  (有关 **sc stop** 和 **net stop** 命令的详细信息，请单击 "开始" 菜单上的 " **帮助和支持** "。如果用户模式应用程序调用 Microsoft WIN32 **control 服务** 函数，并且将服务 \_ 控制 \_ 停止控制代码作为 *dwControl* 参数传递，也会发生这种情况 ) 。  (有关 Win32 服务功能的详细信息，请参阅 Microsoft Windows SDK 文档。 ) 

对于非强制卸载，如果微筛选器驱动程序的 *FilterUnloadCallback* 例程返回错误或警告 NTSTATUS 值（如 STATUS FLT 不 \_ \_ \_ \_ 分离），筛选器管理器不会卸载微筛选器驱动程序。

对于必需的卸载，筛选器管理器会在调用微筛选器驱动程序的 *FilterUnloadCallback* 例程后卸载微筛选器驱动程序，即使 *FilterUnloadCallback* 例程返回错误或警告 NTSTATUS 值（如 STATUS FLT 不 \_ 分离） \_ \_ \_ 。

若要禁用微筛选器驱动程序的强制卸载，微筛选器驱动程序 \_ \_ \_ 会 \_ \_ \_ 在[**FLT \_ 注册**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_registration)结构的**Flags**成员中设置 FLTFL 注册，不支持服务停止标志。 [**FltRegisterFilter**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter) **DriverEntry** 设置此标志后，筛选器管理器通常会处理非强制卸载请求。 但是，必需的 unload 请求将会失败。 筛选器管理器不会为失败的卸载请求调用微筛选器驱动程序的 *FilterUnloadCallback* 例程。

请注意，如果微筛选器驱动程序的 **DriverEntry** 例程返回一个警告或错误 NTSTATUS 值，则不会调用 *FilterUnloadCallback* 例程;筛选器管理器只需卸载微筛选器驱动程序。

系统关闭时不会调用 *FilterUnloadCallback* 例程。 必须执行关闭处理的微筛选器驱动程序应为 IRP \_ MJ 关闭操作注册一个 preoperation 回调例程 \_ 。

 

