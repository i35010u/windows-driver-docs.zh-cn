---
title: eHS_UNLOAD_REASON 枚举
description: EHS_UNLOAD_REASON 枚举指示卸载插件的原因。
ms.assetid: 1e658dd3-f66d-4803-ad3c-84bfa1890a86
keywords:
- 从 Windows Vista 开始 eHS_UNLOAD_REASON 枚举网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f129de2852a9af4c196ee99984357badcfe829c
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403486"
---
# <a name="ehs_unload_reason-enumeration"></a>eHS \_ 卸载 \_ 原因枚举

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


**EHS \_ 卸载 \_ 原因**枚举指示卸载插件的原因。

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

<a href="" id="hs-unload-reason-none"></a>**HS \_ 卸载 \_ 原因 \_ 无**  
卸载操作没有特定的原因。

<a href="" id="hs-unload-reason-plugn-init-failed"></a>**HS \_ 卸载 \_ 原因 \_ PLUGN \_ 初始化 \_ 失败**  
正在卸载插件，因为该插件未能成功初始化。

<a href="" id="hs-unload-reason-no-networks-supported"></a>**HS \_ 卸载 \_ 原因 \_ 不 \_ \_ 支持网络**  
正在卸载插件，因为插件的 [**HS \_ 插件 \_ 配置文件**](hs-plugin-profile.md) 结构未指示 **dwNumNetworksSupported**的有效值。

<a href="" id="hs-unload-reason-no-provide-name-id"></a>**HS \_ 卸载 \_ 原因 \_ 无 \_ 提供 \_ 名称 \_ ID**  
正在卸载插件，因为插件的 [**HS \_ 插件 \_ 配置文件**](hs-plugin-profile.md) 结构未指定 **dwProviderNameStringID**的字符串 ID。

<a href="" id="hs-unload-reason-zero-sim-count"></a>**HS \_ 卸载 \_ 原因 \_ 零 \_ SIM \_ 计数**  
正在卸载插件，因为不存在 SIM 卡。

<a href="" id="hs-unload-reason-display-flag-but-no-display-string-id"></a>**HS \_ 卸载 \_ 原因 \_ 显示 \_ 标志， \_ 但 \_ 没有 \_ 显示 \_ 字符串 \_ ID**  
正在卸载插件，因为插件的 [**HS \_ 插件 \_ 配置文件**](hs-plugin-profile.md) 结构需要使用 HTTP 或基于 EAP SIM 的身份验证，但未指定 dwSupportedSIMCount 的值 **。**

<a href="" id="hs-unload-reason-custom-realm-flag-but-no-realm-string"></a>**HS \_ 卸载 \_ 原因 \_ 自定义 \_ 领域 \_ 标志， \_ 但 \_ 没有 \_ 领域 \_ 字符串**  
正在卸载插件，因为插件的 [**HS \_ 插件 \_ 配置文件**](hs-plugin-profile.md) 结构指定了 **hs \_ 标志 \_ 功能 \_ 网络 \_ 自定义 \_ 领域** 功能，但未提供有效的 **szRealm**字符串。

<a href="" id="hs-unload-reason-duplicate-plugin-loaded"></a>**HS \_ 卸载 \_ 原因 \_ 已 \_ 加载重复插件 \_**  
正在卸载插件，因为另一个插件正在使用同一个 DLL。

<a href="" id="hs-unload-reason-reload-requested-by-plugin"></a>**\_ \_ \_ \_ \_ 由于插件请求重载， \_ 卸载原因**  
正在卸载插件，因为请求通过指定 **HS \_ 更新 \_ 结果 \_ 操作 \_ ** with [**eHS \_ update \_ result**](ehs-update-result.md) 枚举重新加载操作来卸载和重新加载插件。

<a href="" id="hs-unload-reason-exception-during-plugin-call"></a>**\_ \_ \_ \_ 在 \_ 插件 \_ 调用期间出现 HS 卸载原因异常**  
正在卸载插件，因为主机进程在调用插件时遇到异常。

<a href="" id="hs-unload-reason-exception-in-plugin-host"></a>**\_ \_ \_ \_ \_ 插件主机中的 \_ HS 卸载原因异常**  
正在卸载插件，因为热点主机遇到了异常。

<a href="" id="hs-unload-reason-async-initialization-failed"></a>**HS \_ 卸载 \_ 原因 \_ 异步 \_ 初始化 \_ 失败**  
正在卸载插件，因为热点服务无法从插件注册通知。

