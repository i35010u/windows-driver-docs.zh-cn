---
title: Wi-Fi 热点卸载常量
description: 本部分介绍的 Wi-fi 热点卸载框架定义的常量。
ms.assetid: F09DCB81-C9FF-493B-AE8F-97DE441A4BC3
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: c692c307188c4574bc592470b5cb36331ac8877a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365699"
---
# <a name="wi-fi-hotspot-offloading-constants"></a>Wi-Fi 热点卸载常量

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]

本部分介绍的 Wi-fi 热点卸载框架定义的常量。

<a href="" id="hs-const-host-current-api-version"></a>**HS\_CONST\_HOST\_CURRENT\_API\_VERSION**  
1  
当前的 API 版本号。

<a href="" id="hs-const-max-network-display-name-length"></a>**HS\_常量\_最大\_网络\_显示\_名称\_长度**  
32  
网络显示名称字符串的最大长度。

<a href="" id="hs-const-max-realm-length"></a>**HS\_常量\_最大\_领域\_长度**  
255  
领域值字符串的最大长度。

<a href="" id="hs-const-min-conn-keepalive-time-in-mins"></a>**HS\_常量\_MIN\_CONN\_KEEPALIVE\_时间\_IN\_分钟**  
5  
保持活动状态的消息传输之间的最小时间

<a href="" id="hs-const-profile-update-time-in-days"></a>**HS\_常量\_配置文件\_更新\_时间\_IN\_天**  
7  
配置文件更新检查之间的最短时间。

<a href="" id="hs-const-min-network-priority-value"></a>**HS\_常量\_MIN\_网络\_优先级\_值**  
1  
最低网络优先级值。

<a href="" id="hs-const-max-network-priority-value"></a>**HS\_CONST\_MAX\_NETWORK\_PRIORITY\_VALUE**  
65000  
最大网络优先级值。

<a href="" id="hs-max-phone-number-length"></a>**HS\_最大\_电话\_数\_长度**  
32  
电话号码字符串的最大长度。

<a href="" id="hs-const-max-host-name-length"></a>**HS\_常量\_最大\_主机\_名称\_长度**  
255  
主机名称字符串的最大长度。

<a href="" id="hs-const-plugin-min-rank-value"></a>**HS\_常量\_插件\_MIN\_排名\_值**  
1  
最小的排名值。 必须大于 0。

<a href="" id="hs-const-plugin-max-rank-value"></a>**HS\_常量\_插件\_最大\_排名\_值**  
250  
最大排名值。 必须小于或等于为 250。

<a href="" id="hs-const-max-provider-name-length"></a>**HS\_常量\_最大\_提供程序\_名称\_长度**  
63  
访问接口名称字符串的最大长度。

<a href="" id="hs-const-max-advanced-page-string-length"></a>**HS\_常量\_最大\_高级\_页\_字符串\_长度**  
255  
高级页字符串的最大长度。

<a href="" id="hs-const-max-phone-number-length"></a>**HS\_常量\_最大\_电话\_数\_长度**  
32  
电话号码字符串的最大长度。

<a href="" id="hs-const-max-supported-sims"></a>**HS\_常量\_最大\_支持\_SIMS**  
1000  
支持的 SIM 配置的列表的最大大小。

<a href="" id="hs-const-max-cellular-exception-hosts"></a>**HS\_CONST\_MAX\_CELLULAR\_EXCEPTION\_HOSTS**  
5  
移动电话网络承载列表的最大大小。

<a href="" id="hs-const-max-auth-error-msg-length"></a>**HS\_常量\_最大\_身份验证\_错误\_MSG\_长度**  
512  
身份验证错误消息的最大长度。

<a href="" id="hs-const-max-user-messages-in-minutes"></a>**HS\_常量\_最大\_用户\_消息\_IN\_分钟**  
7\*24\*60  
最大用户消息，以分钟为单位 （7 天）。

以下标志定义插件和宿主以分别指示其要求和功能。

<a href="" id="hs-flag-capability-network-type-visible"></a>**HS\_标志\_功能\_网络\_类型\_可见**  
0x00000001  
指定可见的网络。

<a href="" id="hs-flag-capability-network-type-hidden"></a>**HS\_FLAG\_CAPABILITY\_NETWORK\_TYPE\_HIDDEN**  
0x00000002  
指定隐藏的网络。

<a href="" id="hs-flag-capability-network-display-name"></a>**HS\_标志\_功能\_网络\_显示\_名称**  
0x00000010  
指定使用 EAP-SIM 或 EAP-AKA 身份验证的显示名称。

<a href="" id="hs-flag-capability-network-auth-no-sim"></a>**HS\_标志\_功能\_网络\_身份验证\_否\_SIM**  
0x00000100  
指定没有 SIM 身份验证。

<a href="" id="hs-flag-capability-network-auth-http"></a>**HS\_FLAG\_CAPABILITY\_NETWORK\_AUTH\_HTTP**  
0x00000200  
指定 HTTP 身份验证。

<a href="" id="hs-flag-capability-network-auth-eap-sim"></a>**HS\_标志\_功能\_网络\_身份验证\_EAP\_SIM**  
0x00001000  
指定 EAP SIM 身份验证。

<a href="" id="hs-flag-capability-network-auth-eap-aka"></a>**HS\_FLAG\_CAPABILITY\_NETWORK\_AUTH\_EAP\_AKA**  
0x00002000  
指定 EAP-AKA 身份验证。

<a href="" id="hs-flag-capability-network-auth-eap-aka-prime"></a>**HS\_FLAG\_CAPABILITY\_NETWORK\_AUTH\_EAP\_AKA\_PRIME**  
0x00004000  
指定 EAP-AKA (AKA Prime) 身份验证。

<a href="" id="hs-flag-capability-network-custom-realm"></a>**HS\_FLAG\_CAPABILITY\_NETWORK\_CUSTOM\_REALM**  
0x00010000  
指定使用网络身份验证的自定义的领域值。

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

## <a name="see-also"></a>请参阅


[卸载引用的 Wi-fi 热点](wi-fi-hotspot-offloading-reference.md)

 

 




