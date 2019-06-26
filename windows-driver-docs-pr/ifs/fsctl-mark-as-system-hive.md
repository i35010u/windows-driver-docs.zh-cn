---
title: FSCTL_MARK_AS_SYSTEM_HIVE 控制代码
description: FSCTL\_标记\_AS\_系统\_HIVE 控制代码通知文件系统指定的文件包含注册表的系统配置单元。
ms.assetid: de3cb340-2485-4bc5-bc2a-3c34cee2d6b3
keywords:
- FSCTL_MARK_AS_SYSTEM_HIVE 控制代码可安装文件系统驱动程序
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
ms.openlocfilehash: d826674ac0fdee5ffebb1ce7da70f72cb0e42061
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380129"
---
# <a name="fsctlmarkassystemhive-control-code"></a>FSCTL\_标记\_AS\_系统\_HIVE 控制代码


**FSCTL\_标记\_AS\_系统\_HIVE**控制代码通知文件系统指定的文件包含注册表的系统配置单元。 文件系统必须正好适当时刻避免死锁并确保数据完整性将系统配置单元数据刷新到磁盘。 不要与包含注册表的系统配置单元的文件之外的任何文件使用此文件系统控制代码。 此控制代码并不适用于目录或卷的句柄。 文件系统重定向程序访问远程计算机上的文件将执行任何操作视为此控制代码。

仅内核级别的组件可以使用此文件系统控制代码。

若要执行此操作，调用[ **FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)或[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)使用以下参数。

**Parameters**

<a href="" id="fileobject"></a>*FileObject*  
[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)仅。 用户文件的文件对象指针。 此参数是必需的不能**NULL**。

<a href="" id="filehandle"></a>*FileHandle*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)仅。 用户文件的句柄。 此参数是必需的不能**NULL**。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。 使用**FSCTL\_标记\_AS\_系统\_HIVE**对于此操作。

<a href="" id="inputbuffer"></a>*InputBuffer*  
不使用。 值分配**NULL**给此参数。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
不使用。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
不使用。 值分配**NULL**给此参数。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
不使用。

<a name="status-block"></a>状态块
------------

[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)或[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)将返回状态\_成功如果操作成功。 否则，相应的函数返回相应的 NTSTATUS 错误代码。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h （包括 Ntifs.h）</td>
</tr>
</tbody>
</table>

 

 





