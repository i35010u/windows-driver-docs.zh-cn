---
title: .kdtargetmac（显示目标 MAC 地址）
description: 显示目标 MAC 地址。
keywords:
- kdtargetmac (显示目标 MAC 地址) Windows 调试
ms.date: 05/21/2018
topic_type:
- apiref
api_name:
- .kdtargetmac (Display Target MAC Address)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b5c19f521630f0446de79abe2c4a19c966edd91b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826759"
---
# <a name="kdtargetmac-display-target-mac-address"></a>.kdtargetmac（显示目标 MAC 地址）


显示目标 MAC 地址

```dbgcmd
.kdtargetmac 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>仅限内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅限实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

使用 kdtargetmac 命令显示目标系统的 MAC (media access control) 地址。

```dbgcmd
0: kd> .kdtargetmac 

The target machine MAC address in open-device format is: XXXXXXXXXXXX
```

如果在目标系统上启用了 KDNET，则 kdtargetmac 为命令可用。 使用带有/dbgsettings 选项的 BCDEdit 命令显示目标系统上的配置。 Debugtype 的 *网络* 指示已配置 KDNET。

```dbgcmd
C:\WINDOWS\system32>bcdedit /dbgsettings
key                     1.2.3.4
debugtype               NET
hostip                  192.168.1.10
port                    50000
dhcp                    Yes
The operation completed successfully.
```

有关详细信息，请参阅 [手动设置 KDNET 网络内核调试](setting-up-a-network-debugging-connection.md)。

<a name="remarks"></a>备注
-------

了解目标系统的 MAC 地址对于网络跟踪和其他实用程序可能非常有用。

 

 





