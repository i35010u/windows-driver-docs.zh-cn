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
ms.openlocfilehash: b538fb2e2e9d7a276b9c264872e2b1af0c57d437
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839068"
---
# <a name="bdxva_func-variable"></a>bDXVA\_Func 变量


## <span id="ddk_bdxva_func_variable_gg"></span><span id="DDK_BDXVA_FUNC_VARIABLE_GG"></span>


**BDXVA\_Func**变量是一个与 DirectX VA 操作相关联的8位值，如下所示。

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

 

**BDXVA\_Func**变量用于执行以下任务：

-   探测和锁定特定 DirectX VA 功能的配置。 为此，可在**DXVA\_ConfigQueryOrReplyFlag**变量中包含**bDXVA\_Func** ，并在**DXVA\_ConfigQueryOrReplyFlag**变量中添加这些变量，这是因为在调用[*DwFunction*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)时， [ **\_RENDERMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)结构的**DdMoCompRender**成员中发送这些变量。

-   通过在以下结构的**dwFunction**成员中发送的 DXVA\_ConfigQueryOrReplyFlag 变量中包含**DXVA\_ConfigQueryOrReplyFlag**变量，指定与通过探测或 lock 命令传递的配置结构相关联的函数： [**DXVA\_ConfigPictureDecode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)\_for [ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configalphacombine) [**DXVA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configalphaload)alpha 混合组合
-   为特定的 DirectX VA 函数初始化加密协议，方法是包含在调用[*DdMoCompRender*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)的**DXVA\_EncryptProtocolFunc**变量中，该变量在[**DD\_RENDERMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)结构的**dwFunction**成员中发送。

-   通过包含在[**DXVA\_EncryptProtocolHeader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_encryptprotocolheader)结构的**dwFunction**成员中，指定与加密协议关联的函数。

-   通过在对[*DdMoCompRender*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)的调用中包含[**DD\_RENDERMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)结构的**dwFunction**成员中的一系列**bDXVA\_Func**字节值，通知要执行的操作。 第一个**bDXVA\_Func**操作是在最重要的字节中指定的，下一个操作是在下一个最重要的字节中指定，依此类推。 不用于给操作发出信号的**dwFunction**中的剩余字节数设置为零。

 

 





