---
title: OID_WDI_SET_END_DWELL_TIME
description: OID_WDI_SET_END_DWELL_TIME 通常在操作帧交换期间发送，无论 WDI 在发送跟进操作帧之前必须等待一段时间，还是在协议序列完成后发送。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_END_DWELL_TIME 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 61818931da964daeaa3f82ba9d587938a07e38ca
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829381"
---
# <a name="oid_wdi_set_end_dwell_time"></a>OID \_ WDI \_ SET \_ 结束 \_ 停留 \_ 时间


OID \_ WDI \_ 设置 \_ 结束 \_ 停留 \_ 时间通常在操作帧交换期间发送（当 WDI 必须等待一段时间才能发送跟进操作框架或协议序列完成时）。 可以在设备端口或工作站端口上发送此命令。

| 范围 | 设置序列化任务 | 正常执行时间 (秒)  |
|-------|--------------------------|---------------------------------|
| 端口  | 否                       | 1                               |

 

收到此命令后，固件可以选择在 WDI 发送命令发送操作帧时，停止已指定的通道上的 dwelling。 如果停留时间已过期，则固件应忽略此命令。

## <a name="set-property-parameters"></a>设置属性参数


无其他参数。 标头中的数据足够了。
## <a name="set-property-results"></a>设置属性结果


无其他数据。 标头中的数据足够了。

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

 

 




