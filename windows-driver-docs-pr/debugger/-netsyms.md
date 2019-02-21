---
title: .netsyms （禁用网络符号加载）
description: .netsyms （禁用网络符号加载）
ms.assetid: 09347909-47C8-4a4d-8246-C32A1791F46B
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7a6eea7941550e08ef5d10a8f1c942b73266440
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544708"
---
# <a name="netsyms-disable-network-symbol-loading"></a>.netsyms （禁用网络符号加载）


## <span id="ddk_apc_meta_netsyms_dbg"></span><span id="DDK_APC_META_NETSYMS_DBG"></span>


使用.netsyms 命令以允许或禁止从网络路径加载符号。

### <a name="span-idkdsyntaxspanspan-idkdsyntaxspansyntax"></a><span id="kd_syntax"></span><span id="KD_SYNTAX"></span>语法

**.netsyms** *{yes | 无}*

### <a name="span-idparametersspanspan-idparametersspanparameters"></a><span id="parameters"></span><span id="PARAMETERS"></span>参数

<span id="yes"></span><span id="YES"></span>*是的*  
使网络符号加载。 这是默认设置。

<span id="no"></span><span id="NO"></span>*no*  
禁用网络符号加载。

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

 

### <a name="span-idremarksspanspan-idremarksspanremarks"></a><span id="remarks"></span><span id="REMARKS"></span>备注

使用不带参数.netsyms 显示此设置的当前状态。

使用[ **！ 符号干扰**](-sym.md)或 *-n* [ **WinDbg 命令行选项**](windbg-command-line-options.md)显示为更多详细信息加载符号。

 

 





