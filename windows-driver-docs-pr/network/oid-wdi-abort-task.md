---
title: OID_WDI_ABORT_TASK
description: OID_WDI_ABORT_TASK 是向下发送以取消特定挂起任务的属性。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_ABORT_TASK 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d0a6022ff99eaffc2bcf3f8293fd4c6461ac364d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783793"
---
# <a name="oid_wdi_abort_task"></a>OID \_ WDI \_ 中止 \_ 任务


OID \_ WDI \_ 中止 \_ 任务是向下发送以取消特定挂起任务的属性。

| 范围 | 设置序列化任务 | 正常执行时间 (秒)  |
|-------|--------------------------|---------------------------------|
| 端口  | 否                       | 1                               |

 

此命令遵循属性语义。 应将它视为信号，应尽快处理，并应独立于任务完成完成。 然后，IHV 组件必须尽快尝试完成挂起的任务。

## <a name="command-parameters"></a>命令参数


| TLV                                                                    | 允许多个 TLV 实例 | 可选 | 说明                                          |
|------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------|
| [**WDI \_ TLV \_ 取消 \_ 参数**](./wdi-tlv-cancel-parameters.md) |                                |          | 要取消的命令的信息。 |

 

## <a name="command-result"></a>命令结果


包含 NDIS \_ 状态 \_ 成功状态。 没有其他有效负载。
## <a name="examples"></a>示例


原始输入任务命令：

字段子字段类型值 NDIS \_ oid \_ 请求 oid NDIS \_ OID oid (WDI \_ TASK \_ SCAN) InputBufferLength UINT32 0X210 (示例) InformationBuffer PVOID 指向包含 WDI \_ 消息 \_ 头 + TLV 负载 WDI 消息标头的内存块的指针 + TLV 负载 PortId \_ 消息 \_ 标头 0x0001 UINT16 WiFiStatus (示例) 保留 UINT16 \_
 

中止任务输入命令 (，消息标头) ：

字段子字段类型值 NDIS \_ oid \_ 请求 oid NDIS \_ OID oid (WDI \_ ABORT \_ TASK) InputBufferLength UINT32 sizeof (WDI \_ 消息 \_ 标头) + Sizeof (WDI \_ TLV \_ 取消 \_ 参数) InformationBuffer PVOID 指向包含 WDI 消息头 + TLV 负载的内存块的指针 WDI \_ \_ \_ 消息标头 \_ PortId UINT16 0X0001 (示例) 保留 UINT16 n/a WiFiStatus NDIS \_ 状态 n/a TransactionId UINT32 0x2222 (示例) IhvSpecificId Uint32 0 WDI \_ TLV \_ 取消 \_ 参数 OriginalTaskOid NDIS \_ OID oid (WDI \_ 任务 \_ 扫描) OriginalPortId UINT16 0x0001 (示例) OriginalTransactionId UINT32 0x1111 (示例) 
 

中止任务命令结果：

字段子字段类型值 NDIS \_ oid \_ 请求 oid NDIS \_ OID oid (WDI \_ TASK \_ SCAN) OutputBufferLength UINT32 sizeof (WDI \_ 消息 \_ 标头) InformationBuffer PVOID 指向包含 WDI 消息头的内存块的指针 WDI 消息头 \_ \_ \_ \_ PortId UINT16 0x0001 (示例) 保留 UINT16 n/a WiFiStatus ndis \_ 状态 NDIS \_ 状态 \_ 成功 TransactionId
 

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
<td>Dot11wdi</td>
</tr>
</tbody>
</table>

 

