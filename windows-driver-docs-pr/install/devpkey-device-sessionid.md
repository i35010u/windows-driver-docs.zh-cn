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
ms.openlocfilehash: 25b3459514199b3c06ff0105b3ae4bcfa42812e7
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418528"
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
<th>属性</th>
<th>Value</th>
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

终端服务器功能支持即插即用（PnP）设备重定向。 设备重定向确定设备是否可由所有终端服务会话内的应用程序和服务访问，或者是否只能在特定终端服务会话中访问设备。 终端服务会话中的设备的可访问性由设备的 DEVPKEY_Device_SessionId 设置确定，如下所示：

-   如果 DEVPKEY_Device_SessionId 属性不存在，或者属性存在，但未设置属性的值，则可以在所有活动终端服务会话中访问设备。

-   如果 DEVPKEY_Device_SessionId 属性存在并且属性的值设置为非零终端服务 l 会话标识符，则只能在终端服务会话标识符指示的终端服务会话中访问设备。

-   如果 DEVPKEY_Device_SessionId 属性存在并且属性的值设置为零，则只能通过服务访问设备。 会话零是一种特殊会话，其中只能运行服务。

可以通过调用[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)和[**SetupDiSetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)访问 DEVPKEY_Device_SessionId 属性。

Windows Server 2003、Windows XP 和 Windows 2000 不支持此属性。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows**头**： Devpkey （包括 Devpkey）


## <a name="see-also"></a>请参阅


[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

[**SetupDiSetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)

 

 






