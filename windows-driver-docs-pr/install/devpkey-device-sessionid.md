---
title: DEVPKEY_Device_SessionId
description: DEVPKEY_Device_SessionId
ms.assetid: 0e5815b3-0427-4f07-9ec1-a21976d5d933
keywords:
- DEVPKEY_Device_SessionId 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_SessionId
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 951846d33f4593111d8f11f71a81b446cedd138c
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715272"
---
# <a name="devpkey_device_sessionid"></a>DEVPKEY_Device_SessionId


DEVPKEY_Device_SessionId 设备属性表示一个值，该值指示可在其中访问设备实例的终端服务会话。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr>
<th>Attribute</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_Device_SessionId</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-uint32.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_UINT32&lt;/strong&gt;](devprop-type-uint32.md)"><strong>DEVPROP_TYPE_UINT32</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>按应用程序和服务进行读取和写入访问。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

终端服务器功能支持即插即用 (PnP) 设备重定向。 设备重定向确定设备是否可由所有终端服务会话内的应用程序和服务访问，或者是否只能在特定终端服务会话中访问设备。 终端服务会话中的设备的可访问性由设备的 DEVPKEY_Device_SessionId 设置确定，如下所示：

-   如果 DEVPKEY_Device_SessionId 属性不存在，或者属性存在，但未设置属性的值，则可以在所有活动终端服务会话中访问设备。

-   如果 DEVPKEY_Device_SessionId 属性存在并且属性的值设置为非零终端服务 l 会话标识符，则只能在终端服务会话标识符指示的终端服务会话中访问设备。

-   如果 DEVPKEY_Device_SessionId 属性存在并且属性的值设置为零，则只能通过服务访问设备。 会话零是一种特殊会话，其中只能运行服务。

可以通过调用 [**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw) 和 [**SetupDiSetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)访问 DEVPKEY_Device_SessionId 属性。

Windows Server 2003、Windows XP 和 Windows 2000 不支持此属性。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows **标题**： Devpkey (包含 Devpkey) 


## <a name="see-also"></a>请参阅


[**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

[**SetupDiSetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)

 

