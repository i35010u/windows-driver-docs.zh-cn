---
title: 获取的 MB 设备的 IMEI、 ICCID、 IMSI 和电话号码
description: 获取移动宽带设备 IMEI、 ICCID、 IMSI 和电话号码
ms.assetid: b604d08c-7e6f-4dad-9e1d-3f24a0da5760
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fc18008347d3c4257079311954f62724860f20c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524305"
---
# <a name="get-the-imei-iccid-imsi-and-telephone-numbers-for-the-mobile-broadband-device"></a>获取移动宽带设备 IMEI、 ICCID、 IMSI 和电话号码


以下属性是可用于当前的网络设备的帐户：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>值</th>
<th>MobileBroadbandDeviceInformation 若要使用的属性</th>
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
<td><p>最小值</p></td>
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
<td><p>TelephoneNumbers （只有网络注册后）</p></td>
</tr>
</tbody>
</table>

 

``` syntax
account.currentDeviceInformation.mobileEquipmentId
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[移动宽带 Windows 运行时 Api 的常见任务](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 






