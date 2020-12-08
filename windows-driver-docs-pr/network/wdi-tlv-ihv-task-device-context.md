---
title: WDI_TLV_IHV_TASK_DEVICE_CONTEXT
description: WDI_TLV_IHV_TASK_DEVICE_CONTEXT 是一种 TLV，其中包含用于 NDIS_STATUS_WDI_INDICATION_IHV_TASK_REQUEST 的由 IHV 提供的设备上下文。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_IHV_TASK_DEVICE_CONTEXT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: bb6a3a40f43acfb8ba775bbc943e5ab4bf339f7d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791299"
---
# <a name="wdi_tlv_ihv_task_device_context"></a>WDI \_ TLV \_ IHV \_ 任务 \_ 设备 \_ 上下文


WDI \_ tlv \_ IHV \_ 任务 \_ 设备 \_ 上下文是一个 TLV，其中包含由 IHV 提供的用于 [NDIS \_ 状态 \_ WDI \_ 指示 \_ IHV \_ 任务 \_ 请求](./ndis-status-wdi-indication-ihv-task-request.md)的设备上下文。

## <a name="tlv-type"></a>TLV 类型


0xE0

## <a name="length"></a>长度


UINT8 元素数组的大小 (以字节为单位) 。 数组必须包含1个或多个元素。

## <a name="values"></a>值


| 类型      | 描述                                                                    |
|-----------|--------------------------------------------------------------------------------|
| UINT8\[\] | 由 IHV 提供的、转发到 IHV 任务的设备上下文信息。 |

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

