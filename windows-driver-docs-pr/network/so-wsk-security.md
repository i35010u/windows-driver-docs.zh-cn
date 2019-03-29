---
title: SO_WSK_SECURITY
description: SO_WSK_SECURITY
ms.assetid: 169680ba-6486-48fe-89d7-dcd4e5930605
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 SO_WSK_SECURITY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 49658a55beabad6539913604a6ccdc5a2f425d8f
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349848"
---
# <a name="sowsksecurity"></a>因此\_WSK\_安全


SO\_WSK\_安全套接字选项允许 WSK 的应用程序安全描述符应用到套接字或检索从套接字的套接字的安全描述符的缓存的副本。 安全描述符控制共享套接字绑定到的本地传输地址。

此套接字选项仅适用于侦听套接字、 数据报套接字和面向连接的套接字。

如果 WSK 应用程序使用此套接字选项将安全描述符应用到套接字，它必须实现之前接字绑定到本地传输地址。

若要将安全描述符应用到套接字，WSK 应用程序调用[ **WskControlSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571127)使用以下参数的函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>参数</th>
<th>ReplTest1</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>RequestType</em></p></td>
<td><p><strong>WskSetOption</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SO_WSK_SECURITY</p></td>
</tr>
<tr class="odd">
<td><p><em>Level</em></p></td>
<td><p>SOL_SOCKET</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof(PSECURITY_DESCRIPTOR)</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>指向 PSECURITY_DESCRIPTOR 类型的变量的指针。 此变量必须包含一个指向通过调用获取的安全描述符的缓存副本<a href="https://msdn.microsoft.com/library/windows/hardware/ff571126" data-raw-source="[&lt;strong&gt;WskControlClient&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff571126)"> <strong>WskControlClient</strong> </a>函数与<a href="wsk-cache-sd.md" data-raw-source="[&lt;strong&gt;WSK_CACHE_SD&lt;/strong&gt;](wsk-cache-sd.md)"> <strong>WSK_CACHE_SD</strong> </a>控制代码。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>NULL</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>

WSK 应用程序调用时必须指定一个指向 IRP **WskControlSocket**函数将安全描述符应用到套接字。

如果 WSK 应用程序使用此套接字选项将安全描述符应用到套接字，新的安全描述符将替换任何以前应用到套接字的安全描述符。

WSK 应用程序 IRP 完成后，必须释放之前的安全描述符的缓存的副本。

WSK 应用程序还可以应用的安全描述符到套接字时通过指定指向安全描述符中的缓存副本的最初创建套接字*SecurityDescriptor*参数时它将调用[ **WskSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571149)或[ **WskSocketConnect** ](https://msdn.microsoft.com/library/windows/hardware/ff571150)函数。

如果 WSK 应用程序不适用于到套接字的安全描述符，WSK 子系统使用不允许共享的本地传输地址的默认安全描述符。

若要检索的套接字发出的套接字的安全描述符的缓存的副本，WSK 应用程序调用[ **WskControlSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571127)使用以下参数的函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>参数</th>
<th>ReplTest1</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>RequestType</em></p></td>
<td><p><strong>WskGetOption</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SO_WSK_SECURITY</p></td>
</tr>
<tr class="odd">
<td><p><em>Level</em></p></td>
<td><p>SOL_SOCKET</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>NULL</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>sizeof(PSECURITY_DESCRIPTOR)</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>指向 PSECURITY_DESCRIPTOR 类型的变量的指针。 此变量接收指向套接字的安全描述符的缓存副本。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>

WSK 应用程序调用时必须指定一个指向 IRP **WskControlSocket**函数以检索从套接字的套接字的安全描述符的缓存的副本。

WSK 应用程序必须调用[ **WskControlClient** ](https://msdn.microsoft.com/library/windows/hardware/ff571126)函数与[ **WSK\_版本\_SD** ](wsk-release-sd.md)控制代码，以便当不再需要释放的安全描述符的缓存的副本。

有关安全性的详细信息\_描述符结构，请参阅有关安全的参考页\_Microsoft Windows SDK 文档中的描述符。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>在 Windows Vista 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wsk.h （包括 Wsk.h）</td>
</tr>
</tbody>
</table>

 

 




