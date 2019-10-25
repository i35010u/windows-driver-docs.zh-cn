---
title: 使用文件句柄
description: 使用文件句柄
ms.assetid: f5a4d3f6-b74f-411e-9fa9-a41d83152fd7
keywords:
- 文件 WDK 内核
- 文件对象 WDK 内核
- 对象 WDK 文件对象
- 文件处理 WDK 内核
- 文件 WDK 内核的句柄
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cfddc7ec8ab6985db575b397a7a9ac5d95085756
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836056"
---
# <a name="using-a-file-handle"></a>使用文件句柄





下表列出了驱动程序可以对文件句柄执行的操作，以及执行这些操作的相应例程。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>操作</th>
<th>要调用的例程</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>从文件中读取数据。</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntreadfile" data-raw-source="[&lt;strong&gt;ZwReadFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntreadfile)"><strong>ZwReadFile</strong></a></p></td>
</tr>
<tr class="even">
<td><p>将数据写入文件。</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntwritefile" data-raw-source="[&lt;strong&gt;ZwWriteFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntwritefile)"><strong>ZwWriteFile</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>读取文件或文件句柄的元数据。</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile" data-raw-source="[&lt;strong&gt;ZwQueryInformationFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile)"><strong>ZwQueryInformationFile</strong></a></p></td>
</tr>
<tr class="even">
<td><p>为文件或文件句柄写入元数据。</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntsetinformationfile" data-raw-source="[&lt;strong&gt;ZwSetInformationFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntsetinformationfile)"><strong>ZwSetInformationFile</strong></a></p></td>
</tr>
</tbody>
</table>

 

若要指示文件中开始读取或写入数据的位置，请将*ByteOffset*参数分别传递到**ZwReadFile**或**ZwWriteFile**。

如果使用文件打开了句柄\_追加\_的数据访问，则所有数据都将写入文件的末尾，并且*ByteOffset*参数将被忽略。

在某些情况下，i/o 管理器会为该文件保留当前文件位置指针。 可以通过为*ByteOffset*指定**NULL**来在该位置开始读取或写入操作。 有关当前文件位置指针何时存在的详细信息，请参阅本部分后面[的使用当前文件位置](using-the-current-file-position.md)。

若要检查或更改有关文件的信息，请分别调用[**ZwQueryInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile)或[**ZwSetInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntsetinformationfile)。 指定特定类型的信息作为每个例程的*FileInformationClass*参数。 例如，通过将*FileInformationClass*设置为**FileBasicInformation** ，可以检查或更改[ **\_基本\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_basic_information)结构的文件，其中包含文件创建时间和上一次访问的成员时间等。 有关*FileInformationClass*的所有可能值的信息，请参阅[ **\_类的文件\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_file_information_class)。

 

 




