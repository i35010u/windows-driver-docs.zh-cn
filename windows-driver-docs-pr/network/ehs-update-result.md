---
title: eHS_UPDATE_RESULT 枚举
description: EHS_UPDATE_RESULT 枚举指示 "检查更新" 请求的结果。
ms.assetid: 7b9b8ddc-3101-466a-9640-b936f6d14de4
keywords:
- 从 Windows Vista 开始 eHS_UPDATE_RESULT 枚举网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4263c4043eb148486d9ac9f4e2ea501913fa154
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403482"
---
# <a name="ehs_update_result-enumeration"></a>eHS \_ 更新 \_ 结果枚举

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


**EHS \_ UPDATE \_ 结果**枚举指示 "检查更新" 请求的结果。

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

<a href="" id="hs-update-result-success"></a>**HS \_ 更新 \_ 结果 \_ 成功**  
指示更新成功。

<a href="" id="hs-update-result-action-reconnect"></a>**HS \_ 更新 \_ 结果 \_ 操作 \_ 重新连接**  
更新请求的结果要求服务断开连接，然后重新连接。

<a href="" id="hs-update-result-action-reload"></a>**HS \_ 更新 \_ 结果 \_ 操作 \_ 重载**  
更新请求的结果需要服务卸载和重载插件。

<a href="" id="hs-update-result-max"></a>**HS \_ 更新 \_ 结果 \_ 最大值**  
指示超出范围值。

<a name="remarks"></a>备注
-------

此插件通过 [**HS \_ 主机 \_ 更新 \_ 配置 \_ 完成**](hs-host-update-configuration-completion.md) 功能将此枚举值传递到热点插件主机，该函数用于通知热点插件主机调用 [**HS 插件的结果 \_ \_ 检查 \_ 是否有 \_ 更新**](hs-plugin-check-for-updates.md)。

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


[**HS \_ 主机 \_ 更新 \_ 配置 \_ 完成**](hs-host-update-configuration-completion.md)

[**HS \_ 插件 \_ 检查 \_ \_ 更新**](hs-plugin-check-for-updates.md)

 

 




