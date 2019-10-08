---
title: 指定访问权限
description: 指定访问权限
ms.assetid: 8ef4b4bb-5f4e-4095-b4ab-1182c0f75619
ms.localizationpriority: High
ms.date: 10/17/2018
ms.openlocfilehash: 1371cff860e97ddca0d116d3cc055a7c33fed65c
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007641"
---
# <a name="specifying-access-rights"></a>指定访问权限


ACCESS @ no__t-0MASK 类型是一个位掩码，用于在[访问控制项](https://docs.microsoft.com/windows-hardware/drivers/ifs/access-control-entry)的[访问掩码](https://docs.microsoft.com/windows-hardware/drivers/ifs/access-mask)中指定一组访问权限。

``` syntax
typedef ULONG  ACCESS_MASK;
```

以下标准特定访问权限适用于所有类型的执行对象。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Flag</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DELETE</p></td>
<td><p>调用方可以删除对象。</p></td>
</tr>
<tr class="even">
<td><p>READ_CONTROL</p></td>
<td><p>调用方可以读取文件的访问控制列表（ACL）和所有权信息。</p></td>
</tr>
<tr class="odd">
<td><p>同步</p></td>
<td><p>调用方可以对对象执行等待操作。 （例如，可以将对象传递到<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitformultipleobjects" data-raw-source="[&lt;strong&gt;KeWaitForMultipleObjects&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitformultipleobjects)"><strong>KeWaitForMultipleObjects</strong></a>。）</p></td>
</tr>
<tr class="even">
<td><p>WRITE_DAC</p></td>
<td><p>调用方可以更改对象的自由访问控制列表（DACL）信息。</p></td>
</tr>
<tr class="odd">
<td><p>WRITE_OWNER</p></td>
<td><p>调用方可以更改文件的所有权信息。</p></td>
</tr>
</tbody>
</table>

 

请注意，通常只对驱动程序编写者感兴趣。

你还可以指定以下一般访问权限。 它们也适用于所有类型的执行对象。 每个一般访问权限的含义特定于该类型的对象。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Flag</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>GENERIC_READ</p></td>
<td><p>调用方可以对对象执行正常的读取操作。</p></td>
</tr>
<tr class="even">
<td><p>GENERIC_WRITE</p></td>
<td><p>调用方可以对对象执行常规写入操作。</p></td>
</tr>
<tr class="odd">
<td><p>GENERIC_EXECUTE</p></td>
<td><p>调用方可以执行对象。 （请注意，这通常仅对某些类型的对象（如文件对象和部分对象）有效。）</p></td>
</tr>
<tr class="even">
<td><p>GENERIC_ALL</p></td>
<td><p>调用方可以对对象执行所有正常操作。</p></td>
</tr>
</tbody>
</table>

 

还定义了以下标准特定访问权限的组合。 通常不会直接使用这些类，而是将它们用作模板来定义其他位掩码。 （例如，为文件对象指定一般 @ no__t-0READ 时，系统会将此项映射到特定访问权限的文件 @ no__t-1GENERIC @ no__t-2READ 位掩码。 FILE @ no__t-0GENERIC @ no__t-1READ 是根据标准 @ no__t-2RIGHTS @ no__t-3READ 定义的。）

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>位</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>STANDARD_RIGHTS_READ</p></td>
<td><p>对应于 GENERIC_READ 的标准特定权限</p></td>
</tr>
<tr class="even">
<td><p>STANDARD_RIGHTS_WRITE</p></td>
<td><p>对应于 GENERIC_WRITE 的标准特定权限</p></td>
</tr>
<tr class="odd">
<td><p>STANDARD_RIGHTS_EXECUTE</p></td>
<td><p>对应于 GENERIC_EXECUTE 的标准特定权限</p></td>
</tr>
<tr class="even">
<td><p>STANDARD_RIGHTS_REQUIRED</p></td>
<td><p>对应于 GENERIC_ALL 的标准特定权限。 这包括删除但不同步。</p></td>
</tr>
<tr class="odd">
<td><p>STANDARD_RIGHTS_ALL</p></td>
<td><p>所有标准访问权限。</p></td>
</tr>
</tbody>
</table>

 

每种类型的对象都可以有自己的其他访问权限。 有关适用于文件、目录或设备的访问权限的说明，请参阅[**ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile)。 有关适用于对象管理器目录的访问权限的说明，请参阅[**ZwCreateDirectoryObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatedirectoryobject)。 有关适用于注册表项的访问权限的说明，请参阅[**ZwCreateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatekey)。 有关适用于 section 对象的访问权限的说明，请参阅[**ZwOpenSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopensection)。 有关适用于 WMI 数据块的访问权限的说明，请参阅[**IoWMIOpenBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiopenblock)。

有关访问权限的详细信息，请参阅 Microsoft Windows SDK 文档中的以下主题：

-   [访问权限和访问掩码](https://docs.microsoft.com/windows/desktop/SecAuthZ/access-rights-and-access-masks)
-   [ACCESS @ NO__T-1MASK](https://docs.microsoft.com/windows/desktop/SecAuthZ/access-mask)

Wdm .h （包括 Wdm、Ntddk 或 Ntifs）

## <a name="related-topics"></a>相关主题
[**IoWMIOpenBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiopenblock)  
[**ZwCreateDirectoryObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatedirectoryobject)  
[**ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile)  
[**ZwCreateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatekey)  
[**ZwOpenSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopensection)  



