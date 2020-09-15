---
title: 打开文件的句柄
description: 打开文件的句柄
ms.assetid: 9378282a-ee29-44b6-b206-602eee94ec3b
keywords:
- 文件 WDK 内核
- 文件对象 WDK 内核
- 对象 WDK 文件对象
- 文件处理 WDK 内核
- 文件 WDK 内核的句柄
- 正在打开文件的句柄
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13e64a5d536f43b7bbac72e4c42cb4c82c32309f
ms.sourcegitcommit: a5f76805387760730faed5674d87201ec85b7dd3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90112100"
---
# <a name="opening-a-handle-to-a-file"></a>打开文件的句柄





若要打开文件的句柄，请执行以下步骤：

1.  创建 [**对象 \_ 属性**](/windows/win32/api/ntdef/ns-ntdef-_object_attributes) 结构，并调用 [**InitializeObjectAttributes**](/windows/win32/api/ntdef/nf-ntdef-initializeobjectattributes) 宏来初始化该结构。 将文件的对象名称指定为**InitializeObjectAttributes**的*ObjectName*参数。

2.  通过将 **对象 \_ 特性** 结构传递到 [**IoCreateFile**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatefile)、 [**ZwCreateFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)或 [**ZwOpenFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntopenfile)，打开文件的句柄。

    如果该文件不存在，则 **IoCreateFile** 和 **ZwCreateFile** 将创建该文件，而 **ZwOpenFile** 将返回 \_ " \_ \_ 找不到状态对象名称" \_ 。

请注意，驱动程序几乎始终使用 **ZwCreateFile** 或 **ZwOpenFile** ，而不是 **IoCreateFile**。

调用 **IoCreateFile**、 **ZwCreateFile**或 **ZwOpenFile**时，Windows executive 会创建一个新的文件对象来表示文件，并为对象提供一个打开的句柄。 此文件对象会一直保留，直到关闭所有打开的句柄。

无论你调用哪个例程，你都必须将所需的访问权限作为 *DesiredAccess* 参数进行传递。 这些权限必须涵盖驱动程序将执行的所有操作。 下表列出了这些操作以及要请求的相应访问权限。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>操作</th>
<th>必需的访问权限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>从文件中读取。</p></td>
<td><p>FILE_READ_DATA 或 GENERIC_READ</p></td>
</tr>
<tr class="even">
<td><p>写入文件。</p></td>
<td><p>FILE_WRITE_DATA 或 GENERIC_WRITE</p></td>
</tr>
<tr class="odd">
<td><p>仅写入文件结尾。</p></td>
<td><p>FILE_APPEND_DATA</p></td>
</tr>
<tr class="even">
<td><p>读取文件的元数据，如文件的创建时间。</p></td>
<td><p>FILE_READ_ATTRIBUTES 或 GENERIC_READ</p></td>
</tr>
<tr class="odd">
<td><p>写入文件的元数据，如文件的创建时间。</p></td>
<td><p>FILE_WRITE_ATTRIBUTES 或 GENERIC_WRITE</p></td>
</tr>
</tbody>
</table>

 

有关 *DesiredAccess*的可用值的详细信息，请参阅 [**ZwCreateFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)。

 

