---
title: Bug 检查 0x103 MUP_FILE_SYSTEM
description: MUP_FILE_SYSTEM bug 检查具有 0x00000103 值。
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
ms.openlocfilehash: 401323a98dc77ae35c925ab56f031ea24f7904af
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59902921"
---
# <a name="bug-check-0x103-mupfilesystem"></a>Bug 检查 0x103：MUP\_文件\_系统


MUP\_文件\_检查系统错误的值为 0x00000103。 此 bug 检查指示多个 UNC provider (MUP) 遇到了无效或意外数据。 因此，MUP 无法通道对网络重定向器，通用命名约定 (UNC) 提供程序的远程文件系统请求。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="mupfilesystem-parameters"></a>MUP\_文件\_系统参数


参数 1 标识冲突的类型。

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
<th align="left">参数 2</th>
<th align="left">参数 3</th>
<th align="left">参数 4</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>挂起的 IRP 的地址。</p></td>
<td align="left"><p>找不到文件上下文中的文件对象的地址。</p></td>
<td align="left"><p>设备对象的地址。</p></td>
<td align="left"><p>MUP 找不到对应于文件对象的文件上下文。 这通常表示 MUP 都会看到 MUP 没有看到相应 IRP_MJ_CREATE 请求的文件对象的 I/O 请求。 检查此错误的可能原因是筛选器驱动程序错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>预期的文件上下文的地址。</p></td>
<td align="left"><p>实际的文件对象中检索到的地址。</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>文件上下文已知存在的文件对象，但却不预期 (例如，可能<strong>NULL</strong>)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3</p></td>
<td align="left"><p>IRP 上下文的地址。</p></td>
<td align="left"><p>IRP 完成状态代码。</p></td>
<td align="left"><p>完成 IRP 的 UNC 提供程序的驱动程序对象 (可能是<strong>NULL</strong>)。</p></td>
<td align="left"><p>IRP 完成状态已发生错误或无效。</p>
<p>仅当使用的检查生成的 Windows 并仅应由文件系统筛选器驱动程序的附加到旧的网络重定向程序导致时，会出现此 bug 检查。 使用旧版重定向程序<strong>FsRtlRegisterUncProvider</strong> MUP 向注册。 此 bug 检查检测到返回不在 IRP_MJ_CLEANUP 或 IRP_MJ_CLOSE 请求 STATUS_SUCCESS NTSTATUS 的筛选器驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x4</p></td>
<td align="left"><p>IRP 的地址</p></td>
<td align="left"><p>文件对象的地址</p></td>
<td align="left"><p>文件对象的文件上下文</p></td>
<td align="left"><p>完成文件对象的创建请求之前对文件对象启动 I/O 操作。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

MUP 维护它处理的所有文件对象的每个文件对象基础的上下文信息。

 

 




