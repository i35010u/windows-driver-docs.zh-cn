---
title: Wi-Fi 热点卸载常量
description: 本节介绍为 Wi-Fi 热点卸载框架定义的常量。
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39ae841a8f8bbffa5233e8bd38e0b70a50c0117e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821879"
---
# <a name="wi-fi-hotspot-offloading-constants"></a>Wi-Fi 热点卸载常量

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]

本节介绍为 Wi-Fi 热点卸载框架定义的常量。

<a href="" id="hs-const-host-current-api-version"></a>**HS \_ CONST \_ HOST \_ 当前 \_ API \_ 版本**  
1  
当前 API 版本号。

<a href="" id="hs-const-max-network-display-name-length"></a>**HS \_ CONST \_ MAX \_ 网络 \_ 显示 \_ 名称 \_ 长度**  
32  
网络显示名称字符串的最大长度。

<a href="" id="hs-const-max-realm-length"></a>**HS \_ CONST \_ MAX \_ 领域 \_ 长度**  
255  
领域值字符串的最大长度。

<a href="" id="hs-const-min-conn-keepalive-time-in-mins"></a>**HS \_ CONST \_ MIN \_ CONN \_ 生存 \_ 时间 \_ （ \_ 分钟）**  
5  
保持活动消息传输间隔的最小时间

<a href="" id="hs-const-profile-update-time-in-days"></a>**HS \_ CONST \_ PROFILE \_ 更新 \_ 时间 \_ （ \_ 天）**  
7  
检查配置文件更新之间的最短时间。

<a href="" id="hs-const-min-network-priority-value"></a>**HS \_ CONST \_ MIN \_ 网络 \_ 优先级 \_ 值**  
1  
最小网络优先级值。

<a href="" id="hs-const-max-network-priority-value"></a>**HS \_ CONST \_ MAX \_ 网络 \_ 优先级 \_ 值**  
65000  
最大网络优先级值。

<a href="" id="hs-max-phone-number-length"></a>**HS \_ 最大 \_ 电话 \_ 号码 \_ 长度**  
32  
电话号码字符串的最大长度。

<a href="" id="hs-const-max-host-name-length"></a>**HS \_ CONST \_ MAX \_ 主机 \_ 名 \_ 长度**  
255  
主机名称字符串的最大长度。

<a href="" id="hs-const-plugin-min-rank-value"></a>**HS \_ 常量 \_ 插件 \_ 最小 \_ 排名 \_ 值**  
1  
最小排名值。 必须大于 0。

<a href="" id="hs-const-plugin-max-rank-value"></a>**HS \_ 常量 \_ 插件 \_ 最大 \_ 排名 \_ 值**  
250  
最大排名值。 必须小于或等于250。

<a href="" id="hs-const-max-provider-name-length"></a>**HS \_ 常量 \_ 最大 \_ 提供程序 \_ 名称 \_ 长度**  
63  
提供程序名称字符串的最大长度。

<a href="" id="hs-const-max-advanced-page-string-length"></a>**HS \_ CONST \_ MAX \_ 高级 \_ 页 \_ 字符串 \_ 长度**  
255  
高级页字符串的最大长度。

<a href="" id="hs-const-max-phone-number-length"></a>**HS \_ CONST \_ 最大 \_ 电话 \_ 号码 \_ 长度**  
32  
电话号码字符串的最大长度。

<a href="" id="hs-const-max-supported-sims"></a>**HS \_ CONST \_ MAX \_ 支持的 \_ SIM**  
1000  
支持的 SIM 配置列表的最大大小。

<a href="" id="hs-const-max-cellular-exception-hosts"></a>**HS \_ CONST \_ MAX \_ 手机 \_ 例外 \_ 主机**  
5  
移动电话 bearers 列表的最大大小。

<a href="" id="hs-const-max-auth-error-msg-length"></a>**HS \_ CONST \_ MAX \_ AUTHENTICATION \_ 错误 \_ 消息 \_ 长度**  
512  
身份验证错误消息的最大长度。

<a href="" id="hs-const-max-user-messages-in-minutes"></a>**HS \_ CONST \_ MAX \_ 用户 \_ 消息 \_ \_ （分钟）**  
7 \* 24 \* 60  
最大用户消息 (7 天) ，以分钟为单位。

为插件和宿主定义了下列标志，分别指示它们的要求和功能。

<a href="" id="hs-flag-capability-network-type-visible"></a>**HS \_ 标志 \_ 功能 \_ 网络 \_ 类型 \_ 可见**  
0x00000001  
指定可见网络。

<a href="" id="hs-flag-capability-network-type-hidden"></a>**HS \_ 标志 \_ 功能 \_ 网络 \_ 类型 \_ 隐藏**  
0x00000002  
指定隐藏网络。

<a href="" id="hs-flag-capability-network-display-name"></a>**HS \_ 标志 \_ 功能 \_ 网络 \_ 显示 \_ 名称**  
0x00000010  
指定将显示名称用于 EAP-SIM 或 EAP 身份验证。

<a href="" id="hs-flag-capability-network-auth-no-sim"></a>**HS \_ 标志 \_ 功能 \_ 网络 \_ 身份验证 \_ 无 \_ SIM**  
0x00000100  
指定无 SIM 身份验证。

<a href="" id="hs-flag-capability-network-auth-http"></a>**HS \_ 标志 \_ 功能 \_ 网络 \_ 身份验证 \_ HTTP**  
0x00000200  
指定 HTTP 身份验证。

<a href="" id="hs-flag-capability-network-auth-eap-sim"></a>**HS \_ 标志 \_ 功能 \_ 网络 \_ 身份验证 \_ EAP \_ SIM**  
0x00001000  
指定 EAP-SIM 身份验证。

<a href="" id="hs-flag-capability-network-auth-eap-aka"></a>**HS \_ 标志 \_ 功能 \_ 网络 \_ 身份验证 \_ EAP \_ 称为**  
0x00002000  
指定 EAP 身份验证。

<a href="" id="hs-flag-capability-network-auth-eap-aka-prime"></a>**HS \_ 标志 \_ 功能 \_ 网络 \_ 身份验证 \_ EAP \_ 称为 \_ 质数**  
0x00004000  
指定 EAP " (也称为" 质数) authentication "。

<a href="" id="hs-flag-capability-network-custom-realm"></a>**HS \_ 标志 \_ 功能 \_ 网络 \_ 自定义 \_ 领域**  
0x00010000  
指定使用自定义领域值进行网络身份验证。

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

## <a name="see-also"></a>请参阅


[Wi-Fi 热点卸载参考](wi-fi-hotspot-offloading-reference.md)

 

 




