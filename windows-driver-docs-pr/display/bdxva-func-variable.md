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
ms.openlocfilehash: 1517826a7ea42c1f79eb0e505efdd9a9dc2b8c07
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381884"
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

-   探测，锁定为特定的 DirectX VA 函数配置。 这是通过包括**bDXVA\_Func**中**DXVA\_ConfigQueryOrReplyFlag**变量并在**DXVA\_ConfigQueryOrReplyFlag**变量发送这些变量时**dwFunction**的成员[ **DD\_RENDERMOCOMPDATA** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)对的调用中的结构[ *DdMoCompRender*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)。

-   指定与由包含在使用探测或 lock 命令传递的配置结构关联的函数**DXVA\_ConfigQueryOrReplyFlag**变量中**DXVA\_ConfigQueryOrReplyFlag**变量中发送**dwFunction**以下结构的成员：[**DXVA\_ConfigPictureDecode** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_configpicturedecode)用于压缩的图片解码[ **DXVA\_ConfigAlphaLoad** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_configalphaload)加载的alpha值混合处理数据[**DXVA\_ConfigAlphaCombine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_configalphacombine) alpha 值混合处理组合
-   初始化包含在特定的 DirectX VA 函数的加密协议**DXVA\_EncryptProtocolFunc**变量中发送**dwFunction**隶属[ **DD\_RENDERMOCOMPDATA** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)对的调用中的结构[ *DdMoCompRender*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)。

-   指定通过包含在与加密协议相关联的函数**dwFunction**的成员[ **DXVA\_EncryptProtocolHeader** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_encryptprotocolheader)结构。

-   指示包含在一系列要执行的操作**bDXVA\_Func**中的值以字节**dwFunction**隶属[ **DD\_RENDERMOCOMPDATA** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)调用中的结构[ *DdMoCompRender*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)。 第一个**bDXVA\_Func**中最高有效字节指定操作，则下一步操作中指定的下一步最高有效字节，依此类推。 剩余中的字节**dwFunction**不用于指示操作设置为零。

 

 





