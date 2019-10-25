---
title: IRP_MJ_LOCK_CONTROL
description: IRP\_MJ\_锁定\_控件
ms.assetid: db21d779-c423-42bd-a94b-4d8c8fd1f7cb
keywords:
- IRP_MJ_LOCK_CONTROL 可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- IRP_MJ_LOCK_CONTROL
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ca722f75691d1c2092e5b6d34831b09864d607d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841191"
---
# <a name="irp_mj_lock_control"></a>IRP\_MJ\_锁定\_控件


## <a name="when-sent"></a>发送时间


IRP\_MJ\_锁定\_控制请求由 i/o 管理器和其他操作系统组件以及其他内核模式驱动程序发送。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


文件系统驱动程序应提取并解码文件对象，以确定目标设备对象是否为文件系统的控制设备对象。 如果是这种情况，则文件系统驱动程序应适当地完成 IRP，而不处理锁请求。

否则，如果在表示用户文件打开的句柄上发出了请求，则文件系统驱动程序应执行次要函数代码指示的操作并完成 IRP。 否则，该驱动程序应该会使 IRP 失败。

下面是有效的次要函数代码：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">代码</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>IRP_MN_LOCK</p></td>
<td align="left"><p>指示一个字节范围锁请求，可能代表已调用 Microsoft Win32 <strong>LockFile</strong>函数的用户模式应用程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_UNLOCK_ALL</p></td>
<td align="left"><p>指示释放某个文件的所有字节范围锁的请求，通常是因为正在关闭文件对象的最后一个未完成的句柄。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_UNLOCK_ALL_BY_KEY</p></td>
<td align="left"><p>指示请求释放具有指定键值的所有字节范围锁。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_UNLOCK_SINGLE</p></td>
<td align="left"><p>指示发出单个字节范围锁的请求，可能代表已调用 Microsoft Win32 <strong>UnlockFile</strong>函数的用户模式应用程序。</p></td>
</tr>
</tbody>
</table>

 

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


执行任何所需的处理后，文件系统筛选器驱动程序应将 IRP 向下传递到堆栈中的下一个较低的驱动程序。

## <a name="parameters"></a>参数


文件系统或筛选器驱动程序与给定的 IRP 一起调用[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) ，以获取指向其自己的*IrpSp*[**堆栈位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)的指针，如以下列表所示。 （IRP 显示为*irp*。）驱动程序可以使用 IRP 的下列成员中设置的信息，并使用 IRP 堆栈位置来处理锁定控制请求：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象的指针。

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*  
指向[**IO\_状态的指针\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)结构，它接收最终完成状态和有关请求的操作的信息。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
指向与*DeviceObject*关联的文件对象的指针。

*&gt;IrpSp FileObject*参数包含指向**RelatedFileObject**字段的指针，该字段也是文件\_对象结构。 文件\_对象结构的**RelatedFileObject**字段在处理 IRP\_MJ\_锁定\_控件期间无效，不应使用。

<a href="" id="irpsp--flags"></a>*IrpSp-&gt;标志*  
以下一项或多项操作：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">旗帜</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>SL_EXCLUSIVE_LOCK</p></td>
<td align="left"><p>如果设置此标志，则请求独占字节范围锁。 否则，请求共享锁。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SL_FAIL_IMMEDIATELY</p></td>
<td align="left"><p>如果设置了此标志，则锁定请求应失败（如果不能立即授予）。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
指定 IRP\_MJ\_锁定\_控件。

<a href="" id="irpsp--minorfunction"></a>*IrpSp-&gt;MinorFunction*  
指定以下项之一：

-   IRP\_MN\_锁定
-   IRP\_MN\_解锁\_
-   IRP\_MN\_通过\_密钥\_所有\_进行解锁
-   IRP\_MN\_解锁\_单一

<a href="" id="irpsp--parameters-lockcontrol-byteoffset"></a>*IrpSp-&gt;参数. LockControl. ByteOffset*  
要锁定或解锁的字节范围内的文件中的起始字节偏移量。

<a href="" id="irpsp--parameters-lockcontrol-key"></a>*IrpSp-&gt;LockControl。*  
字节范围锁的键。

<a href="" id="irpsp--parameters-lockcontrol-length"></a>*IrpSp-&gt;参数. LockControl. 长度*  
要锁定或解锁的字节范围的长度（以字节为单位）。

## <a name="see-also"></a>另请参阅


[**FltProcessFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltprocessfilelock)

[**FsRtlProcessFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlprocessfilelock)

[**IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO\_状态\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

 

 






