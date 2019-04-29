---
title: eHS_NETWORK_STATE 枚举
description: EHS_NETWORK_STATE 枚举指示网络是否热点网络。
ms.assetid: a833d226-e2cf-41f9-a926-5b1f6daa03af
keywords:
- 与 Windows Vista 一起启动的网络驱动程序的 eHS_NETWORK_STATE 枚举
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0e258c385af2e7dcce00d736219fca8895140dc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372573"
---
# <a name="ehsnetworkstate-enumeration"></a>eHS\_网络\_状态枚举

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**EHS\_网络\_状态**枚举指示网络是否热点网络。

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

<a href="" id="hs-network-state-not-a-hotspot"></a>**HS\_网络\_状态\_不\_A\_热点**  
指示网络不会热点网络。

<a href="" id="hs-network-state-hotspot-manual-connect"></a>**HS\_网络\_状态\_热点\_手动\_连接**  
指示用户可以手动连接到热点网络。

<a href="" id="hs-network-state-hotspot-auto-connect"></a>**HS\_网络\_状态\_热点\_自动\_连接**  
指示该设备可以自动连接到热点网络。

<a href="" id="hs-network-state-max"></a>**HS\_NETWORK\_STATE\_MAX**  
指示一个范围外的值。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>Windows 10 移动版</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Hotspotoffloadplugin.h （包括 Hotspotoffloadplugin.h）</td>
</tr>
</tbody>
</table>

 

 




