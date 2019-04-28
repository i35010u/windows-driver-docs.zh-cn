---
title: WDI_TLV_P2P_CONFIG_METHODS
description: WDI_TLV_P2P_CONFIG_METHODS 是 TLV 包含 Wi-Fi Direct 配置方法。
ms.assetid: 95F81FBB-CF78-47EC-8DB3-90F639C30865
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_CONFIG_METHODS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5325763ad6396b8b0872fe3ec656aca91c7f5724
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345946"
---
# <a name="wditlvp2pconfigmethods"></a>WDI\_TLV\_P2P\_CONFIG\_方法


WDI\_TLV\_P2P\_CONFIG\_方法是包含 Wi-Fi Direct 配置方法 TLV。

## <a name="tlv-type"></a>TLV 类型


0xEB

## <a name="length"></a>长度


UINT16 大小 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入   | 描述                                                                                                                                                              |
|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT16 | 配置方法中定义[ **WDI\_WPS\_配置\_方法**](https://msdn.microsoft.com/library/windows/hardware/dn898198)。 仅 PIN 显示、 PIN 键盘和 WFDS 均适用。 |

 

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

 

 




