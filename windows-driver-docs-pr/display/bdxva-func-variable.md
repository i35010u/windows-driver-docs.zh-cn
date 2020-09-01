---
title: bDXVA_Func 变量
description: bDXVA_Func 变量
ms.assetid: 6db9fa71-7bc2-4eb6-afcb-b16df48f7e8b
keywords:
- 视频解码 WDK DirectX VA，格式
- 解码视频 WDK DirectX VA，格式
- 图片解码 WDK DirectX VA，格式
- 格式化 WDK DirectX VA
- bDXVA_Func 变量 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3cf18e88e5d31ff70a34708676029ea825dd099
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064934"
---
# <a name="bdxva_func-variable"></a>bDXVA \_ 函数函数


## <span id="ddk_bdxva_func_variable_gg"></span><span id="DDK_BDXVA_FUNC_VARIABLE_GG"></span>


**BDXVA \_ Func**变量是一个与 DirectX VA 操作关联的8位值，如下所示。

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
<td align="left"><p>Alpha-blend 数据加载</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>Alpha-blend 组合</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>图片重新采样</p></td>
</tr>
</tbody>
</table>

 

**BDXVA \_ Func**变量用于执行以下任务：

-   探测和锁定特定 DirectX VA 功能的配置。 这是通过以下方式实现的：在**DXVA \_ ConfigQueryOrReplyFlag**变量和**DXVA \_ ConfigQueryOrReplyFlag**变量中的**bDXVA \_ 函数**中发送这些变量时，在调用[*dwFunction*](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)**的 RENDERMOCOMPDATA 成员中**发送这些变量。 [** \_ **](/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)

-   通过在以下结构的**dwFunction**成员中发送的**DXVA \_ ConfigQueryOrReplyFlag**变量中包含 DXVA ConfigQueryOrReplyFlag 变量，指定与通过探测或 lock 命令传递的配置结构相关联的函数： [**DXVA \_ ConfigPictureDecode**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode) for ** \_ ** ，用于 alpha 混合[**数据加载的 \_ **](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configalphacombine) [**DXVA ConfigAlphaLoad \_ **](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configalphaload)
-   为特定的 DirectX VA 函数初始化加密协议，方法是包含在调用[*DdMoCompRender*](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)的**dwFunction**成员中发送的**DXVA \_ EncryptProtocolFunc**变量中。 [** \_ **](/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)

-   通过包含在[**DXVA \_ EncryptProtocolHeader**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_encryptprotocolheader)结构的**dwFunction**成员中，指定与加密协议关联的函数。

-   通过在对[*DdMoCompRender*](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)的调用中包含[**DD \_ RENDERMOCOMPDATA**](/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)结构的**DwFunction**成员中的一系列**bDXVA \_ Func**字节值，通知要执行的操作。 第一个 **bDXVA \_ Func** 操作是在最重要的字节中指定的，下一个操作是在下一个最重要的字节中指定的，依此类推。 不用于给操作发出信号的 **dwFunction** 中的剩余字节数设置为零。

 

