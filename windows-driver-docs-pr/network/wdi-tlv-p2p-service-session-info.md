---
title: WDI_TLV_P2P_SERVICE_SESSION_INFO
description: WDI_TLV_P2P_SERVICE_SESSION_INFO 是包含的服务会话信息 TLV。
ms.assetid: ED1FF2F5-82BA-48AC-A986-8B75F099DCA0
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_SERVICE_SESSION_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4d6daf4f042907c9b8803cd8d57e5054ba2067a5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375649"
---
# <a name="wditlvp2pservicesessioninfo"></a>WDI\_TLV\_P2P\_服务\_会话\_信息


WDI\_TLV\_P2P\_服务\_会话\_信息是包含的服务会话信息 TLV。

## <a name="tlv-type"></a>TLV 类型


0xF0

## <a name="length"></a>长度


UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入      | 描述                  |
|-----------|------------------------------|
| UINT8\[\] | 服务的会话信息。 |

 

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

 

 