<a href="" id="hs-unload-reason-unsupported-auth-capability-requested"></a>**HS \_ 卸载 \_ 原因 \_ 请求了不受支持的 \_ 身份验证 \_ 功能 \_**  
正在卸载插件，因为插件请求的任何身份验证功能均不可用。

<a href="" id="hs-unload-reason-failed-to-load-provider-name-string"></a>**HS \_ 卸载 \_ 原因 \_ 导致 \_ 无法 \_ 加载 \_ 提供程序 \_ 名称 \_ 字符串**  
正在卸载插件，因为热点服务无法将插件的[**HS \_ 插件 \_ 配置文件**](hs-plugin-profile.md)结构中提供的**dwProviderNameStringID**字符串 ID 映射到有效的字符串。

<a href="" id="hs-unload-reason-failed-to-load-advanced-page-string"></a>**HS \_ 卸载 \_ 原因 \_ 无法 \_ \_ 加载 \_ 高级 \_ 页 \_ 字符串**  
正在卸载插件，因为插件的 [**HS \_ 插件 \_ 配置文件**](hs-plugin-profile.md) 结构指定了 (可选) **dwAdvancedPageStringID** 字符串 ID，但未映射到有效的字符串。

<a href="" id="hs-unload-reason-failed-to-load-network-name-string"></a>**HS \_ 卸载 \_ 原因 \_ 导致 \_ 无法 \_ 加载 \_ 网络 \_ 名称 \_ 字符串**  
正在卸载插件，因为插件的 [**HS \_ 插件 \_ 配置文件**](hs-plugin-profile.md) 结构指定了 (可选) **dwGenericNetworkNameStringID** 字符串 ID，但未映射到有效的字符串。

<a href="" id="hs-unload-reason-failed-to-configure-hidden-network"></a>**HS \_ 卸载 \_ 原因 \_ 无法 \_ \_ 配置 \_ 隐藏的 \_ 网络**  
正在卸载插件，因为插件指定了隐藏的网络 (通过 **HS \_ 标志 \_ 功能 \_ 网络 \_ 类型 \_ 隐藏** 功能) ，但热点服务无法配置隐藏网络。

<a href="" id="hs-unload-reason-hidden-network-already-configured"></a>**HS \_ 卸载 \_ 原因 \_ \_ \_ 已配置隐藏 \_ 网络**  
正在卸载插件，因为该插件通过 **HS \_ 标志 \_ 功能 \_ 网络 \_ 类型 \_ 隐藏** 功能指定了隐藏的网络，而另一个插件已经要求使用隐藏的网络槽。

<a href="" id="hs-unload-reason-failed-to-query-sims"></a>**HS \_ 卸载 \_ 原因 \_ 无法 \_ \_ 查询 \_ SIM**  
正在卸载插件，因为对 [**HS 插件的调用 \_ \_ 查询支持 \_ 的 \_ sim**](hs-plugin-query-supported-sims.md) 失败。

<a href="" id="hs-unload-reason-plugin-required-sim-not-present"></a>**HS \_ 卸载 \_ 原因 \_ 插件 \_ 要求的 \_ SIM \_ 不 \_ 存在**  
正在卸载插件，因为设备中不存在该插件所需的 Sim。

<a href="" id="hs-unload-reason-sim-config-changed"></a>**HS \_ 卸载 \_ 原因 \_ \_ \_ 更改了 SIM 配置**  
正在卸载插件，因为 SIM 配置已更改，这需要卸载和重新加载插件。

<a href="" id="hs-unload-reason-wifi-switched-off-in-os"></a>**HS \_ 卸载 \_ 原因 \_ \_ \_ \_ OS 中的 WIFI \_ 关闭**  
正在卸载插件，因为 Wi-fi 功能已在 OS 中关闭。

<a href="" id="hs-unload-reason-max"></a>**HS \_ 卸载 \_ 原因 \_ 最大值**  
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

## <a name="see-also"></a>另请参阅


[**HS \_ 插件 \_ 配置文件**](hs-plugin-profile.md)

[**eHS \_ 更新 \_ 结果**](ehs-update-result.md)

[**HS \_ 插件 \_ 查询 \_ 支持的 \_ SIM**](hs-plugin-query-supported-sims.md)

 

 




