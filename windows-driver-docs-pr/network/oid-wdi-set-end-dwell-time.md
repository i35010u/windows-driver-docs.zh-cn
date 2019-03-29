---
title: OID_WDI_SET_END_DWELL_TIME
description: WDI 必须等待一段时间发送跟进操作帧之前或协议序列完成后，通常会操作帧交换期间发送 OID_WDI_SET_END_DWELL_TIME。
ms.assetid: 8ED1FDB1-BFDB-4522-8FF8-00D3B59EE43C
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_END_DWELL_TIME 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e6a8769db6f39033d33e9d04d209ca782cc03809
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568140"
---
# <a name="oidwdisetenddwelltime"></a>OID\_WDI\_SET\_END\_DWELL\_TIME


OID\_WDI\_设置\_最终\_会仔细斟酌\_时间期间操作帧交换，通常会进行发送，WDI 必须等待一段时间之前发送跟进操作帧，或者当协议序列是完成。 可以在设备端口或站端口上发送此命令。

| 范围 | 设置与任务序列化 | 正常执行时间 （秒） |
|-------|--------------------------|---------------------------------|
| 端口  | 否                       | 1                               |

 

在此命令的回执，固件可以选择停止抛开 WDI 发送命令以发送操作帧时假定已指定的通道。 如果在此再次详述时间已过期，则固件应忽略此命令。

## <a name="set-property-parameters"></a>设置属性参数


任何其他参数。 标头中的数据就足够了。
## <a name="set-property-results"></a>设置属性结果


没有其他数据。 标头中的数据就足够了。
要求
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

 

 




