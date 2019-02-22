---
title: 使用文件句柄
description: 使用文件句柄
ms.assetid: f5a4d3f6-b74f-411e-9fa9-a41d83152fd7
keywords:
- 文件 WDK 内核
- 文件对象 WDK 内核
- WDK 文件对象的对象
- 文件句柄 WDK 内核
- 文件 WDK 内核的句柄
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6898283ebcacc5c43631a0c6887ef396326c1a3c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525057"
---
# <a name="using-a-file-handle"></a>使用文件句柄





下表列出了驱动程序可以对文件句柄和执行这些操作的相应例程执行的操作。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>操作</th>
<th>若要调用的例程</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>从文件中读取数据。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567072" data-raw-source="[&lt;strong&gt;ZwReadFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567072)"><strong>ZwReadFile</strong></a></p></td>
</tr>
<tr class="even">
<td><p>向文件写入数据。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567121" data-raw-source="[&lt;strong&gt;ZwWriteFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567121)"><strong>ZwWriteFile</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>读取元数据的文件或文件句柄。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567052" data-raw-source="[&lt;strong&gt;ZwQueryInformationFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567052)"><strong>ZwQueryInformationFile</strong></a></p></td>
</tr>
<tr class="even">
<td><p>写入文件或文件句柄的元数据。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567096" data-raw-source="[&lt;strong&gt;ZwSetInformationFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567096)"><strong>ZwSetInformationFile</strong></a></p></td>
</tr>
</tbody>
</table>

 

若要指示在文件中开始读取或写入数据，传递*ByteOffset*参数**ZwReadFile**或**ZwWriteFile**分别。

如果使用文件打开句柄\_追加\_数据访问的所有数据都写入到文件的末尾，并*ByteOffset*参数将被忽略。

某些情况下，I/O 管理器维护的文件的当前文件位置指针。 您可以开始读取或写入该位置处的操作通过指定**NULL**有关*ByteOffset*。 当前文件位置指针存在时的详细信息，请参阅[使用当前的文件位置](using-the-current-file-position.md)在本部分中更高版本。

若要检查或更改文件有关的信息，请调用[ **ZwQueryInformationFile** ](https://msdn.microsoft.com/library/windows/hardware/ff567052)或[ **ZwSetInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567096)分别。 指定特定类型的信息作为*FileInformationClass*的每个例程的参数。 例如，设置*FileInformationClass*到**FileBasicInformation**可以检查或更改[**文件\_BASIC\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff545762)结构，其中包含的文件创建时间和上次访问时间，以及其他成员。 有关的所有可能值的信息*FileInformationClass*，请参阅[**文件\_信息\_类**](https://msdn.microsoft.com/library/windows/hardware/ff728840)。

 

 




