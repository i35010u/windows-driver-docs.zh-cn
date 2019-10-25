---
title: 注册表运行时库例程
description: 注册表运行时库例程
ms.assetid: 53e55969-3c8e-44ab-8ba7-6abb0ddbfc24
keywords:
- 注册表 WDK 内核，运行时库例程
- 驱动程序注册表信息 WDK 内核，运行时库例程
- 运行时库例程 WDK 内核
- RtlXxxRegistryYyy 例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2369bc67424e3052c3cc6065e23186b763c1a8d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827459"
---
# <a name="registry-run-time-library-routines"></a>注册表运行时库例程





若要操作注册表项，驱动程序可以调用**Rtl*xxx*registry * Xxx**，它们提供比**Zw*Xxx*密钥**例程更简单的接口。 执行此操作时，驱动程序不需要打开和关闭句柄;相反，驱动程序会按名称引用密钥。

将*RelativeTo*和*Path*参数传递给每个**Rtl*Xxx*Registry * xxx*** 例程。 如果*RelativeTo*为 RTL\_注册表\_绝对路径，则*Path*指定密钥的完整路径，从 **\\注册表**根开始。 如果*RelativeTo*为 RTL\_注册表\_句柄，则*路径*实际上是一个打开的句柄。 其他 RTL\_注册表\_*XXX*值用于*RelativeTo*指定密钥的公共根的路径;在这些情况下， *path*指定相对于该根的路径。 例如，RTL\_注册表\_用户要求该*路径*相对于当前用户的注册表设置。 （此值等效于在用户模式应用程序中指定 HKEY\_当前\_用户。）有关所有 RTL\_注册表\_*XXX*值的说明，请参阅[**RtlCheckRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlcheckregistrykey)。

下表列出了驱动程序可以通过调用**Rtl*Xxx*Registry * Xxx*** 例程执行的操作。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>操作</th>
<th>要调用的 Rtl<em>xxx</em>Registry<em>xxx</em>例程</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>创建注册表项</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlcreateregistrykey" data-raw-source="[&lt;strong&gt;RtlCreateRegistryKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlcreateregistrykey)"><strong>RtlCreateRegistryKey</strong></a></p></td>
</tr>
<tr class="even">
<td><p>检查注册表项是否存在</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlcheckregistrykey" data-raw-source="[&lt;strong&gt;RtlCheckRegistryKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlcheckregistrykey)"><strong>RtlCheckRegistryKey</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>检查一个或多个注册表项值</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlqueryregistryvalues" data-raw-source="[&lt;strong&gt;RtlQueryRegistryValues&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlqueryregistryvalues)"><strong>RtlQueryRegistryValues</strong></a></p></td>
</tr>
<tr class="even">
<td><p>写入注册表项值</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlwriteregistryvalue" data-raw-source="[&lt;strong&gt;RtlWriteRegistryValue&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlwriteregistryvalue)"><strong>RtlWriteRegistryValue</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>删除注册表项值</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtldeleteregistryvalue" data-raw-source="[&lt;strong&gt;RtlDeleteRegistryValue&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtldeleteregistryvalue)"><strong>RtlDeleteRegistryValue</strong></a></p></td>
</tr>
</tbody>
</table>

 

下面的代码示例演示如何将 **\\注册表\\Machine\\System\\** <em>KeyName</em>的*ValueName*设置为 ULONG 值0xff。 将此示例与 "[注册表项对象例程](registry-key-object-routines.md)" 部分中的对应项进行比较。

```cpp
NTSTATUS status;
ULONG data = 0xFF;

status = RtlWriteRegistryValue(RTL_REGISTRY_ABSOLUTE,
                               (PWCSTR)L"\\Registry\\Machine\\System\\KeyName",
                               (PWCSTR)L"ValueName",
                               REG_DWORD,
                               &data,
                               sizeof(ULONG));
```

尽管使用**Rtl*xxx*Registry * Xxx*** 例程（而不是**Zw*Xxx*密钥**例程）编写的代码行更少，但在执行某些操作时需要使用后者。 例如，不存在对应于[**ZwEnumerateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwenumeratekey)的**Rtl*Xxx*Registry * Xxx*** 例程。

如果对同一项执行多个操作， **Zw*Xxx*密钥**例程将更高效，你可以对每个操作使用相同的打开句柄。 与此相反， **Rtl*Xxx*Registry * Xxx*** 例程打开并关闭每个操作的新句柄。

 

 




