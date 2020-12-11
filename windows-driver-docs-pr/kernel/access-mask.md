---
title: 指定访问权限
description: 指定访问权限
ms.localizationpriority: High
ms.date: 10/17/2018
ms.openlocfilehash: 579eadc9349b09f94164216a4521290fb3f61afa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840695"
---
# <a name="specifying-access-rights"></a>指定访问权限


ACCESS\_MASK 类型是一个位掩码，它在[访问控制项](../ifs/access-control-entry.md)的[访问掩码](../ifs/access-mask.md)中指定一组访问权限。

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
<th>标志</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DELETE</p></td>
<td><p>调用方可以删除对象。</p></td>
</tr>
<tr class="even">
<td><p>READ_CONTROL</p></td>
<td><p>调用方可以读取文件的访问控制列表 (ACL) 和所有权信息。</p></td>
</tr>
<tr class="odd">
<td><p>SYNCHRONIZE</p></td>
<td><p>调用方可以对对象执行等待操作。 （例如，可以将对象传递到 <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitformultipleobjects" data-raw-source="[&lt;strong&gt;KeWaitForMultipleObjects&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitformultipleobjects)"><strong>KeWaitForMultipleObjects</strong></a>。）</p></td>
</tr>
<tr class="even">
<td><p>WRITE_DAC</p></td>
<td><p>调用方可以更改对象的自定义访问控制列表 (DACL) 信息。</p></td>
</tr>
<tr class="odd">
<td><p>WRITE_OWNER</p></td>
<td><p>调用方可以更改文件的所有权信息。</p></td>
</tr>
</tbody>
</table>

 

请注意，通常只有 DELETE 和 SYNCHRONIZE 受驱动程序编写者关注。

还可以指定以下通用访问权限。 它们也适用于所有类型的执行对象。 每个通用访问权限的含义特定于该类型的对象。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>标志</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>GENERIC_READ</p></td>
<td><p>调用方可以对对象执行正常的读取操作。</p></td>
</tr>
<tr class="even">
<td><p>GENERIC_WRITE</p></td>
<td><p>调用方可以对对象执行正常的写入操作。</p></td>
</tr>
<tr class="odd">
<td><p>GENERIC_EXECUTE</p></td>
<td><p>调用方可以执行对象。 （请注意，这通常仅对文件对象和节对象等特定类型的对象有意义。）</p></td>
</tr>
<tr class="even">
<td><p>GENERIC_ALL</p></td>
<td><p>调用方可以对对象执行所有正常的操作。</p></td>
</tr>
</tbody>
</table>

 

还定义了以下标准特定访问权限的组合。 通常不会直接使用这些组合，而是会将它们用作模板来定义其他位掩码。 （例如，当你为文件对象指定 GENERIC\_READ 时，系统会将此信息映射到特定访问权限的 FILE\_GENERIC\_READ 位掩码。 FILE\_GENERIC\_READ 按照 STANDARD\_RIGHTS\_READ 定义。）

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>位掩码</th>
<th>说明</th>
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
<td><p>对应于 GENERIC_ALL 的标准特定权限。 这包括 DELETE，但不包括 SYNCHRONIZE。</p></td>
</tr>
<tr class="odd">
<td><p>STANDARD_RIGHTS_ALL</p></td>
<td><p>所有标准访问权限。</p></td>
</tr>
</tbody>
</table>

 

每种类型的对象都可以有自己的其他访问权限。 有关适用于文件、目录或设备的访问权限的说明，请参阅 [**ZwCreateFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)。 有关适用于对象管理器目录的访问权限的说明，请参阅 [**ZwCreateDirectoryObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatedirectoryobject)。 有关适用于注册表项的访问权限的说明，请参阅 [**ZwCreateKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatekey)。 有关适用于节对象的访问权限的说明，请参阅 [**ZwOpenSection**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopensection)。 有关适用于 WMI 数据块的访问权限的说明，请参阅 [**IoWMIOpenBlock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiopenblock)。

有关访问权限的详细信息，请参阅 Microsoft Windows SDK 文档中的以下主题：

-   [访问权限和访问掩码](/windows/desktop/SecAuthZ/access-rights-and-access-masks)
-   [ACCESS\_MASK](/windows/desktop/SecAuthZ/access-mask)

Wdm.h（包括 Wdm.h、Ntddk.h 或 Ntifs.h）

## <a name="related-topics"></a>相关主题
[**IoWMIOpenBlock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiopenblock)  
[**ZwCreateDirectoryObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatedirectoryobject)  
[**ZwCreateFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)  
[**ZwCreateKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatekey)  
[**ZwOpenSection**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopensection)
