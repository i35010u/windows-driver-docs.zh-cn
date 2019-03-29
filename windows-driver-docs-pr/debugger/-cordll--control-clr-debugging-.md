---
title: .cordll（控制 CLR 调试）
description: .Cordll 命令控件托管代码调试和 Microsoft.NET 公共语言运行时 (CLR)。
ms.assetid: d46965b3-4f20-4e25-82e6-79e7fb9b4838
keywords:
- 控制 CLR 调试 (.cordll) 命令
- CLR （公共语言运行时）
- .cordll （控制 CLR 调试） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .cordll (Control CLR Debugging)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 74b60e1a937d8f14f0e5a8188afbcf532077c330
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564555"
---
# <a name="cordll-control-clr-debugging"></a>.cordll（控制 CLR 调试）


**.Cordll**命令控件托管代码调试和 Microsoft.NET 公共语言运行时 (CLR)。

```dbgsyntax
.cordll [Options]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *选项*   
一个或多个以下选项：

<span id="-l___lower-case_L_"></span><span id="-l___lower-case_l_"></span><span id="-L___LOWER-CASE_L_"></span>**-l** (小写 L)  
加载 CLR 调试模块。

<span id="-I_Module___upper-case_i__"></span><span id="-i_module___upper-case_i__"></span><span id="-I_MODULE___UPPER-CASE_I__"></span>**-I** **** *模块*(大写 i)   
指定的名称或要进行调试的 CLR 模块的基址。 有关详细信息，请参阅备注。

<span id="-u"></span><span id="-U"></span>**-u**  
卸载 CLR 调试模块。

<span id="-e"></span><span id="-E"></span>**-e**  
启用 CLR 调试。

<span id="-d"></span><span id="-D"></span>**-d**  
禁用 CLR 调试。

<span id="-D"></span><span id="-d"></span>**-D**  
禁用 CLR 调试和卸载 CLR 调试模块。

<span id="-N"></span><span id="-n"></span>**-N**  
重新加载 CLR 调试模块。

<span id="-lp_Path"></span><span id="-lp_path"></span><span id="-LP_PATH"></span>**-lp** **** *Path*  
指定 CLR 调试模块的目录的路径。

<span id="-se"></span><span id="-SE"></span>**-se**  
通过使用 CLR 调试模块的短名称，启用 mscordacwks.dll。

<span id="-sd"></span><span id="-SD"></span>**-sd**  
禁用通过 CLR 调试模块的短名称 mscordacwks.dll。 相反，调试器使用的长名称的 CLR 调试模块 mscordacwks\_&lt;spec&gt;.dll。 关闭短名称使用情况，可避免如果担心不匹配，则使用在本地 CLR。

<span id="-ve"></span><span id="-VE"></span>**-ve**  
开启详细模式进行加载的 CLR 模块。

<span id="-vd"></span><span id="-VD"></span>**-vd**  
关闭详细模式进行加载的 CLR 模块。

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

若要调试托管应用程序，调试器必须加载对应于应用程序已加载的 CLR 数据访问组件 (DAC)。 但是，在某些情况下，应用程序加载多个 CLR。 在这种情况下，可以使用**我**参数来指定调试器应加载哪个 DAC。 Mscorwks.dll，名为的 CLR 版本 2 和版本 4 的 CLR 名为 Clr.dll。 下面的示例演示如何指定调试器应加载 (mscorwks) 版本 2 的 DAC。

```dbgcmd
.cordll -I mscorwks -lp c:\dacFolder
```

如果省略**我**参数，调试器使用默认情况下的版本 4。 例如，以下两个命令是等效的。

```dbgcmd
.cordll -lp c:\dacFolder
.cordll -I clr -lp c:\dacFolder
```

Sos.dll 是用于调试托管的代码的组件。 有关 Windows 调试工具的当前版本不包括任何的 sos.dll 版本。 若要了解如何获取 sos.dll，请参阅[获取 SOS 调试扩展 (sos.dll)](debugging-managed-code.md#getting-the-sos-debugging-extension)。

**.Cordll**命令支持在内核模式调试。 但是，此命令可能无法运行除非必要的内存分页中。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[调试托管代码使用 Windows 调试器](debugging-managed-code.md)

[SOS 调试扩展](https://go.microsoft.com/fwlink/p/?linkid=223345)

 

 






