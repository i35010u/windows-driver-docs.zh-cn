---
title: .netuse（控制网络连接）
description: .Netuse 命令将连接添加到网络共享。
ms.assetid: f27e5ae5-1beb-4d2b-987e-5e91d0742e2d
keywords:
- .netuse （控制网络连接） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .netuse (Control Network Connections)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9574f14e6be8e9f5805337786f30f63f49a30acb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562647"
---
# <a name="netuse-control-network-connections"></a>.netuse（控制网络连接）


**.Netuse**命令将连接添加到网络共享。

```dbgcmd
.netuse /a "[Local]" "Remote" "[User]" "[Password]" 
```

## <a name="span-idddkmetacontrolnetworkconnectionsdbgspanspan-idddkmetacontrolnetworkconnectionsdbgspanparameters"></a><span id="ddk_meta_control_network_connections_dbg"></span><span id="DDK_META_CONTROL_NETWORK_CONNECTIONS_DBG"></span>参数


<span id="________a______"></span><span id="________A______"></span> **/a**   
添加新的连接。 必须始终使用 **/a**切换。

<span id="_______Local______"></span><span id="_______local______"></span><span id="_______LOCAL______"></span> *Local*   
指定要用于连接的驱动器号。 必须将*本地*引号引起来。 如果省略此参数，则必须作为参数包含一对空引号引起来。

<span id="_______Remote______"></span><span id="_______remote______"></span><span id="_______REMOTE______"></span> *远程*   
指定要连接的共享的 UNC 路径。 必须将*远程*引号引起来。

<span id="_______User______"></span><span id="_______user______"></span><span id="_______USER______"></span> *用户*   
指定有权建立连接的帐户的用户名。 必须将*用户*引号引起来。 如果省略此参数，则必须作为参数包含一对空引号引起来。

<span id="_______Password______"></span><span id="_______password______"></span><span id="_______PASSWORD______"></span> *Password*   
指定与之关联的密码*用户*帐户。 必须将*密码*引号引起来。 如果省略此参数，则必须作为参数包含一对空引号引起来。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**.Netuse**命令的行为类似于**net 使用**Microsoft MS-DOS 命令。

如果您使用 **.netuse**远程调试会话期间，此命令会影响调试服务器，而不是调试客户端。

下面的示例显示了此命令。

```dbgcmd
0:000> .netuse "m:" "\\myserver\myshare" "" "" 
```

 

 





