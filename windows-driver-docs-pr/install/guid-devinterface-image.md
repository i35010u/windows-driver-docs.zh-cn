---
title: GUID_DEVINTERFACE_IMAGE
description: GUID_DEVINTERFACE_IMAGE
ms.assetid: 2768f0ef-3765-4a66-b480-0f75a7c49c3c
keywords:
- GUID_DEVINTERFACE_IMAGE 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_IMAGE
api_location:
- Wiaintfc.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a3642dc07bee9be83f0bd59ee6d4e0f1de6c83e1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375275"
---
# <a name="guiddevinterfaceimage"></a>GUID_DEVINTERFACE_IMAGE


GUID_DEVINTERFACE_IMAGE[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)为定义[WIA 的设备和仍映像 (STI) 设备](https://docs.microsoft.com/windows-hardware/drivers/image/index)，包括数字照相机和扫描仪。

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
<td align="left"><p>GUID_DEVINTERFACE_IMAGE</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{6BDD1FC6-810F-11D0-BEC7-08002BE2092F}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

WIA 的设备的系统提供的内核模式驱动程序注册通知的操作系统和应用程序的 WIA 的设备存在此设备接口类的实例。

WIA 驱动程序和 STI 驱动程序有关的信息，请参阅[Windows 图像采集驱动程序](https://docs.microsoft.com/windows-hardware/drivers/image/windows-image-acquisition-drivers)。

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
<td align="left"><p>在 Windows XP 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Wiaintfc.h （包括 Wiaintfc.h）</td>
</tr>
</tbody>
</table>

 

 





