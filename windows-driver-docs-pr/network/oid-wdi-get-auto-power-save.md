---
title: OID_WDI_GET_AUTO_POWER_SAVE
description: OID_WDI_GET_AUTO_POWER_SAVE 获取省电状态的端口。
ms.assetid: b7a14348-66ad-4728-986d-05145eb49b27
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_GET_AUTO_POWER_SAVE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: dc34e729070cc62dccb6fc3069b4767f8fc56c13
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568818"
---
# <a name="oidwdigetautopowersave"></a>OID\_WDI\_GET\_AUTO\_POWER\_SAVE


OID\_WDI\_获取\_自动\_POWER\_保存获取省电状态的端口。

| 范围 | 设置与任务序列化 | 正常执行时间 （秒） |
|-------|--------------------------|---------------------------------|
| 端口  | 不适用           | 1                               |

 

没有省电和延迟之间进行权衡。 当自动节能模式设置为启用了[OID\_WDI\_设置\_连接\_质量](oid-wdi-set-connection-quality.md)命令，固件会尝试连接的访问点，若要转到与之交互节能模式多达相应以节约电源。 固件程序还负责检测连接的访问点确认 802.11 规范，并遵循模式协议节能。 如果不符合的访问点 （不支持节能模式正确），固件应不进入节能模式，即使自动 Power 保存设置为启用。 当设置为禁用自动节能时，固件主要关注发送和接收数据包的低延迟。 此示例包括和流式处理模式时，系统使用交流电源，因此较低的延迟是优先于节省电源时。

## <a name="get-property-parameters"></a>获取属性参数


任何其他参数。 标头中的数据就足够了。
## <a name="get-property-results"></a>获取属性的结果


| TLV                                                                          | 允许多个 TLV 实例 | 可选 | 描述                  |
|------------------------------------------------------------------------------|--------------------------------|----------|------------------------------|
| [**WDI\_TLV\_GET\_AUTO\_POWER\_SAVE**](https://msdn.microsoft.com/library/windows/hardware/dn926307) |                                |          | 自动 power 保存信息。 |

 

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

 

 




