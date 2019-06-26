---
title: IRP_MJ_LOCK_CONTROL
description: IRP\_MJ\_锁\_控件
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
ms.openlocfilehash: a3faf9fcb0c11f053cacd3f6ef87a4b6393d5d64
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384824"
---
# <a name="irpmjlockcontrol"></a>IRP\_MJ\_锁\_控件


## <a name="when-sent"></a>发送时间


IRP\_MJ\_锁\_控制请求发送的 I/O 管理器和其他操作系统组件，以及其他内核模式驱动程序。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


文件系统驱动程序应提取和解码以确定目标设备对象是否为文件系统控制设备对象的文件对象。 如果这种情况，文件系统驱动程序应完成根据 IRP，而无需处理锁定请求。

否则为如果请求已发出上表示用户文件的句柄打开时，文件系统驱动程序应执行次要函数代码所指示的操作和完成 IRP。 如果没有，该驱动程序应失败 IRP。

以下是有效的次要函数代码：

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
<td align="left"><p>指示字节范围锁请求，可能是代表用户模式应用程序的已调用 Microsoft Win32<strong>锁定文件</strong>函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_UNLOCK_ALL</p></td>
<td align="left"><p>指示要释放的文件的所有字节范围锁的请求通常是因为正在关闭的最后一个未完成句柄的文件对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_UNLOCK_ALL_BY_KEY</p></td>
<td align="left"><p>指示发布具有指定键值的所有字节范围锁的请求。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_UNLOCK_SINGLE</p></td>
<td align="left"><p>指示请求发布一个单一的字节范围锁定，可能是代表用户模式应用程序的已调用 Microsoft Win32 <strong>UnlockFile</strong>函数。</p></td>
</tr>
</tbody>
</table>

 

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


文件系统筛选器驱动程序应执行任何所需的处理后将向下一步低驱动程序 IRP 传递到堆栈上。

## <a name="parameters"></a>Parameters


文件系统或筛选器驱动程序调用[ **IoGetCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)与给定 IRP，若要获取一个指向其自己[**堆栈位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)中，在以下列表中所示*IrpSp*。 (显示为 IRP *Irp*。)该驱动程序可以使用以下成员的 IRP 和中处理锁定控件请求的 IRP 堆栈位置中设置的信息：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象指针。

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*  
指向[ **IO\_状态\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)接收最终完成状态以及有关请求的操作信息的结构。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
与之关联的文件对象的指针*DeviceObject*。

*IrpSp-&gt;的文件对象*参数包含一个指向**RelatedFileObject**字段中，这也是一个文件\_对象结构。 **RelatedFileObject**字段的文件\_对象结构不是有效的 IRP 处理期间\_MJ\_锁\_控件，不应使用。

<a href="" id="irpsp--flags"></a>*IrpSp-&gt;Flags*  
一个或多个以下：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Flag</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>SL_EXCLUSIVE_LOCK</p></td>
<td align="left"><p>如果设置此标志，请求的独占字节范围锁。 否则，请求共享的锁。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SL_FAIL_IMMEDIATELY</p></td>
<td align="left"><p>如果设置此标志，锁请求失败，如果无法立即批准。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
指定 IRP\_MJ\_锁\_控件。

<a href="" id="irpsp--minorfunction"></a>*IrpSp-&gt;MinorFunction*  
指定以下值之一：

-   IRP\_MN\_锁
-   IRP\_MN\_解锁\_所有
-   IRP\_MN\_解锁\_所有\_BY\_密钥
-   IRP\_MN\_解锁\_单一

<a href="" id="irpsp--parameters-lockcontrol-byteoffset"></a>*IrpSp-&gt;Parameters.LockControl.ByteOffset*  
从开始的字节范围锁定或解锁在文件中的字节偏移量。

<a href="" id="irpsp--parameters-lockcontrol-key"></a>*IrpSp-&gt;Parameters.LockControl.Key*  
字节范围锁定的密钥。

<a href="" id="irpsp--parameters-lockcontrol-length"></a>*IrpSp-&gt;Parameters.LockControl.Length*  
长度 （字节），才能锁定或解锁的字节范围。

## <a name="see-also"></a>请参阅


[**FltProcessFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltprocessfilelock)

[**FsRtlProcessFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlprocessfilelock)

[**IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)

[**IO\_状态\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_irp)

 

 






