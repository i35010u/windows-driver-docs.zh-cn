---
title: 打开文件的句柄
description: 打开文件的句柄
ms.assetid: 9378282a-ee29-44b6-b206-602eee94ec3b
keywords:
- 文件 WDK 内核
- 文件对象 WDK 内核
- WDK 文件对象的对象
- 文件句柄 WDK 内核
- 文件 WDK 内核的句柄
- 打开文件句柄
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a802bf10a78f6935d9cdb6196a2655ab2ccbaa2
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57348676"
---
# <a name="opening-a-handle-to-a-file"></a>打开文件的句柄





若要打开文件的句柄，请执行以下步骤：

1.  创建[**对象\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff557749)结构，并调用[ **InitializeObjectAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff547804)宏来初始化结构。 指定文件的对象同名*ObjectName*参数**InitializeObjectAttributes**。

2.  表示通过打开文件的句柄**对象\_特性**结构[ **IoCreateFile**](https://msdn.microsoft.com/library/windows/hardware/ff548418)， [ **zwcreatefile 转换** ](https://msdn.microsoft.com/library/windows/hardware/ff566424)，或[ **ZwOpenFile**](https://msdn.microsoft.com/library/windows/hardware/ff567011)。

    如果该文件不存在， **IoCreateFile**并**ZwCreateFile**将创建它，而**ZwOpenFile**将返回状态\_对象\_名称\_不\_找到。

请注意，驱动程序几乎总是使用**ZwCreateFile**或**ZwOpenFile**而非**IoCreateFile**。

当您调用**IoCreateFile**， **ZwCreateFile**，或**ZwOpenFile**，Windows 高级管理人员创建一个新的文件对象来表示该文件，还可以提供的打开句柄对象。 关闭所有打开的句柄它之前，一直保留此文件对象。

无论您调用的例程必须传递所需的访问权限*DesiredAccess*参数。 这些权限必须包括您的驱动程序将执行的所有操作。 下表列出了这些操作，并相应访问权限请求。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>操作</th>
<th>所需的访问权限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>从文件中读取。</p></td>
<td><p>FILE_READ_DATA 或 GENERIC_READ</p></td>
</tr>
<tr class="even">
<td><p>写入到文件。</p></td>
<td><p>FILE_WRITE_DATA 或 GENERIC_WRITE</p></td>
</tr>
<tr class="odd">
<td><p>仅写入文件的末尾。</p></td>
<td><p>FILE_APPEND_DATA</p></td>
</tr>
<tr class="even">
<td><p>读取文件的元数据，例如文件的创建时间。</p></td>
<td><p>FILE_READ_ATTRIBUTES 或 GENERIC_READ</p></td>
</tr>
<tr class="odd">
<td><p>写入文件的元数据，例如文件的创建时间。</p></td>
<td><p>FILE_WRITE_ATTRIBUTES 或 GENERIC_WRITE</p></td>
</tr>
</tbody>
</table>

 

详细了解可用的值*DesiredAccess*，请参阅[ **ZwCreateFile**](https://msdn.microsoft.com/library/windows/hardware/ff566424)。

 

 




