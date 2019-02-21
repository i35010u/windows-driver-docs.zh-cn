---
title: .kdtargetmac （显示目标 MAC 地址）
description: 显示目标 MAC 地址。
ms.assetid: 95042682-BD92-44B0-AAA8-AB8661393230
keywords:
- .kdtargetmac （显示目标 MAC 地址） Windows 调试
ms.date: 05/21/2018
topic_type:
- apiref
api_name:
- .kdtargetmac (Display Target MAC Address)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f8c92bc89fa5ba62ce8aca2a33240b6761eb9444
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533206"
---
# <a name="kdtargetmac-display-target-mac-address"></a>.kdtargetmac （显示目标 MAC 地址）


显示目标 MAC 地址

```dbgcmd
.kdtargetmac 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>内核模式下</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

使用.kdtargetmac 命令显示在目标系统的 MAC （媒体访问控制） 地址。

```dbgcmd
0: kd> .kdtargetmac 

The target machine MAC address in open-device format is: XXXXXXXXXXXX
```

.Kdtargetmac 是命令在目标系统上启用 KDNET 时可用。 使用具有 /dbgsettings 选项 BCDEdit 命令在目标系统上显示的配置。 Debugtype *NET*指示 KDNET 已配置。

```dbgcmd
C:\WINDOWS\system32>bcdedit /dbgsettings
key                     1.2.3.4
debugtype               NET
hostip                  192.168.1.10
port                    50000
dhcp                    Yes
The operation completed successfully.
```

有关详细信息，请参阅[设置向上 KDNET 网络内核调试手动](setting-up-a-network-debugging-connection.md)。

<a name="remarks"></a>备注
-------

了解在目标系统的 MAC 地址也可用于网络跟踪和其他实用程序。

 

 





