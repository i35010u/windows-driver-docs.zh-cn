---
title: bDXVA_Func 变量
description: bDXVA_Func 变量
ms.assetid: 6db9fa71-7bc2-4eb6-afcb-b16df48f7e8b
keywords:
- 视频解码 WDK DirectX VA，格式
- 解码视频 WDK DirectX VA，格式
- 解码 WDK DirectX va，因此格式的图片
- 格式 WDK DirectX VA
- bDXVA_Func 变量 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92174b1651c0da6fc2ec8496930572a716848ee4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346989"
---
# <a name="bdxvafunc-variable"></a>bDXVA\_Func 变量


## <span id="ddk_bdxva_func_variable_gg"></span><span id="DDK_BDXVA_FUNC_VARIABLE_GG"></span>


**BDXVA\_Func**变量是一个 8 位值，是与 DirectX VA 操作相关联，如下所示。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">bDXVA_Func 值</th>
<th align="left">操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>压缩的图片解码</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>Alpha 混合数据加载</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>Alpha 混合组合</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>图片来重新采样</p></td>
</tr>
</tbody>
</table>

 

**BDXVA\_Func**变量用于执行以下任务：

-   探测，锁定为特定的 DirectX VA 函数配置。 这是通过包括**bDXVA\_Func**中**DXVA\_ConfigQueryOrReplyFlag**变量并在**DXVA\_ConfigQueryOrReplyFlag**变量发送这些变量时**dwFunction**的成员[ **DD\_RENDERMOCOMPDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551693)对的调用中的结构[ *DdMoCompRender*](https://msdn.microsoft.com/library/windows/hardware/ff550248)。

-   指定与由包含在使用探测或 lock 命令传递的配置结构关联的函数**DXVA\_ConfigQueryOrReplyFlag**变量中**DXVA\_ConfigQueryOrReplyFlag**变量中发送**dwFunction**以下结构的成员：[**DXVA\_ConfigPictureDecode** ](https://msdn.microsoft.com/library/windows/hardware/ff563133)用于压缩的图片解码[ **DXVA\_ConfigAlphaLoad** ](https://msdn.microsoft.com/library/windows/hardware/ff563129)加载的alpha值混合处理数据[**DXVA\_ConfigAlphaCombine** ](https://msdn.microsoft.com/library/windows/hardware/ff563126) alpha 值混合处理组合
-   初始化包含在特定的 DirectX VA 函数的加密协议**DXVA\_EncryptProtocolFunc**变量中发送**dwFunction**隶属[ **DD\_RENDERMOCOMPDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551693)对的调用中的结构[ *DdMoCompRender*](https://msdn.microsoft.com/library/windows/hardware/ff550248)。

-   指定通过包含在与加密协议相关联的函数**dwFunction**的成员[ **DXVA\_EncryptProtocolHeader** ](https://msdn.microsoft.com/library/windows/hardware/ff563965)结构。

-   指示包含在一系列要执行的操作**bDXVA\_Func**中的值以字节**dwFunction**隶属[ **DD\_RENDERMOCOMPDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551693)调用中的结构[ *DdMoCompRender*](https://msdn.microsoft.com/library/windows/hardware/ff550248)。 第一个**bDXVA\_Func**中最高有效字节指定操作，则下一步操作中指定的下一步最高有效字节，依此类推。 剩余中的字节**dwFunction**不用于指示操作设置为零。

 

 





