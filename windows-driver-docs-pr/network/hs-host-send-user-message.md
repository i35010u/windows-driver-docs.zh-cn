---
title: HS_HOST_SEND_USER_MESSAGE 函数
description: HS_HOST_SEND_USER_MESSAGE 函数调用与用户进行通信。 传递给热点卸载服务的自定义用户界面显示字符串中包含消息内容。
ms.assetid: c4ab1fda-18eb-44e4-aa64-f7b37b4147a3
keywords:
- 与 Windows Vista 一起启动的网络驱动程序的 typedef DWORD (WINAPI HS_HOST_SEND_USER_MESSAGE) 函数
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: af7f445d32f21ab001fe945f86b5d80aa822b0c5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568040"
---
# <a name="hshostsendusermessage-function"></a>HS\_主机\_发送\_用户\_消息函数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_主机\_发送\_用户\_消息**函数调用与用户进行通信。 传递给热点卸载服务的自定义用户界面显示字符串中包含消息内容。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_HOST_SEND_USER_MESSAGE)(
  _In_ HANDLE hPluginContext,
  _In_ DWORD  dwConnectionId,
  _In_ DWORD  dwStringID
);
```

<a name="parameters"></a>Parameters
----------

*hPluginContext* \[in\]  
此函数在调用插件的上下文句柄。

*dwConnectionId* \[in\]  
网络连接的唯一标识符。

*dwStringID* \[in\]  
字符串 ID 的索引使用到字符串表中存储的消息。

<a name="return-value"></a>返回值
------------

此函数调用由插件与主机通信，并不会返回一个值。

<a name="remarks"></a>备注
-------

热点插件会将消息存储字符串表。 该插件必须向热点卸载服务以使其能够加载相应的字符串传递字符串 Id。

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
<td>Hotspotoffloadplugin.h （包括 Hotspotoffloadplugin.h）</td>
</tr>
</tbody>
</table>

 

 




