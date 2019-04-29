---
title: eHS_UPDATE_RESULT 枚举
description: EHS_UPDATE_RESULT 枚举指示"检查更新"请求的结果。
ms.assetid: 7b9b8ddc-3101-466a-9640-b936f6d14de4
keywords:
- 与 Windows Vista 一起启动的网络驱动程序的 eHS_UPDATE_RESULT 枚举
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e21d5a357a50a80211922019781688770539a1b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372554"
---
# <a name="ehsupdateresult-enumeration"></a>eHS\_更新\_结果枚举

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**EHS\_更新\_结果**枚举指示"检查更新"请求的结果。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef enum _eHS_UPDATE_RESULT { 
  HS_UPDATE_RESULT_SUCCESS,
  HS_UPDATE_RESULT_ACTION_RECONNECT,
  HS_UPDATE_RESULT_ACTION_RELOAD,
  HS_UPDATE_RESULT_MAX
} eHS_UPDATE_RESULT;
```

<a name="constants"></a>常量
---------

<a href="" id="hs-update-result-success"></a>**HS\_UPDATE\_RESULT\_SUCCESS**  
指示已成功更新。

<a href="" id="hs-update-result-action-reconnect"></a>**HS\_更新\_结果\_操作\_重新连接**  
更新请求的结果需要服务断开连接，然后重新连接。

<a href="" id="hs-update-result-action-reload"></a>**HS\_更新\_结果\_操作\_重新加载**  
更新请求的结果需要卸载并重新加载该插件服务。

<a href="" id="hs-update-result-max"></a>**HS\_UPDATE\_RESULT\_MAX**  
指示一个范围外的值。

<a name="remarks"></a>备注
-------

该插件将此枚举值传递给热点插件宿主通过[ **HS\_主机\_更新\_配置\_完成**](hs-host-update-configuration-completion.md)函数，用来通知调用的结果的热点插件主机[ **HS\_插件\_检查\_有关\_更新**](hs-plugin-check-for-updates.md).

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


[**HS\_主机\_更新\_配置\_完成**](hs-host-update-configuration-completion.md)

[**HS\_插件\_检查\_为\_更新**](hs-plugin-check-for-updates.md)

 

 




