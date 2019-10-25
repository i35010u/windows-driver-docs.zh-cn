---
title: WSK_RELEASE_SD
description: WSK_RELEASE_SD
ms.assetid: de8cc759-c778-464e-9e19-984ea20c0d29
ms.date: 07/18/2017
keywords:
- WSK_RELEASE_SD 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f76618607d7f9cb48d383a22cb194599e1ce3d41
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844355"
---
# <a name="wsk_release_sd"></a>WSK\_RELEASE\_SD


WSK 应用程序使用 WSK\_RELEASE\_SD client control 操作来释放以前使用[**WSK\_缓存\_SD**](wsk-cache-sd.md) client control 操作获取的安全描述符的缓存副本，或 was使用[ **\_WSK\_SECURITY**](so-wsk-security.md) socket 选项检索。

若要释放安全描述符的缓存副本，WSK 应用程序需要使用以下参数调用[**WskControlClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_client)函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>参数</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ControlCode</em></p></td>
<td><p>WSK_RELEASE_SD</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof （PSECURITY_DESCRIPTOR）</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>指向 PSECURITY_DESCRIPTOR 类型的变量的指针。 此变量包含一个指向 SECURITY_DESCRIPTOR 结构的指针，该结构定义要释放的缓存安全说明符。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p><strong>无效</strong></p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p><strong>无效</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>Irp</em></p></td>
<td><p><strong>无效</strong></p></td>
</tr>
</tbody>
</table>

有关安全\_描述符结构的详细信息，请参阅 Microsoft Windows SDK 文档中的安全性\_描述符的参考页。

此客户端控制操作的*Irp*参数必须为**NULL** 。

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
<td>Wsk （包括 Wsk）</td>
</tr>
</tbody>
</table>

 

 




