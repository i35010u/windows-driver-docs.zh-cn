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
ms.openlocfilehash: db6d9e3ad65edac142af51b1864fa553038eea76
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370067"
---
# <a name="devpkeydevicesessionid"></a>DEVPKEY_Device_SessionId


DEVPKEY_Device_SessionId 设备属性表示一个值，指示设备实例可访问中的终端服务会话。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
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
<td align="left"><p><strong>属性访问</strong></p></td>
<td align="left"><p>读取和写入应用程序和服务的访问。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>本地化？</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

终端服务器功能支持插即用 (PnP) 设备重定向。 设备重定向确定是否可以访问设备的应用程序和服务在所有终端服务会话中，或是否仅在特定的终端服务会话中访问设备。 设备的终端服务会话中的可访问性取决于一台设备，DEVPKEY_Device_SessionId 的设置，如下所示：

-   如果 DEVPKEY_Device_SessionId 属性不存在，或该属性存在，但未设置属性的值，则可以在所有活动的终端服务会话中访问该设备。

-   如果存在 DEVPKEY_Device_SessionId 属性和属性的值设置为非零的终端服务 l 会话标识符，则可以仅在终端服务会话标识符所指示的终端服务会话中访问该设备。

-   如果存在 DEVPKEY_Device_SessionId 属性和属性的值设置为零，则可以仅由服务访问该设备。 会话 0 是只有服务可以在其中运行的特殊会话。

可以通过调用访问 DEVPKEY_Device_SessionId 属性[ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963)并[ **SetupDiSetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff552163).

Windows Server 2003、 Windows XP 和 Windows 2000 不支持此属性。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>在 Windows Vista 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Devpkey.h （包括 Devpkey.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

[**SetupDiSetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff552163)

 

 






