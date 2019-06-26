---
title: WSK_TDI_DEVICENAME_MAPPING
description: WSK_TDI_DEVICENAME_MAPPING
ms.assetid: 7636fa80-3908-4808-8fb8-6227ec6e023b
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WSK_TDI_DEVICENAME_MAPPING 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 57851b9e6e76a0d889724b84e959c8fe03bbf8b5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379711"
---
# <a name="wsktdidevicenamemapping"></a>WSK\_TDI\_DEVICENAME\_MAPPING


WSK 应用程序使用 WSK\_TDI\_DEVICENAME\_映射客户端管理操作要映射的地址族的组合，套接字类型，并与设备名称的协议[TDI](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565094(v=vs.85))传输。 WSK 应用程序使用此客户端管理操作，仅当它需要支持 TDI 传输。 时 WSK 应用程序创建的套接字，仅当地址族、 套接字类型和指定 WSK 应用程序协议的组合不本机支持的映射列表请参阅 WSK 子系统。

如果 WSK 应用程序使用 WSK\_TDI\_DEVICENAME\_映射客户端管理操作要映射的地址族、 套接字类型和协议组合到 TDI 传输的设备名称，它必须执行此操作之前它会创建任何套接字。

若要映射的地址族、 套接字类型和协议组合到 TDI 传输的设备名称，WSK 应用程序调用[ **WskControlClient** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_client)使用以下参数的函数。

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
<td><p><em>ControlCode</em></p></td>
<td><p>WSK_TDI_DEVICENAME_MAPPING</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof(WSK_TDI_MAP_INFO)</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>一个指向<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/ns-wsk-_wsk_tdi_map_info" data-raw-source="[&lt;strong&gt;WSK_TDI_MAP_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/ns-wsk-_wsk_tdi_map_info)"> <strong>WSK_TDI_MAP_INFO</strong> </a>结构，其中包含的映射的地址族的组合列表套接字类型，并为协议<a href="https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565091(v=vs.85)" data-raw-source="[TDI](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565091(v=vs.85))">TDI</a>设备名称。</p></td>
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

有关使用 TDI 传输的详细信息，请参阅[使用 TDI 传输](https://docs.microsoft.com/windows-hardware/drivers/network/using-tdi-transports)。

*Irp*参数必须是**NULL**此客户端控制操作。

**请注意**  TDI 将不支持在 Microsoft Windows 版本在 Windows Vista 后。 使用[Windows 筛选平台](https://docs.microsoft.com/windows-hardware/drivers/network/windows-filtering-platform-callout-drivers2)或[Winsock 内核](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)相反。

 

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

 

 




