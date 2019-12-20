---
title: Bug 检查 0x103 MUP_FILE_SYSTEM
description: MUP_FILE_SYSTEM bug 检查的值为0x00000103。
ms.assetid: 2756bdcc-5b10-481e-99ec-17b00c4f459d
keywords:
- Bug 检查 0x103 MUP_FILE_SYSTEM
- MUP_FILE_SYSTEM
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- MUP_FILE_SYSTEM
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9b1661c8512d0a99b59a1a110a77f1611462de9d
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209095"
---
# <a name="bug-check-0x103-mup_file_system"></a>Bug 检查0x103： MUP\_文件\_系统


MUP\_文件\_系统 bug 检查的值为0x00000103。 此 bug 检查表明多 UNC 提供程序（MUP）遇到无效或意外的数据。 因此，MUP 无法向网络重定向程序（通用命名约定（UNC）提供程序）发出远程文件系统请求通道。

> [!IMPORTANT]
> 本主题面向程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。


## <a name="mup_file_system-parameters"></a>MUP\_文件\_系统参数


参数1标识冲突类型。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 1</th>
<th align="left">参数2</th>
<th align="left">参数3</th>
<th align="left">参数4</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>挂起 IRP 的地址。</p></td>
<td align="left"><p>找不到其文件上下文的文件对象的地址。</p></td>
<td align="left"><p>设备对象的地址。</p></td>
<td align="left"><p>MUP 找不到对应于文件对象的文件上下文。 这通常表示 MUP 正在查看某个文件对象的 i/o 请求，而 MUP 没有看到对应的 IRP_MJ_CREATE 请求。 此错误检查的可能原因是筛选器驱动程序错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>预期文件上下文的地址。</p></td>
<td align="left"><p>实际从 file 对象检索到的地址。</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>知道文件对象存在文件上下文，但这不是预期的（例如，它可能为<strong>NULL</strong>）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3</p></td>
<td align="left"><p>IRP 上下文的地址。</p></td>
<td align="left"><p>IRP 完成状态代码。</p></td>
<td align="left"><p>完成 IRP 的 UNC 提供程序的驱动程序对象（可能为<strong>NULL</strong>）。</p></td>
<td align="left"><p>IRP 完成状态为意外或无效。</p>
<p>仅当您使用的是 Windows 的已检查版本时，才会发生此错误检查，而只应由附加到旧网络重定向器的文件系统筛选器驱动程序引起。 在 Windows 10 版本1803之前，已检查的生成在 windows 的早期版本上可用。 旧版重定向器使用<strong>FsRtlRegisterUncProvider</strong>注册 MUP。 此 bug 检查检测返回在 IRP_MJ_CLEANUP 或 IRP_MJ_CLOSE 请求中未 STATUS_SUCCESS 的 NTSTATUS 的筛选器驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x4</p></td>
<td align="left"><p>IRP 的地址</p></td>
<td align="left"><p>File 对象的地址</p></td>
<td align="left"><p>文件对象的文件上下文</p></td>
<td align="left"><p>在对文件对象的 create 请求完成之前，对该文件对象启动了 i/o 操作。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

MUP 为其处理的所有文件对象维护每个文件对象的上下文信息。

 

 




