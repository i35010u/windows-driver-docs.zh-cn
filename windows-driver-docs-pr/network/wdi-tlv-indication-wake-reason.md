---
title: WDI_TLV_INDICATION_WAKE_REASON
description: WDI_TLV_INDICATION_WAKE_REASON 是包含 NDIS_STATUS_WDI_INDICATION_WAKE_REASON 唤醒原因 TLV。
ms.assetid: 3D3F93EA-4733-44FC-9CB3-721F0552F3E2
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_INDICATION_WAKE_REASON 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 883f368ed0da138f079f9657697f22ebc094f254
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361751"
---
# <a name="wditlvindicationwakereason"></a>WDI\_TLV\_指示\_唤醒\_原因


WDI\_TLV\_指示\_唤醒\_原因是包含唤醒原因 TLV [NDIS\_状态\_WDI\_指示\_唤醒\_原因](https://msdn.microsoft.com/library/windows/hardware/dn925669)。

## <a name="tlv-type"></a>TLV 类型


0x9C

## <a name="length"></a>长度


UINT32 大小 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入   | 描述                |
|--------|----------------------------|
| UINT32 | 指定唤醒原因。 |

 

有效唤醒原因的值为：

| 唤醒原因                                       | ReplTest1  | 描述                                                                                                          |
|---------------------------------------------------|--------|----------------------------------------------------------------------------------------------------------------------|
| WDI\_唤醒\_原因\_代码\_数据包                   | 0x0001 | 接收的数据包与唤醒模式匹配。                                                                          |
| WDI\_唤醒\_原因\_代码\_媒体\_断开连接        | 0x0002 | 媒体断开连接。                                                                                                 |
| WDI\_唤醒\_原因\_代码\_媒体\_连接           | 0x0003 | 媒体连接。                                                                                                    |
| WDI\_唤醒\_原因\_代码\_NLO\_发现           | 0x1000 | NLO 发现。                                                                                                       |
| WDI\_唤醒\_原因\_代码\_AP\_关联\_丢失    | 0x1001 | 访问点关联丢失。                                                                                       |
| WDI\_唤醒\_原因\_代码\_GTK\_握手\_错误    | 0x1002 | GTK 握手时出错。                                                                                                 |
| WDI\_唤醒\_原因\_代码\_4 道\_握手\_请求 | 0x1003 | 4 路握手请求。                                                                                             |
| WDI\_唤醒\_原因\_代码\_EAPID\_请求           | 0x1004 | 保留供将来使用。                                                                                             |
| WDI\_唤醒\_原因\_代码\_传入\_M1           | 0x1005 | 使用 WDI\_唤醒\_原因\_代码\_4 道\_握手\_改为请求。                                                       |
| WDI\_唤醒\_原因\_代码\_固件\_STALLED        | 0x1010 | 固件挂起 （例如，通过监视程序计时器） 检测到并唤醒逻辑仍正常运转唤醒主机。 |
| WDI\_唤醒\_原因\_代码\_GTK\_握手\_请求  | 0x1020 | 组键重新生成密钥的请求。                                                                                             |

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




