---
title: WSK_RELEASE_SD
description: WSK_RELEASE_SD
ms.assetid: de8cc759-c778-464e-9e19-984ea20c0d29
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WSK_RELEASE_SD 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 43396190f4f9d1e890437251ebfb5a922f1f1b4f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386309"
---
# <a name="wskreleasesd"></a>WSK\_RELEASE\_SD


WSK 应用程序使用 WSK\_释放\_SD 客户端控制操作以释放任何一个通过使用先前获得的安全描述符的缓存的副本[ **WSK\_缓存\_SD** ](wsk-cache-sd.md)客户端管理操作或使用检索[**因此\_WSK\_安全**](so-wsk-security.md)套接字选项。

若要释放的安全描述符的缓存的副本，WSK 应用程序调用[ **WskControlClient** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_client)使用以下参数的函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>参数</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ControlCode</em></p></td>
<td><p>WSK_RELEASE_SD</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof(PSECURITY_DESCRIPTOR)</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>指向 PSECURITY_DESCRIPTOR 类型的变量的指针。 此变量包含指向 SECURITY_DESCRIPTOR 结构，它定义要发布的缓存的安全描述符的指针。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>Irp</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
</tbody>
</table>

有关安全性的详细信息\_描述符结构，请参阅有关安全的参考页\_Microsoft Windows SDK 文档中的描述符。

*Irp*参数必须是**NULL**此客户端控制操作。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>在 Windows Vista 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wsk.h （包括 Wsk.h）</td>
</tr>
</tbody>
</table>

 

 




