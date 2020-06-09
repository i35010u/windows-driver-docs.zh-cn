---
title: .cordll（控制 CLR 调试）
description: Cordll 命令控制托管代码调试和 Microsoft .NET 公共语言运行时（CLR）。
ms.assetid: d46965b3-4f20-4e25-82e6-79e7fb9b4838
keywords:
- Control CLR 调试（. cordll）命令
- CLR （公共语言运行时）
- 。 cordll （控件 CLR 调试） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .cordll (Control CLR Debugging)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 174b7bea404ef5240d74d16f5403cd60ac1e28e4
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534238"
---
# <a name="cordll-control-clr-debugging"></a>.cordll（控制 CLR 调试）

**Cordll**命令控制托管代码调试和 Microsoft .NET 公共语言运行时（CLR）。

```dbgsyntax
.cordll [Options]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters

<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*选项*   
以下一个或多个选项：

<span id="-l___lower-case_L_"></span><span id="-l___lower-case_l_"></span><span id="-L___LOWER-CASE_L_"></span>**-l** （小写 l）  
加载 CLR 调试模块。

<span id="-I_Module___upper-case_i__"></span><span id="-i_module___upper-case_i__"></span><span id="-I_MODULE___UPPER-CASE_I__"></span>**-I**  **** *模块*（大写 i）   
指定要调试的 CLR 模块的名称或基址。 有关详细信息，请参阅“备注”。

<span id="-u"></span><span id="-U"></span>**-u**  
卸载 CLR 调试模块。

<span id="-e"></span><span id="-E"></span>**-e**  
启用 CLR 调试。

<span id="-d"></span><span id="-D"></span>**-d.ddd...e**  
禁用 CLR 调试。

<span id="-D"></span><span id="-d"></span>**-D**  
禁用 CLR 调试和卸载 CLR 调试模块。

<span id="-N"></span><span id="-n"></span>**-N**  
重新加载 CLR 调试模块。

<span id="-lp_Path"></span><span id="-lp_path"></span><span id="-LP_PATH"></span>**-lp**  **** *路径*  
指定 CLR 调试模块的目录路径。

<span id="-se"></span><span id="-SE"></span>**-se**  
使用 CLR 调试模块 mscordacwks 的短名称启用。

<span id="-sd"></span><span id="-SD"></span>**-sd**  
禁用使用 CLR 调试模块 mscordacwks 的短名称。 相反，调试器使用 CLR 调试模块的长名称 mscordacwks \_ &lt; &gt; 。 如果你担心不匹配，则关闭短名称用法可使你避免使用本地 CLR。

<span id="-ve"></span><span id="-VE"></span>**-ve**  
打开 CLR 模块加载的详细模式。

<span id="-vd"></span><span id="-VD"></span>**-wb2-vd-lq4**  
关闭 CLR 模块加载的详细模式。

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

 

<a name="remarks"></a>注解
-------

若要调试托管应用程序，调试器必须加载与应用程序已加载的 CLR 相对应的数据访问组件（DAC）。 但是，在某些情况下，应用程序会加载多个 CLR。 在这种情况下，可以使用**I**参数指定调试器应加载的 DAC。 CLR 的版本2命名为 Mscorwks.dll，并且 CLR 的版本4命名为 Clr。 下面的示例演示如何指定调试器应为版本2（mscorwks.dll）加载 DAC。

```dbgcmd
.cordll -I mscorwks -lp c:\dacFolder
```

如果省略**I**参数，则默认情况下，调试器使用版本4。 例如，以下两个命令是等效的。

```dbgcmd
.cordll -lp c:\dacFolder
.cordll -I clr -lp c:\dacFolder
```

Sos 是用于调试托管代码的组件。 当前版本的 Windows 调试工具不包括任何版本的 sos。 有关如何获取 sos 的信息，请参阅[使用 Windows 调试器调试托管代码](debugging-managed-code.md)中*的获取 sos 调试扩展（sos）* 。

内核模式调试支持**cordll**命令。 但是，除非在中分页了所需的内存，否则此命令可能不起作用。

## <a name="see-also"></a>另请参阅

[使用 Windows 调试器调试托管代码](debugging-managed-code.md)

[SOS 调试扩展](https://docs.microsoft.com/dotnet/framework/tools/sos-dll-sos-debugging-extension)
