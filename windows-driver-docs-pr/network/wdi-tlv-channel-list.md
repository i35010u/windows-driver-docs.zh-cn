---
title: WDI_TLV_CHANNEL_LIST
description: WDI_TLV_CHANNEL_LIST 是包含一个或多个频道号 TLV。
ms.assetid: DBBA28C2-D80F-409B-BEE6-81B6FEDF7484
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CHANNEL_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 19d8a03559bcf38dca4b7e606a2ef0d94ff48e42
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357261"
---
# <a name="wditlvchannellist"></a>WDI\_TLV\_通道\_列表


WDI\_TLV\_通道\_列表是包含一个或多个频道号 TLV。

## <a name="tlv-type"></a>TLV 类型


0x4

## <a name="length"></a>长度


数组的大小 （以字节为单位） [ **WDI\_通道\_映射\_条目**](https://msdn.microsoft.com/library/windows/hardware/dn897799)结构。 该数组必须包含一个或多个结构。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                       | 描述                          |
|----------------------------------------------------------------------------|--------------------------------------|
| [**WDI\_通道\_映射\_条目**](https://msdn.microsoft.com/library/windows/hardware/dn897799)\[\] | 通道映射项的数组。 |

 

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

 

 




