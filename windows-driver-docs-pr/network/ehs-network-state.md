---
title: eHS_NETWORK_STATE 枚举
description: EHS_NETWORK_STATE 枚举指示网络是否是热点网络。
keywords:
- 从 Windows Vista 开始 eHS_NETWORK_STATE 枚举网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 526f8310adb8a6b345960dd2d785706a682ca10f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822994"
---
# <a name="ehs_network_state-enumeration"></a>eHS \_ 网络 \_ 状态枚举

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


**EHS \_ 网络 \_ 状态** 枚举指示网络是否是热点网络。

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
<td><p>标头</p></td>
<td>Hotspotoffloadplugin (包含 Hotspotoffloadplugin) </td>
</tr>
</tbody>
</table>

 

 




