---
title: WSK_TDI_DEVICENAME_MAPPING
description: WSK_TDI_DEVICENAME_MAPPING
ms.assetid: 7636fa80-3908-4808-8fb8-6227ec6e023b
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WSK_TDI_DEVICENAME_MAPPING 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 045a892e4f732d7ae6be4d9ab8034d1f4ca62135
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90106810"
---
# <a name="wsk_tdi_devicename_mapping"></a>WSK \_ TDI \_ DEVICENAME \_ 映射


WSK 应用程序使用 WSK \_ tdi \_ DEVICENAME \_ 映射客户端控制操作将地址族、套接字类型和协议的组合映射到 [TDI](/previous-versions/windows/hardware/network/ff565094(v=vs.85)) 传输的设备名称。 仅当 WSK 应用程序需要支持 TDI 传输时，才使用此客户端控制操作。 当 WSK 应用程序创建套接字时，只有当 WSK 应用程序指定的地址族、套接字类型和协议的组合不提供本机支持时，WSK 子系统才会引用映射的列表。

如果 WSK 应用程序使用 WSK \_ tdi \_ DEVICENAME \_ 映射客户端控制操作将地址族、套接字类型和协议的组合映射到 TDI 传输的设备名称，则必须在创建任何套接字之前执行此操作。

若要将地址族、套接字类型和协议的组合映射到 TDI 传输的设备名称，WSK 应用程序需要使用以下参数调用 [**WskControlClient**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_client) 函数。

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
<td><p>WSK_TDI_DEVICENAME_MAPPING</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof (WSK_TDI_MAP_INFO) </p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>一个指向 <a href="/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_tdi_map_info" data-raw-source="[&lt;strong&gt;WSK_TDI_MAP_INFO&lt;/strong&gt;](/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_tdi_map_info)"><strong>WSK_TDI_MAP_INFO</strong></a> 结构的指针，该结构包含地址族、套接字类型和协议到 <a href="/previous-versions/windows/hardware/network/ff565091(v=vs.85)" data-raw-source="[TDI](/previous-versions/windows/hardware/network/ff565091(v=vs.85))">TDI</a> 设备名称的组合的映射列表。</p></td>
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

有关使用 TDI 传输的详细信息，请参阅 [使用 Tdi 传输](./using-tdi-transports.md)。

此客户端控制操作的 *Irp* 参数必须为 **NULL** 。

**注意**   Windows Vista 之后的 Microsoft Windows 版本不支持 TDI。 请改用 [Windows 筛选平台](./windows-filtering-platform-callout-drivers2.md) 或 [Winsock 内核](/windows-hardware/drivers/ddi/_netvista/) 。

 

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

