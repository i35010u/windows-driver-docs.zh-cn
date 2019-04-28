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
ms.openlocfilehash: 759770a949541de488c13fcc39d021568ab3e0bb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338441"
---
# <a name="registry-run-time-library-routines"></a>注册表运行时库例程





若要操作的注册表项，驱动程序可以调用**Rtl*Xxx*注册表 * Xxx*** 例程，提供较简单的接口比**Zw*Xxx*密钥**例程。 这样做时，该驱动程序不需要打开和关闭句柄;相反，该驱动程序是指密钥的名称。

您传递*RelativeTo*并*路径*到每个参数**Rtl*Xxx*注册表 * Xxx*** 例程。 如果*RelativeTo*是 RTL\_注册表\_绝对的*路径*指定的密钥，开头的完整路径**\\注册表**根。 如果*RelativeTo*是 RTL\_注册表\_处理，*路径*实际上开放句柄。 其他 RTL\_注册表\_*XXX*值*RelativeTo*指定的键; 在这些情况下，常见的根的路径*路径*指定相对于该根的路径。 例如，RTL\_注册表\_用户需要*路径*是相对于当前用户的注册表设置。 (此值相当于指定 HKEY\_当前\_用户模式应用程序中的用户。)有关说明所有 RTL\_注册表\_*XXX*值，请参阅[ **RtlCheckRegistryKey**](https://msdn.microsoft.com/library/windows/hardware/ff561754)。

下表列出了驱动程序可以通过调用执行的操作**Rtl*Xxx*注册表 * Xxx*** 例程。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>操作</th>
<th>Rtl<em>Xxx</em>注册表<em>Xxx</em>例程，以调用</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>创建注册表项</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561822" data-raw-source="[&lt;strong&gt;RtlCreateRegistryKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561822)"><strong>RtlCreateRegistryKey</strong></a></p></td>
</tr>
<tr class="even">
<td><p>检查是否存在注册表项</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561754" data-raw-source="[&lt;strong&gt;RtlCheckRegistryKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561754)"><strong>RtlCheckRegistryKey</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>检查一个或多个注册表项值</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff562046" data-raw-source="[&lt;strong&gt;RtlQueryRegistryValues&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff562046)"><strong>RtlQueryRegistryValues</strong></a></p></td>
</tr>
<tr class="even">
<td><p>写入注册表项值</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563034" data-raw-source="[&lt;strong&gt;RtlWriteRegistryValue&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563034)"><strong>RtlWriteRegistryValue</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>删除注册表项值</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561829" data-raw-source="[&lt;strong&gt;RtlDeleteRegistryValue&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561829)"><strong>RtlDeleteRegistryValue</strong></a></p></td>
</tr>
</tbody>
</table>

 

下面的代码示例演示了如何设置*ValueName*有关**\\注册表\\机\\系统\\**<em>KeyName</em> ULONG 值为 0xFF。 比较此示例中的对应一个[注册表项对象例程](registry-key-object-routines.md)部分。

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

虽然使用时，您编写更少的代码行**Rtl*Xxx*注册表 * Xxx*** 而不是例程**Zw*Xxx*密钥**例程，后一种的不需要执行某些操作。 例如，不**Rtl*Xxx*注册表 * Xxx*** 例程存在对应于[ **ZwEnumerateKey**](https://msdn.microsoft.com/library/windows/hardware/ff566447)。

如果您执行多个相同的密钥操作**Zw*Xxx*密钥**例程的效率更高，可以为每个操作中使用相同的打开句柄。 与此相反， **Rtl*Xxx*注册表 * Xxx*** 例程打开和关闭每个操作的新句柄。

 

 




