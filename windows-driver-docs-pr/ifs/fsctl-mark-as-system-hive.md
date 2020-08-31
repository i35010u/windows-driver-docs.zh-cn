---
title: FSCTL_MARK_AS_SYSTEM_HIVE 控制代码
description: FSCTL \_ 标记 \_ 为 \_ 系统 \_ HIVE 控制代码通知文件系统指定的文件包含注册表的系统配置单元。
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
ms.openlocfilehash: 1bc0a6df34002f55cca6dabcb96feaab790fc74d
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067004"
---
# <a name="fsctl_mark_as_system_hive-control-code"></a>FSCTL \_ 标记 \_ 为 \_ 系统 \_ HIVE 控制代码


**FSCTL \_ 标记 \_ 为 \_ 系统 \_ HIVE**控制代码通知文件系统指定的文件包含注册表的系统配置单元。 文件系统必须在适当的时间将系统 hive 数据刷新到磁盘，以避免死锁并确保数据完整性。 不要将此文件系统控制代码与包含注册表系统配置单元的文件之外的任何文件一起使用。 此控制代码不适用于目录或卷句柄。 访问远程计算机上的文件的文件系统重定向程序将此控制代码视为无操作。

只有内核级组件可以使用此 filesystem 控制代码。

若要执行此操作，请调用具有以下参数的 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 或 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 。

**参数**

<a href="" id="fileobject"></a>*FileObject*  
仅[**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 用户文件的文件对象指针。 此参数是必需的，不能为 **NULL**。

<a href="" id="filehandle"></a>*FileHandle*  
仅[**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 。 用户文件的句柄。 此参数是必需的，不能为 **NULL**。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。 使用 **FSCTL \_ 标记作为此操作的 \_ \_ 系统 \_ 配置单元** 。

<a href="" id="inputbuffer"></a>*InputBuffer*  
未使用。 为此参数分配 **NULL** 值。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
未使用。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
未使用。 为此参数分配 **NULL** 值。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
未使用。

<a name="status-block"></a>状态块
------------

如果操作成功，则[**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)或[**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85))返回状态 \_ SUCCESS。 否则，相应的函数将返回相应的 NTSTATUS 错误代码。

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
<td align="left">Ntifs (包含 Ntifs) </td>
</tr>
</tbody>
</table>

 

