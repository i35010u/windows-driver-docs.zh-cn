---
title: .netsyms（禁用网络符号加载）
description: .netsyms（禁用网络符号加载）
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08008d16de3e2dc216a174309d5e25c819d6ab14
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803313"
---
# <a name="netsyms-disable-network-symbol-loading"></a>.netsyms（禁用网络符号加载）


## <span id="ddk_apc_meta_netsyms_dbg"></span><span id="DDK_APC_META_NETSYMS_DBG"></span>


使用 netsyms 命令可允许或禁止从网络路径加载符号。

### <a name="span-idkd_syntaxspanspan-idkd_syntaxspansyntax"></a><span id="kd_syntax"></span><span id="KD_SYNTAX"></span>语法

**。 netsyms** *{yes | no}*

### <a name="span-idparametersspanspan-idparametersspanparameters"></a><span id="parameters"></span><span id="PARAMETERS"></span>参数

<span id="yes"></span><span id="YES"></span>*是的*  
启用网络符号加载。 这是默认值。

<span id="no"></span><span id="NO"></span>*不*  
禁用网络符号加载。

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
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idremarksspanspan-idremarksspanremarks"></a><span id="remarks"></span><span id="REMARKS"></span>标记

使用不带参数的 netsyms 以显示此设置的当前状态。

使用 [**！符号干扰**](-sym.md) 或 *-n* [**WinDbg Command-Line 选项**](windbg-command-line-options.md) ，以在加载符号时显示更多详细信息。

 

 





