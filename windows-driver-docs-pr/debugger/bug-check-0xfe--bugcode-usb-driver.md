---
title: Bug 检查 0xFE BUGCODE_USB_DRIVER
description: BUGCODE_USB_DRIVER bug 检查具有 0x000000FE 值。 这指示错误发生在通用串行总线 (USB) 驱动程序。
ms.assetid: 830f9d11-4b16-41a9-a804-6d689a779278
keywords:
- Bug 检查 0xFE BUGCODE_USB_DRIVER
- BUGCODE_USB_DRIVER
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- BUGCODE_USB_DRIVER
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d32c731d9260ad074a1bfed4e66d04882a252d3e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361477"
---
# <a name="bug-check-0xfe-bugcodeusbdriver"></a>Bug 检查 0xFE：BUGCODE\_USB\_DRIVER


BUGCODE\_USB\_驱动程序 bug 检查的值为 0x000000FE。 这指示错误发生在通用串行总线 (USB) 驱动程序。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)。


## <a name="bugcodeusbdriver-parameters"></a>BUGCODE\_USB\_驱动程序参数


四个 bug 检查参数显示在错误检查停止屏幕并可使用 ！ 分析。 参数 1 标识冲突的类型。

| 参数 1 | 参数 2 | 参数 3 | 参数 4 | 错误的原因                            | 
|-------------|-------------|-------------|-------------|-------------------------------------------|
| 0x1 | 保留 | 保留 | 保留 | USB 堆栈中发生内部错误。 |
| 0x2 | 挂起的 IRP 的地址 | 传入的 IRP 的地址| USB 请求块 (URB) 导致了错误地址 | USB 客户端驱动程序已提交仍附加到挂起的总线驱动程序中的另一个 IRP URB。| 
|0x3| 保留 | 保留| 保留| USB 微型端口驱动程序已生成的 bug 检查。 这通常发生硬件故障的响应中。|
| 0x4 | IRP 的地址| URB 的地址| 保留| 调用方已提交操作已被挂起 IRP USB 总线驱动程序中。| 
| 0x5| 设备扩展的主控制器的指针| PCI 供应商，为控制器的产品 id| 指向终结点数据结构| 由于硬件数据结构中找到的错误的物理地址出现硬件故障。| 
| 0x6 | 对象地址| 应有的签名| 保留 | 内部数据结构 （对象） 已损坏。|
| 0x7 | 指向 usbport.sys 调试日志 | 消息字符串 | 文件名 | 请参阅提供的消息字符串的详细信息。|
| 0x8 | 1 | 保留 | 保留 | 保留 |
| | 2 | 设备对象  | IRP | 它不需要或尚未注册的中心驱动程序接收 IRP。 |
| | 3 | 保留 | 保留 | 保留
| | 4 | PDO 如果参数 3 不为 NULL。 如果参数 3 为 NULL 的上下文。 | 上下文或 NULL | 致命 PDO 陷阱
| | 5 | 保留 | 保留 | 保留 |
| | 6 | 超时代码。 请参阅下表。 | 超时代码上下文： 端口数据 | 致命超时

如果参数 1 的值为 8，参数 2 的值为 6，参数 3 是超时代码。 下表给出了超时代码的可能值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">超时代码</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>非致命超时</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>失败恢复挂起的端口。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>超时等待重置，由客户端驱动程序，启动完成，然后挂起该端口。</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p>等待要完成恢复之前暂停它的端口时超时。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>4</p></td>
<td align="left"><p>等待要挂起端口之前禁用的端口更改状态机超时。</p></td>
</tr>
<tr class="even">
<td align="left"><p>5</p></td>
<td align="left"><p>等待完成的挂起端口请求超时。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>6</p></td>
<td align="left"><p>等待要禁用的端口更改状态机超时。</p></td>
</tr>
<tr class="even">
<td align="left"><p>7</p></td>
<td align="left"><p>等待要关闭的端口更改状态机超时。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>8</p></td>
<td align="left"><p>操作已超时等待中心继续从选择性挂起。</p></td>
</tr>
<tr class="even">
<td align="left"><p>9</p></td>
<td align="left"><p>操作已超时等待中心继续从选择性挂起之前系统挂起。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>10</p></td>
<td align="left"><p>等待端口更改状态机进入空闲状态时超时。</p></td>
</tr>
</tbody>
</table>

## <a name="resolution"></a>分辨率

[ **！ 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)调试扩展显示有关错误检查的信息，有助于在确定根本原因。
 
 

 




