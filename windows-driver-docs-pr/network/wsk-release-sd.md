---
title: WSK_RELEASE_SD
description: WSK_RELEASE_SD
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WSK_RELEASE_SD 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: df23ce884d20997666227a1ab3b8fa4a2cf875dc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813621"
---
# <a name="wsk_release_sd"></a>WSK \_ RELEASE \_ SD


WSK 应用程序使用 WSK \_ release \_ sd client control 操作来释放以前使用 [**WSK \_ 缓存 \_ SD**](wsk-cache-sd.md) 客户端控制操作获取的安全描述符的缓存副本，或使用 [**\_ WSK \_ security**](so-wsk-security.md) socket 选项检索此描述符。

若要释放安全描述符的缓存副本，WSK 应用程序需要使用以下参数调用 [**WskControlClient**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_client) 函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>参数</th>
<th>“值”</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ControlCode</em></p></td>
<td><p>WSK_RELEASE_SD</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof (PSECURITY_DESCRIPTOR) </p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>指向 PSECURITY_DESCRIPTOR 类型化变量的指针。 此变量包含一个指向 SECURITY_DESCRIPTOR 结构的指针，该结构定义要释放的缓存安全说明符。</p></td>
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

有关安全描述符结构的详细信息 \_ ，请参阅 \_ Microsoft Windows SDK 文档中的安全描述符的参考页。

此客户端控制操作的 *Irp* 参数必须为 **NULL** 。

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
<td><p>标头</p></td>
<td>Wsk (包含 Wsk) </td>
</tr>
</tbody>
</table>

 

