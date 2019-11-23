---
title: WSK_TDI_DEVICENAME_MAPPING
description: WSK_TDI_DEVICENAME_MAPPING
ms.assetid: 7636fa80-3908-4808-8fb8-6227ec6e023b
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WSK_TDI_DEVICENAME_MAPPING 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 60fc5c3785c25c0e58b60f504bde2680c0489525
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844420"
---
# <a name="wsk_tdi_devicename_mapping"></a>WSK\_TDI\_DEVICENAME\_映射


WSK 应用程序使用 WSK\_TDI\_DEVICENAME\_映射客户端控制操作，将地址族、套接字类型和协议的组合映射到[TDI](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565094(v=vs.85))传输的设备名称。 仅当 WSK 应用程序需要支持 TDI 传输时，才使用此客户端控制操作。 当 WSK 应用程序创建套接字时，只有当 WSK 应用程序指定的地址族、套接字类型和协议的组合不提供本机支持时，WSK 子系统才会引用映射的列表。

如果 WSK 应用程序使用 WSK\_TDI\_DEVICENAME\_映射客户端控制操作以将地址族、套接字类型和协议的组合映射到 TDI 传输的设备名称，则必须在创建任何套接字之前执行此操作。

若要将地址族、套接字类型和协议的组合映射到 TDI 传输的设备名称，WSK 应用程序需要使用以下参数调用[**WskControlClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_client)函数。

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
<td><p>WSK_TDI_DEVICENAME_MAPPING</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof （WSK_TDI_MAP_INFO）</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>一个指向<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_tdi_map_info" data-raw-source="[&lt;strong&gt;WSK_TDI_MAP_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_tdi_map_info)"><strong>WSK_TDI_MAP_INFO</strong></a>结构的指针，该结构包含地址族、套接字类型和协议到<a href="https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565091(v=vs.85)" data-raw-source="[TDI](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565091(v=vs.85))">TDI</a>设备名称的组合的映射列表。</p></td>
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

有关使用 TDI 传输的详细信息，请参阅[使用 Tdi 传输](https://docs.microsoft.com/windows-hardware/drivers/network/using-tdi-transports)。

此客户端控制操作的*Irp*参数必须为**NULL** 。

**请注意**，在 Windows Vista 之后的 Microsoft windows 版本中不支持  TDI。 请改用[Windows 筛选平台](https://docs.microsoft.com/windows-hardware/drivers/network/windows-filtering-platform-callout-drivers2)或[Winsock 内核](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)。

 

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

 

 




