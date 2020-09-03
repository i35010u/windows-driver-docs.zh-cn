---
title: eHS_NETWORK_STATE 枚举
description: EHS_NETWORK_STATE 枚举指示网络是否是热点网络。
ms.assetid: a833d226-e2cf-41f9-a926-5b1f6daa03af
keywords:
- 从 Windows Vista 开始 eHS_NETWORK_STATE 枚举网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5477e08e77924d379d8886628605b3ae6d78de0c
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403542"
---
# <a name="ehs_network_state-enumeration"></a>eHS \_ 网络 \_ 状态枚举

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


**EHS \_ 网络 \_ 状态**枚举指示网络是否是热点网络。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef enum _eHS_NETWORK_STATE { 
  HS_NETWORK_STATE_NOT_A_HOTSPOT,
  HS_NETWORK_STATE_HOTSPOT_MANUAL_CONNECT,
  HS_NETWORK_STATE_HOTSPOT_AUTO_CONNECT,
  HS_NETWORK_STATE_MAX
} eHS_NETWORK_STATE;
```

<a name="constants"></a>常量
---------

<a href="" id="hs-network-state-not-a-hotspot"></a>**HS \_ 网络 \_ 状态 \_ 不 \_ 是 \_ 热点**  
指示网络不是热点网络。

<a href="" id="hs-network-state-hotspot-manual-connect"></a>**HS \_ 网络 \_ 状态 \_ 热点 \_ 手动 \_ 连接**  
指示用户可以手动连接到热点网络。

<a href="" id="hs-network-state-hotspot-auto-connect"></a>**HS \_ 网络 \_ 状态 \_ 热点 \_ 自动 \_ 连接**  
指示设备可以自动连接到热点网络。

<a href="" id="hs-network-state-max"></a>**HS \_ 网络 \_ 状态 \_ 最大值**  
指示超出范围值。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>Windows 10 移动版</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Hotspotoffloadplugin (包含 Hotspotoffloadplugin) </td>
</tr>
</tbody>
</table>

 

 




