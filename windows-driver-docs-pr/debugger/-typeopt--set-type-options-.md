---
title: .typeopt（设置类型选项）
description: Typeopt 命令设置或显示类型选项。
keywords:
- typeopt (设置类型选项) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .typeopt (Set Type Options)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6b219bc0d160adecc5b1dffa3e755ec235566b58
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838251"
---
# <a name="typeopt-set-type-options"></a>.typeopt（设置类型选项）


**Typeopt** 命令设置或显示类型选项。

```dbgcmd
.typeopt +Flags 
.typeopt -Flags 
.typeopt +FlagName 
.typeopt -FlagName 
.typeopt 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="______________"></span> **+**   
导致 *FlagName* 类型选项 (s) 指定。 *Flags*

<span id="_______-______"></span> **-**   
导致 *FlagName* *的类型* 选项 (s) 指定。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
指定要更改的类型选项。 *标志* 可以是以下任一值的总和 (没有默认) ：

<span id="0x1"></span><span id="0X1"></span>**0x1**  
将所有 "监视" 窗口和 "局部变量" 窗口中的16位无符号整数值显示为 UNICODE 数据类型。

<span id="0x2"></span><span id="0X2"></span>**0x2**  
在所有 "监视" 窗口和 "局部变量" 窗口中将已签名的32位整数值显示为默认基数中的无符号整数。

<span id="0x4"></span><span id="0X4"></span>**0x4**  
在所有 "监视" 窗口和 "局部变量" 窗口中显示所有大小的有符号整数，作为默认基数中的无符号值。

<span id="0x8"></span><span id="0X8"></span>**0x8**  
使调试器在 "局部变量" 窗口或监视窗口按名称引用符号但存在多个与此名称匹配的符号时，选择最大大小的匹配符号。 符号的大小定义如下：如果符号是函数的名称，则其大小为内存中函数的大小。 否则，符号的大小就是它所表示的数据类型的大小。

<span id="_______FlagName______"></span><span id="_______flagname______"></span><span id="_______FLAGNAME______"></span>*FlagName*   
指定要更改的类型选项。 *FlagName* 可以是下列字符串之一 (没有默认) ：

<span id="uni"></span><span id="UNI"></span>**单向**  
将所有 "监视" 窗口和 "局部变量" 窗口中的16位无符号整数值显示为 UNICODE 数据类型。  (这与 **0x1** 具有相同的效果。 ) 

<span id="longst"></span><span id="LONGST"></span>**longst**  
在所有 "监视" 窗口和 "局部变量" 窗口中将已签名的32位整数值显示为默认基数中的无符号整数。  (这与 **0x2** 具有相同的效果。 ) 

<span id="radix"></span><span id="RADIX"></span>**基数**  
在所有 "监视" 窗口和 "局部变量" 窗口中显示所有大小的有符号整数，作为默认基数中的无符号值。  (这与 **0x4** 具有相同的效果。 ) 

<span id="size"></span><span id="SIZE"></span>**规格**  
使调试器在 "局部变量" 窗口或监视窗口按名称引用符号但存在多个与此名称匹配的符号时，选择最大大小的匹配符号。 符号的大小定义如下：如果符号是函数的名称，则其大小为内存中函数的大小。 否则，符号的大小就是它所表示的数据类型的大小。  (这与 **0x8** 具有相同的效果。 ) 

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

 

<a name="remarks"></a>备注
-------

如果没有任何参数， **. typeopt** 将显示当前的符号选项。

若要更改默认基数，请使用 [**n (设置 Number Base)**](n--set-number-base-.md) 命令。

 





