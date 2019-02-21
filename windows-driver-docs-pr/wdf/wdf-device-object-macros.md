---
title: WDF 设备对象宏
description: 本部分介绍提供 WDF 设备对象支持的宏。
ms.assetid: D91C16EB-5E31-4AB2-984E-A0B35C3B1BA1
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f19eae51ea42c047cd6b2b4eda125a33ed4e8200
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520188"
---
# <a name="wdf-device-object-macros"></a>WDF 设备对象宏


本部分介绍提供 WDF 设备对象支持的宏。

## <a name="in-this-section"></a>本部分内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>主题</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="wdfdeviceresumeidlewithtag.md" data-raw-source="[&lt;strong&gt;WdfDeviceResumeIdleWithTag method&lt;/strong&gt;](wdfdeviceresumeidlewithtag.md)"><strong>WdfDeviceResumeIdleWithTag 方法</strong></a></p></td>
<td><div class="alert">
<strong>请注意</strong>  适用于 KMDF 和 UMDF
</div>
<div>
 
</div>
<p><a href="wdfdeviceresumeidlewithtag.md" data-raw-source="[&lt;strong&gt;WdfDeviceResumeIdleWithTag&lt;/strong&gt;](wdfdeviceresumeidlewithtag.md)"> <strong>WdfDeviceResumeIdleWithTag</strong> </a>宏递减 power 引用计数为指定的框架设备对象并将分配该驱动程序&#39;s 当前文件名和行号到引用。 宏还将分配到引用的标记值。</p></td>
</tr>
<tr class="even">
<td><p><a href="wdfdevicestopidlewithtag.md" data-raw-source="[&lt;strong&gt;WdfDeviceStopIdleWithTag method&lt;/strong&gt;](wdfdevicestopidlewithtag.md)"><strong>WdfDeviceStopIdleWithTag 方法</strong></a></p></td>
<td><div class="alert">
<strong>请注意</strong>  适用于 KMDF 和 UMDF
</div>
<div>
 
</div>
<p><a href="wdfdevicestopidlewithtag.md" data-raw-source="[&lt;strong&gt;WdfDeviceStopIdleWithTag&lt;/strong&gt;](wdfdevicestopidlewithtag.md)"> <strong>WdfDeviceStopIdleWithTag</strong> </a>宏递增指定的框架设备对象的 power 引用计数并将分配该驱动程序&#39;s 当前文件名和行号的参考. 宏还将分配到引用的标记值。</p></td>
</tr>
</tbody>
</table>

 

 

 






