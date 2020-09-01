---
title: GUID \_ DEVINTERFACE \_ 映像设备接口类
description: GUID \_ DEVINTERFACE \_ 映像设备接口类
ms.assetid: 2bf0bb35-c047-481e-a0f3-b8a8c06e259b
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce2d151a3475d639b7fc72cd43fa0302780b1649
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186479"
---
# <a name="guid_devinterface_image-device-interface-class"></a>GUID \_ DEVINTERFACE \_ 映像设备接口类


映像 [设备接口类](../install/overview-of-device-interface-classes.md) 定义为 [静止图像设备](./index.md)，包括数字照相机和扫描仪。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribute</th>
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
<td><p>{0x6bdd1fc6L，0x810f，0x11d0，0xbe，0xc7，0x08，0x00，0x2b，0xe2，0x09，0x2f}</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idheadersspanspan-idheadersspanheaders"></a><span id="headers"></span><span id="HEADERS"></span>只要

在 *Wiaintfc*中定义。 包括 *Wiaintfc。*

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

系统为静止图像设备提供的内核模式驱动程序为静止图像设备注册此设备接口类的实例。 可以通过使用仍为映像驱动程序支持的 i/o 接口，来访问此设备接口类的实例。 有关静止图像设备和驱动程序的详细信息，请参阅 [Windows 映像获取驱动程序](./windows-image-acquisition-drivers.md)。

此接口同时适用于静止映像驱动程序和 WIA 驱动程序，适用于 Microsoft Windows XP 和更高版本的 Windows。

 

