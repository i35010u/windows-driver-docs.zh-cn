---
title: CTRL + D （切换调试信息）
description: CTRL + D 键切换调试器的内部信息流打开和关闭。 这用于在其中调试器无法正常通信的情况下重新开始通信。
ms.assetid: fcc5d597-6a3f-4d6c-82f9-3624efb4f434
keywords:
- CTRL + D （切换调试信息） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CTRL+D (Toggle Debug Info)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3907900b3bdc971293c9aae752738d2c6445952d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542347"
---
# <a name="ctrld-toggle-debug-info"></a>CTRL + D （切换调试信息）


CTRL + D 键切换调试器的内部信息流打开和关闭。 这用于在其中调试器无法正常通信的情况下重新启动目标计算机和主机计算机之间的通信。

KD 语法

```dbgcmd
CTRL+D  ENTER 
```

WinDbg 语法

```dbgcmd
CTRL+ALT+D 
```

## <span id="ddk_meta_ctrl_d_dbg"></span><span id="DDK_META_CTRL_D_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>调试器</strong></p></td>
<td align="left"><p>KD 和 WinDbg 仅</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>内核模式下</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅实时调试</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

这已切换，调试器会输出有关主机计算机和目标计算机之间通信的信息。

此密钥可用于测试是否在调试器已崩溃。 如果您怀疑调试器或目标已被冻结，则使用此密钥。 如果您看到正在发送的数据包，目标仍然正常工作。 如果您看到超时消息，然后在目标未响应。 如果没有任何消息根本，调试器已崩溃。

如果目标没有响应，使用 CTRL + R 输入 CTRL + C。 如果超时消息继续出现，目标已崩溃 （或调试器未正确配置）。

这也是用于调试 KD 调试器本身。

 

 





