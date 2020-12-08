---
title: FloppyClassGuid
description: FloppyClassGuid
keywords:
- FloppyClassGuid 设备和驱动程序安装
topic_type:
- apiref
api_name:
- FloppyClassGuid
api_location:
- Ntddstor.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9ff15e9397a9973397a2db0cee0f5f89979434cb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820193"
---
# <a name="floppyclassguid"></a>FloppyClassGuid


FloppyClassGuid 是适用于软盘[存储设备](../storage/index.md)的[设备接口类](./overview-of-device-interface-classes.md)的过时标识符。 启动 Microsoft Windows 2000，使用此类的新实例 [**GUID_DEVINTERFACE_FLOPPY**](guid-devinterface-floppy.md) 类标识符。

<a name="remarks"></a>备注
-------

WDK 中的存储 [示例](https://go.microsoft.com/fwlink/p/?LinkId=618052) 包括使用 FloppyClassGuid 注册此设备接口类的实例的 [软盘驱动程序](/samples/browse/) 示例。

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
<td align="left"><p>已过时。 从 Windows 2000 开始，改用 GUID_DEVINTERFACE_FLOPPY。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ntddstor (包含 Ntddstor) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**GUID_DEVINTERFACE_FLOPPY**](guid-devinterface-floppy.md)

