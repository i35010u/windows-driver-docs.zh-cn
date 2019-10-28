---
title: FSCTL_MARK_AS_SYSTEM_HIVE 控制代码
description: FSCTL\_将\_标记为\_系统\_HIVE 控制代码通知文件系统指定的文件包含注册表的系统配置单元。
ms.assetid: de3cb340-2485-4bc5-bc2a-3c34cee2d6b3
keywords:
- FSCTL_MARK_AS_SYSTEM_HIVE 控制代码可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_MARK_AS_SYSTEM_HIVE
api_location:
- Ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee10cec4463f52afd6cf0dbb4c50f32b86242882
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841287"
---
# <a name="fsctl_mark_as_system_hive-control-code"></a>FSCTL\_将\_标记为\_系统\_HIVE 控制代码


**FSCTL\_将\_标记为\_系统\_HIVE**控制代码通知文件系统指定的文件包含注册表的系统配置单元。 文件系统必须在适当的时间将系统 hive 数据刷新到磁盘，以避免死锁并确保数据完整性。 不要将此文件系统控制代码与包含注册表系统配置单元的文件之外的任何文件一起使用。 此控制代码不适用于目录或卷句柄。 访问远程计算机上的文件的文件系统重定向程序将此控制代码视为无操作。

只有内核级组件可以使用此 filesystem 控制代码。

若要执行此操作，请调用具有以下参数的[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)或[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462) 。

**参数**

<a href="" id="fileobject"></a>*FileObject*  
仅[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 用户文件的文件对象指针。 此参数是必需的，不能为**NULL**。

<a href="" id="filehandle"></a>*FileHandle*  
仅[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462) 。 用户文件的句柄。 此参数是必需的，不能为**NULL**。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。 使用**FSCTL\_标记\_作为此操作的\_系统\_HIVE** 。

<a href="" id="inputbuffer"></a>*InputBuffer*  
不使用。 为此参数分配**NULL**值。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
不使用。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
不使用。 为此参数分配**NULL**值。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
不使用。

<a name="status-block"></a>状态块
------------

如果操作成功，则[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)或[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)返回状态\_成功。 否则，相应的函数将返回相应的 NTSTATUS 错误代码。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ntifs （包括 Ntifs）</td>
</tr>
</tbody>
</table>

 

 





