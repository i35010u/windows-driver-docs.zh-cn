---
title: OID_WDI_ABORT_TASK
description: OID_WDI_ABORT_TASK 是向下发送取消挂起的任务特定的属性。
ms.assetid: 0E454DC9-1CED-497F-90A8-7065883BB945
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_ABORT_TASK 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 36e481f0eff633f580756a8dfc2f1165e30cc884
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353668"
---
# <a name="oidwdiaborttask"></a>OID\_WDI\_ABORT\_TASK


OID\_WDI\_中止\_任务是向下发送取消挂起的任务特定的属性。

| 范围 | 设置与任务序列化 | 正常执行时间 （秒） |
|-------|--------------------------|---------------------------------|
| Port  | 否                       | 1                               |

 

此命令遵循属性语义。 它应被视为一个信号，应尽可能快地处理，应完成独立任务完成。 然后，IHV 组件必须尝试尽可能快地完成挂起的任务。

## <a name="command-parameters"></a>命令参数


| TLV                                                                    | 允许多个 TLV 实例 | 可选 | 描述                                          |
|------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------|
| [**WDI\_TLV\_CANCEL\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-cancel-parameters) |                                |          | 正在取消此命令的信息。 |

 

## <a name="command-result"></a>命令结果


包含状态的 NDIS\_状态\_成功。 没有任何额外负载。
## <a name="examples"></a>示例


原始输入的任务命令：

字段子字段类型值 NDIS\_OID\_请求 Oid NDIS\_OID OID(WDI\_TASK\_SCAN) InputBufferLength UINT32 0x210 （示例） InformationBuffer PVOID 指针指向包含 WDI 的内存块\_消息\_标头 + TLV 负载 WDI\_消息\_标头 PortId UINT16 0x0001 （示例） 保留 UINT16 n/A WiFiStatus NDIS\_状态 n/A TransactionId UINT32 0x1111 （示例) IhvSpecificId UINT32 n/A TLV 负载 TLV 负载各种负载数据
 

中止任务输入的命令 （使用消息标头中）：

字段子字段类型值 NDIS\_OID\_请求 Oid NDIS\_OID OID(WDI\_ABORT\_TASK) InputBufferLength UINT32 sizeof (WDI\_消息\_标头) + sizeof (WDI\_TLV\_取消\_参数) InformationBuffer PVOID 指向内存块，其中包含 WDI\_消息\_标头 + TLV 负载 WDI\_消息\_标头 PortId UINT16 0x0001 （示例） 保留 UINT16 n/A WiFiStatus NDIS\_状态 n/A TransactionId UINT32 0x2222 （示例） IhvSpecificId UINT32 0 WDI\_TLV\_取消\_参数OriginalTaskOid NDIS\_OID OID(WDI\_TASK\_SCAN) OriginalPortId UINT16 0x0001 （示例） OriginalTransactionId UINT32 0x1111 （示例）
 

中止任务命令的结果：

字段子字段类型值 NDIS\_OID\_请求 Oid NDIS\_OID OID(WDI\_TASK\_SCAN) OutputBufferLength UINT32 sizeof (WDI\_消息\_标头)InformationBuffer PVOID 指向内存块，其中包含 WDI\_消息\_标头 WDI\_消息\_标头 PortId UINT16 0x0001 （示例） 保留 UINT16 n/A WiFiStatus NDIS\_状态 NDIS\_状态\_成功 TransactionId UINT32 0x2222 （示例） IhvSpecificId UINT32 n/A
 

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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 




