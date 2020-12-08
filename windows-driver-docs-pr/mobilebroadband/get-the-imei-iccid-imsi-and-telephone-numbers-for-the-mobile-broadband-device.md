---
title: 获取用于 MB 设备的 IMEI、ICCID、IMSI 和电话号码
description: 获取移动宽带设备的 IMEI、ICCID、IMSI 和电话号码
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4164c3b78471162377810edbded8014a14bf7eb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782337"
---
# <a name="get-the-imei-iccid-imsi-and-telephone-numbers-for-the-mobile-broadband-device"></a>获取移动宽带设备的 IMEI、ICCID、IMSI 和电话号码


以下属性可用于此帐户的当前网络设备：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>“值”</th>
<th>要使用的 MobileBroadbandDeviceInformation 的属性</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>IMEI</p></td>
<td><p>MobileEquipmentId</p></td>
</tr>
<tr class="even">
<td><p>MEID</p></td>
<td><p>MobileEquipmentId</p></td>
</tr>
<tr class="odd">
<td><p>IMSI</p></td>
<td><p>SubscriberId</p></td>
</tr>
<tr class="even">
<td><p>MIN</p></td>
<td><p>SubscriberId</p></td>
</tr>
<tr class="odd">
<td><p>IRM</p></td>
<td><p>SubscriberId</p></td>
</tr>
<tr class="even">
<td><p>ICCID</p></td>
<td><p>SimIccId</p></td>
</tr>
<tr class="odd">
<td><p>电话号码</p></td>
<td><p>TelephoneNumbers (仅在网络注册之后可用) </p></td>
</tr>
</tbody>
</table>

 

``` syntax
account.currentDeviceInformation.mobileEquipmentId
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 API 的常见任务](./create-a-mobilebroadbandaccount-object.md)

 

