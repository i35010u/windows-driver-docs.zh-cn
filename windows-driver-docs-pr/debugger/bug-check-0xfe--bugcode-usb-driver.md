---
title: Bug 检查 0xFE BUGCODE_USB_DRIVER
description: BUGCODE_USB_DRIVER bug 检查的值为0x000000FE。 这表明 (USB) 驱动程序的通用串行总线出现错误。
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
ms.openlocfilehash: 0ba6ac112bb4ee999e9f8c17749acc2e80d3855c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836887"
---
# <a name="bug-check-0xfe-bugcode_usb_driver"></a>Bug 检查0xFE： BUGCODE \_ USB \_ 驱动程序


BUGCODE \_ USB \_ 驱动程序 bug 检查的值为0x000000FE。 这表明 (USB) 驱动程序的通用串行总线出现错误。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="bugcode_usb_driver-parameters"></a>BUGCODE \_ USB \_ 驱动程序参数


四个 bug 检查参数显示在 bug 检查停止屏幕上，并可使用！分析。 参数1标识冲突类型。

| 参数 1 | 参数2 | 参数3 | 参数4 | 错误的原因                            | 
|-------------|-------------|-------------|-------------|-------------------------------------------|
| 0x1 | 预留 | 预留 | 预留 | USB 堆栈中出现内部错误。 |
| 0x2 | 挂起 IRP 的地址 | 传入的 IRP 的地址| 导致错误的 USB 请求块 (URB) 的地址 | USB 客户端驱动程序已提交 URB，该连接仍附加到在总线驱动程序中挂起的另一个 IRP。| 
|0x3| 预留 | 预留| 预留| USB 微型端口驱动程序已生成 bug 检查。 发生这种情况时，通常会出现硬件故障。|
| 0x4 | IRP 的地址| URB 的地址| 预留| 调用方提交了已在 USB 总线驱动程序中挂起的 IRP。| 
| 0x5| 主机控制器的设备扩展指针| PCI 供应商，控制器的产品 id| 指向终结点数据结构的指针| 由于在硬件数据结构中发现了错误的物理地址，导致硬件故障。| 
| 0x6 | 对象地址| 预期的签名| 预留 | 内部数据结构 (对象) 已损坏。|
| 0x7 | 指向 usbport.sys 调试日志的指针 | 消息字符串 | 文件名 | 有关详细信息，请参阅提供的消息字符串。|
| 0x8 | 1 | 预留 | 预留 | 预留 |
| | 2 | 设备对象  | IRP | 缺少 IRP 的集线器驱动程序已收到 IRP，或未对其进行注册。 |
| | 3 | 预留 | 预留 | 预留
| | 4 | 如果参数3不为 NULL，则为 PDO。 如果参数3为 NULL，则为上下文。 | 上下文或 NULL | 严重的 PDO 陷阱
| | 5 | 预留 | 预留 | 预留 |
| | 6 | 超时代码。 请参阅下表。 | 超时代码上下文：端口数据 | 严重超时

如果参数1的值为8，并且参数2的值为6，则参数3为超时代码。 下表中给出了超时代码的可能值。

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
<td align="left"><p>恢复暂停的端口失败。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>等待由客户端驱动程序启动的重置超时，在挂起端口前完成。</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p>等待端口完成恢复，然后再将其挂起。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>4</p></td>
<td align="left"><p>等待在挂起端口之前禁用端口更改状态机超时。</p></td>
</tr>
<tr class="even">
<td align="left"><p>5</p></td>
<td align="left"><p>等待挂起端口请求完成时超时。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>6</p></td>
<td align="left"><p>等待禁用端口更改状态计算机时超时。</p></td>
</tr>
<tr class="even">
<td align="left"><p>7</p></td>
<td align="left"><p>等待端口更改状态机关闭时超时。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>8</p></td>
<td align="left"><p>等待集线器从选择性挂起状态恢复超时。</p></td>
</tr>
<tr class="even">
<td align="left"><p>9</p></td>
<td align="left"><p>等待中心从选择性挂起恢复到系统挂起之前已超时。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>10</p></td>
<td align="left"><p>等待端口更改状态机处于空闲状态时超时。</p></td>
</tr>
</tbody>
</table>

## <a name="resolution"></a>解决方法

[**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。
 
 

 




