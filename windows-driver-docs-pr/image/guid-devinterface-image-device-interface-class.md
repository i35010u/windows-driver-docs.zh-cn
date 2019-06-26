---
title: GUID\_DEVINTERFACE\_图像设备接口类
description: GUID\_DEVINTERFACE\_图像设备接口类
ms.assetid: 2bf0bb35-c047-481e-a0f3-b8a8c06e259b
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d741fec903cc2ca37355c407f3f25c5e676b0213
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363059"
---
# <a name="guiddevinterfaceimage-device-interface-class"></a>GUID\_DEVINTERFACE\_图像设备接口类


图像[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)为定义[静止图像设备](https://docs.microsoft.com/windows-hardware/drivers/image/index)，包括数字照相机和扫描仪。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>特性</th>
<th>设置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>清单常量</p></td>
<td><p>GUID_DEVINTERFACE_IMAGE</p></td>
</tr>
<tr class="even">
<td><p>类 GUID</p></td>
<td><p>{0x6bdd1fc6L，0x810f、 0x11d0、 0xbe，0xc7:sp、 0x08，0x00、 0x2b、 0xe2、 0x09，0x2f}</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idheadersspanspan-idheadersspanheaders"></a><span id="headers"></span><span id="HEADERS"></span>标头

在中定义*Wiaintfc.h*。 包括*Wiaintfc.h。*

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

静止图像设备的系统提供的内核模式驱动程序注册静止图像设备此设备接口类的实例。 可以使用静止图像的驱动程序支持的 I/O 接口来访问此设备接口类的实例。 有关仍映像设备和驱动程序的详细信息，请参阅[Windows 图像采集驱动程序](https://docs.microsoft.com/windows-hardware/drivers/image/windows-image-acquisition-drivers)。

此接口是适用于仍映像驱动程序和 WIA 驱动程序，适用于 Microsoft Windows XP 和更高版本的 Windows。

 

 





