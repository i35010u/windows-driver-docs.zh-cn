---
title: UsbContReader 规则 (kmdf)
description: UsbContReader 规则指定一个持续的读取器已正确配置的驱动程序 EvtDevicePrepareHardware 事件回调函数，其中该驱动程序会对 WdfUsbTargetPipeConfigContinuousReader 方法的调用中。
ms.assetid: f9bb885e-2da0-4f4d-ad62-6d450d9a64dd
ms.date: 05/21/2018
keywords:
- UsbContReader 规则 (kmdf)
topic_type:
- apiref
api_name:
- UsbContReader
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2f91b26ea3cc88869330459413c6a4b285d95280
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392851"
---
# <a name="usbcontreader-rule-kmdf"></a>UsbContReader 规则 (kmdf)


**UsbContReader**规则指定连续读取器是否已正确配置中的驱动程序[ *EvtDevicePrepareHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)事件回调函数，其中该驱动程序将调用[ **WdfUsbTargetPipeConfigContinuousReader** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipeconfigcontinuousreader)方法。

|              |      |
|--------------|------|
| 驱动程序模型 | KMDF |

<a name="how-to-test"></a>如何测试
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在编译时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>并指定<strong>UsbContReader</strong>规则。</p>
使用以下步骤来分析你的代码：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">准备你的代码 （使用角色类型声明）。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">运行的 Static Driver Verifier。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">查看和分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">以找到缺陷驱动程序中使用 Static Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用对象
----------

[**WdfUsbTargetPipeConfigContinuousReader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipeconfigcontinuousreader)
 

 





