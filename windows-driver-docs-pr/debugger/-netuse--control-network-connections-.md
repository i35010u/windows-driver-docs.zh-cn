---
title: .netuse（控制网络连接）
description: Netuse 命令将连接添加到网络共享。
keywords:
- netuse (控制网络连接) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .netuse (Control Network Connections)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8683548a0c34db0ccabc0b398e78ec2f0af5d43b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803309"
---
# <a name="netuse-control-network-connections"></a>.netuse（控制网络连接）


**Netuse** 命令将连接添加到网络共享。

```dbgcmd
.netuse /a "[Local]" "Remote" "[User]" "[Password]" 
```

## <a name="span-idddk_meta_control_network_connections_dbgspanspan-idddk_meta_control_network_connections_dbgspanparameters"></a><span id="ddk_meta_control_network_connections_dbg"></span><span id="DDK_META_CONTROL_NETWORK_CONNECTIONS_DBG"></span>参数


<span id="________a______"></span><span id="________A______"></span>**/a**   
添加新连接。 必须始终使用 **/a** 开关。

<span id="_______Local______"></span><span id="_______local______"></span><span id="_______LOCAL______"></span>*本地*   
指定用于连接的驱动器号。 必须用引号将 *本地* 括起来。 如果省略此参数，则必须包含一对空的引号作为参数。

<span id="_______Remote______"></span><span id="_______remote______"></span><span id="_______REMOTE______"></span>*远程*   
指定正在连接的共享的 UNC 路径。 必须用引号将 *远程* 括起来。

<span id="_______User______"></span><span id="_______user______"></span><span id="_______USER______"></span>*用户*   
指定有权建立连接的帐户的用户名。 必须将 *用户* 用引号引起来。 如果省略此参数，则必须包含一对空的引号作为参数。

<span id="_______Password______"></span><span id="_______password______"></span><span id="_______PASSWORD______"></span>*密码*   
指定与 *用户* 帐户关联的密码。 必须将 *密码* 用引号引起来。 如果省略此参数，则必须包含一对空的引号作为参数。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**Netuse** 命令的行为类似于 **net use** Microsoft MS-DOS 命令。

如果在远程调试会话期间使用 **. netuse** ，此命令将影响调试服务器，而不会影响调试客户端。

下面的示例显示了此命令。

```dbgcmd
0:000> .netuse "m:" "\\myserver\myshare" "" "" 
```

 

 





