---
title: BUS1394_CLASS_GUID
description: BUS1394_CLASS_GUID
ms.assetid: 5452c829-b1d2-4a15-93ef-3d82ac6c04d0
keywords:
- BUS1394_CLASS_GUID 设备和驱动程序安装
topic_type:
- apiref
api_name:
- BUS1394_CLASS_GUID
api_location:
- 1394.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a1a0655553e33af83f35f10fb583f071ee0cd219
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566785"
---
# <a name="bus1394classguid"></a>BUS1394_CLASS_GUID


BUS1394_CLASS_GUID[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)为定义[1394年总线设备](https://msdn.microsoft.com/library/windows/hardware/ff537209)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">特性</th>
<th align="left">设置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>标识符</p></td>
<td align="left"><p>BUS1394_CLASS_GUID</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{6BDD1FC1-810F-11d0-BEC7-08002BE2092F}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

对于 1394年总线总线驱动程序注册通知的操作系统和应用程序的 1394年总线设备存在此设备接口类的实例。

1394 总线有关的信息，请参阅[1394年总线设备](https://msdn.microsoft.com/library/windows/hardware/ff537209)。

WDK 示例包括[1394api 示例](https://msdn.microsoft.com/library/windows/hardware/ff536887)应用程序。 此应用程序使用 BUS1394_CLASS_GUID 注册此设备接口类的实例存在接收通知。

有关 IEEE 1394 设备的设备接口类中 61883[设备安装程序类](https://msdn.microsoft.com/library/windows/hardware/ff541509)的支持 IEC 61883 协议，请参阅[ **GUID_61883_CLASS**](guid-61883-class.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>在 Windows XP 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">1394.h （包括 1394.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**GUID_61883_CLASS**](guid-61883-class.md)

 

 






