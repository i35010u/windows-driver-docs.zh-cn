---
title: eHS_UNLOAD_REASON 枚举
description: EHS_UNLOAD_REASON 枚举指示插件以被卸载的原因。
ms.assetid: 1e658dd3-f66d-4803-ad3c-84bfa1890a86
keywords:
- 与 Windows Vista 一起启动的网络驱动程序的 eHS_UNLOAD_REASON 枚举
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce0db9474ca5f9c714bc396503549020004714cd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372547"
---
# <a name="ehsunloadreason-enumeration"></a>eHS\_UNLOAD\_原因枚举

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**EHS\_UNLOAD\_原因**枚举指示插件以被卸载的原因。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef enum _eHS_UNLOAD_REASON { 
  HS_UNLOAD_REASON_NONE,
  HS_UNLOAD_REASON_PLUGN_INIT_FAILED,
  HS_UNLOAD_REASON_NO_NETWORKS_SUPPORTED,
  HS_UNLOAD_REASON_NO_PROVIDE_NAME_ID,
  HS_UNLOAD_REASON_ZERO_SIM_COUNT,
  HS_UNLOAD_REASON_DISPLAY_FLAG_BUT_NO_DISPLAY_STRING_ID,
  HS_UNLOAD_REASON_CUSTOM_REALM_FLAG_BUT_NO_REALM_STRING,
  HS_UNLOAD_REASON_DUPLICATE_PLUGIN_LOADED,
  HS_UNLOAD_REASON_RELOAD_REQUESTED_BY_PLUGIN,
  HS_UNLOAD_REASON_EXCEPTION_DURING_PLUGIN_CALL,
  HS_UNLOAD_REASON_EXCEPTION_IN_PLUGIN_HOST,
  HS_UNLOAD_REASON_ASYNC_INITIALIZATION_FAILED,
  HS_UNLOAD_REASON_UNSUPPORTED_AUTH_CAPABILITY_REQUESTED,
  HS_UNLOAD_REASON_FAILED_TO_LOAD_PROVIDER_NAME_STRING,
  HS_UNLOAD_REASON_FAILED_TO_LOAD_ADVANCED_PAGE_STRING,
  HS_UNLOAD_REASON_FAILED_TO_LOAD_NETWORK_NAME_STRING,
  HS_UNLOAD_REASON_FAILED_TO_CONFIGURE_HIDDEN_NETWORK,
  HS_UNLOAD_REASON_HIDDEN_NETWORK_ALREADY_CONFIGURED,
  HS_UNLOAD_REASON_FAILED_TO_QUERY_SIMS,
  HS_UNLOAD_REASON_PLUGIN_REQUIRED_SIM_NOT_PRESENT,
  HS_UNLOAD_REASON_SIM_CONFIG_CHANGED,
  HS_UNLOAD_REASON_WIFI_SWITCHED_OFF_IN_OS,
  HS_UNLOAD_REASON_MAX
} eHS_UNLOAD_REASON;
```

<a name="constants"></a>常量
---------

<a href="" id="hs-unload-reason-none"></a>**HS\_UNLOAD\_原因\_NONE**  
卸载操作没有明确的理由。

<a href="" id="hs-unload-reason-plugn-init-failed"></a>**HS\_UNLOAD\_原因\_PLUGN\_INIT\_失败**  
插件是正在卸载，因为它无法成功初始化。

<a href="" id="hs-unload-reason-no-networks-supported"></a>**HS\_UNLOAD\_原因\_否\_网络\_支持**  
由于正在卸载插件的插件[ **HS\_插件\_配置文件**](hs-plugin-profile.md)结构未指明的有效值**dwNumNetworksSupported**.

<a href="" id="hs-unload-reason-no-provide-name-id"></a>**HS\_UNLOAD\_原因\_否\_提供\_名称\_ID**  
由于正在卸载插件的插件[ **HS\_插件\_配置文件**](hs-plugin-profile.md)结构未指定的字符串 ID **dwProviderNameStringID**.

<a href="" id="hs-unload-reason-zero-sim-count"></a>**HS\_UNLOAD\_原因\_零\_SIM\_计数**  
因为存在没有 SIM 卡正在卸载该插件。

<a href="" id="hs-unload-reason-display-flag-but-no-display-string-id"></a>**HS\_UNLOAD\_原因\_显示\_标志\_但是\_否\_显示\_字符串\_ID**  
由于正在卸载插件的插件[ **HS\_插件\_配置文件**](hs-plugin-profile.md)结构需要的 HTTP 或基于 EAP SIM 的身份验证，但未指定的值**dwSupportedSIMCount。**

<a href="" id="hs-unload-reason-custom-realm-flag-but-no-realm-string"></a>**HS\_UNLOAD\_原因\_自定义\_领域\_标志\_但是\_否\_领域\_字符串**  
由于正在卸载插件的插件[ **HS\_插件\_配置文件**](hs-plugin-profile.md)指定结构**HS\_标志\_功能\_网络\_自定义\_领域**功能，但未提供的有效字符串**szRealm**。

<a href="" id="hs-unload-reason-duplicate-plugin-loaded"></a>**HS\_UNLOAD\_原因\_重复\_插件\_LOADED**  
插件是正在卸载，因为另一个插件使用的同一个 DLL。

<a href="" id="hs-unload-reason-reload-requested-by-plugin"></a>**HS\_UNLOAD\_原因\_重新加载\_请求\_BY\_插件**  
因为该插件需要卸载并重新加载通过指定正在卸载插件**HS\_更新\_结果\_操作\_重新加载**操作具有[ **eHS\_更新\_结果**](ehs-update-result.md)枚举。

<a href="" id="hs-unload-reason-exception-during-plugin-call"></a>**HS\_UNLOAD\_原因\_异常\_在\_插件\_调用**  
正在卸载插件宿主进程出现中对插件的调用出现异常。

<a href="" id="hs-unload-reason-exception-in-plugin-host"></a>**HS\_UNLOAD\_原因\_异常\_IN\_插件\_主机**  
正在卸载插件因为热点主机遇到了异常。

<a href="" id="hs-unload-reason-async-initialization-failed"></a>**HS\_UNLOAD\_原因\_异步\_初始化\_失败**  
正在卸载插件因为热点服务无法注册来自插件的通知。

<a href="" id="hs-unload-reason-unsupported-auth-capability-requested"></a>**HS\_UNLOAD\_原因\_不支持\_身份验证\_功能\_请求**  
插件是正在卸载，因为所有请求通过该插件的身份验证功能均不可用。

<a href="" id="hs-unload-reason-failed-to-load-provider-name-string"></a>**HS\_UNLOAD\_原因\_FAILED\_TO\_负载\_提供程序\_名称\_字符串**  
因为热点服务无法映射正在卸载插件**dwProviderNameStringID**字符串中的插件提供的 ID [ **HS\_插件\_配置文件**](hs-plugin-profile.md)为有效的字符串的结构。

<a href="" id="hs-unload-reason-failed-to-load-advanced-page-string"></a>**HS\_UNLOAD\_原因\_FAILED\_TO\_负载\_高级\_页\_字符串**  
由于正在卸载插件的插件[ **HS\_插件\_配置文件**](hs-plugin-profile.md) （可选） 指定结构**dwAdvancedPageStringID**字符串 ID，但它未映射到有效的字符串。

<a href="" id="hs-unload-reason-failed-to-load-network-name-string"></a>**HS\_UNLOAD\_原因\_FAILED\_TO\_负载\_网络\_名称\_字符串**  
由于正在卸载插件的插件[ **HS\_插件\_配置文件**](hs-plugin-profile.md) （可选） 指定结构**dwGenericNetworkNameStringID**字符串 ID，但它未映射到有效的字符串。

<a href="" id="hs-unload-reason-failed-to-configure-hidden-network"></a>**HS\_UNLOAD\_原因\_FAILED\_TO\_配置\_HIDDEN\_网络**  
因为该插件指定隐藏的网络正在卸载插件 (通过**HS\_标志\_功能\_网络\_类型\_HIDDEN**功能)，但热点服务找不配置隐藏的网络。

<a href="" id="hs-unload-reason-hidden-network-already-configured"></a>**HS\_UNLOAD\_原因\_HIDDEN\_网络\_已\_已配置**  
因为该插件指定通过隐藏的网络正在卸载插件**HS\_标志\_功能\_网络\_类型\_HIDDEN**功能，但另一个插件已经占用了隐藏的网络槽。

<a href="" id="hs-unload-reason-failed-to-query-sims"></a>**HS\_UNLOAD\_原因\_FAILED\_TO\_查询\_SIMS**  
由于正在卸载插件调用[ **HS\_插件\_查询\_支持\_SIMS** ](hs-plugin-query-supported-sims.md)失败。

<a href="" id="hs-unload-reason-plugin-required-sim-not-present"></a>**HS\_UNLOAD\_原因\_插件\_必需\_SIM\_不\_存在**  
插件是正在卸载，因为所需的插件 sims 就不存在的设备中。

<a href="" id="hs-unload-reason-sim-config-changed"></a>**HS\_UNLOAD\_原因\_SIM\_配置\_已更改**  
正在卸载插件模块由于 SIM 配置更改，这需要卸载并重新加载的插件。

<a href="" id="hs-unload-reason-wifi-switched-off-in-os"></a>**HS\_UNLOAD\_REASON\_WIFI\_SWITCHED\_OFF\_IN\_OS**  
因为在操作系统中关闭 Wi-fi 功能正在卸载该插件。

<a href="" id="hs-unload-reason-max"></a>**HS\_UNLOAD\_REASON\_MAX**  
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

## <a name="see-also"></a>请参阅


[**HS\_插件\_配置文件**](hs-plugin-profile.md)

[**eHS\_UPDATE\_RESULT**](ehs-update-result.md)

[**HS\_插件\_查询\_支持\_SIMS**](hs-plugin-query-supported-sims.md)

 

 




