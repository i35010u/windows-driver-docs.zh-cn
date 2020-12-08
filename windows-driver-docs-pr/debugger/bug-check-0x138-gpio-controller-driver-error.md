---
title: Bug 检查 0x138 GPIO_CONTROLLER_DRIVER_ERROR
description: GPIO_CONTROLLER_DRIVER_ERROR bug 检查的值为0x00000138。 此 bug 检查指示 GPIO 类扩展驱动程序遇到错误。
keywords:
- Bug 检查 0x138 GPIO_CONTROLLER_DRIVER_ERROR
- GPIO_CONTROLLER_DRIVER_ERROR
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- GPIO_CONTROLLER_DRIVER_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6c9914c42563a9b07df167e5d4569496ccf777a1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837355"
---
# <a name="bug-check-0x138-gpio_controller_driver_error"></a>Bug 检查0x138： GPIO \_ 控制器 \_ 驱动程序 \_ 错误


GPIO \_ 控制器 \_ 驱动程序 \_ 错误检查的值为0x00000138。 此 bug 检查指示 GPIO 类扩展驱动程序遇到错误。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="gpio_controller_driver_error-parameters"></a>GPIO \_ 控制器 \_ 驱动程序 \_ 错误参数


*参数 1* 指示违规类型。 其他参数的意义取决于 *参数 1* 的值。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 1</th>
<th align="left">参数2</th>
<th align="left">参数3</th>
<th align="left">参数4</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>GSIV</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>未注册管理特定 GSIV 的 GPIO 控制器。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>上下文值</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>客户端驱动程序为锁定或解锁请求指定了无效的上下文。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>指示是否正在请求关键转换。</p></td>
<td align="left"><p>指示由于非关键转换，银行是否已在 F1。</p></td>
<td align="left"><p>指示由于关键转换，银行是否已在 F1。</p></td>
<td align="left"><p>PoFx 请求 GPIO 控制器通过不适当的 F1 电源状态和/或关键转换发送银行。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>指示是否正在请求关键转换。</p></td>
<td align="left"><p>指示银行是否由于非关键转换而处于 F1。</p></td>
<td align="left"><p>指示银行是否由于关键转换而处于 F1。</p></td>
<td align="left"><p>PoFx 请求 GPIO 控制器通过不当 F0 电源状态和/或关键转换发送银行。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>5</p></td>
<td align="left"><p>NTSTATUS</p></td>
<td align="left"><p>GPIO 设备扩展</p></td>
<td align="left"><p>GPIO 中断参数</p></td>
<td align="left"><p>Soc GPIO 中断操作失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>6</p></td>
<td align="left"><p>NTSTATUS</p></td>
<td align="left"><p>GPIO 设备扩展</p></td>
<td align="left"><p>GPIO IO 参数</p></td>
<td align="left"><p>Soc GPIO IO 操作失败。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>7</p></td>
<td align="left"><p>修订 ID</p></td>
<td align="left"><p>函数索引</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>_DSM 方法返回了格式不正确的数据。</p></td>
</tr>
</tbody>
</table>

 

 

 




