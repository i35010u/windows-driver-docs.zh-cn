---
title: WdfRequestSendSyncAtDispatch2 规则 (kmdf)
description: WdfRequestSendSyncAtDispatch2 规则验证在正确的 IRQL 优先级级别的已发送 WdfRequestSend 函数。
ms.assetid: 0C66BC01-9467-4A04-B1E5-A0EA248F8725
ms.date: 05/21/2018
keywords:
- WdfRequestSendSyncAtDispatch2 规则 (kmdf)
topic_type:
- apiref
api_name:
- WdfRequestSendSyncAtDispatch2
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c46865e14abd4271350fc054ff92c2e9e8e28359
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567223"
---
# <a name="wdfrequestsendsyncatdispatch2-rule-kmdf"></a>WdfRequestSendSyncAtDispatch2 规则 (kmdf)


**WdfRequestSendSyncAtDispatch2**规则确认[ **WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027)在正确的 IRQL 优先级别发送函数。

如果驱动程序设置 WDF\_请求\_发送\_选项\_同步标志，它必须调用[ **WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027)函数在 IRQL = 被动\_级别。 如果未设置此标志，该驱动程序必须调用**WdfRequestSend**函数在 IRQL = 调度\_级别。

> [!NOTE]
>
> 此规则测试相同条件[ **WdfRequestSendSyncAtDispatch** ](wdfrequestsendsyncatdispatch.md)规则，但它使用不同的工具来测试不同的代码路径。

 

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>WdfRequestSendSyncAtDispatch2</strong>规则。</p>
使用以下步骤来分析你的代码：
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">准备你的代码 （使用角色类型声明）。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">运行的 Static Driver Verifier。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">查看和分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">以找到缺陷驱动程序中使用 Static Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用对象
----------

[**WdfUsbInterfaceGetConfiguredPipe**](https://msdn.microsoft.com/library/windows/hardware/ff550057)
[**WdfUsbInterfaceGetConfiguredSettingIndex**](https://msdn.microsoft.com/library/windows/hardware/ff550059)
[**WdfUsbInterfaceGetDescriptor**](https://msdn.microsoft.com/library/windows/hardware/ff550060)
[**WdfUsbInterfaceGetEndpointInformation**](https://msdn.microsoft.com/library/windows/hardware/ff550063)
[**WdfUsbInterfaceGetInterfaceNumber**](https://msdn.microsoft.com/library/windows/hardware/ff550065)
[**WdfUsbInterfaceGetNumConfiguredPipes**](https://msdn.microsoft.com/library/windows/hardware/ff550066)
[**WdfUsbInterfaceGetNumEndpoints**](https://msdn.microsoft.com/library/windows/hardware/ff550068)
[**WdfUsbInterfaceGetNumSettings**](https://msdn.microsoft.com/library/windows/hardware/ff550070)
[**WdfUsbInterfaceSelectSetting**](https://msdn.microsoft.com/library/windows/hardware/ff550073)
[**WdfUsbTargetDeviceAllocAndQueryString**](https://msdn.microsoft.com/library/windows/hardware/ff550074)
[**WdfUsbTargetDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff550077)
[**WdfUsbTargetDeviceCyclePortSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff550080)
[**WdfUsbTargetDeviceFormatRequestForControlTransfer**](https://msdn.microsoft.com/library/windows/hardware/ff550082)
[**WdfUsbTargetDeviceFormatRequestForCyclePort**](https://msdn.microsoft.com/library/windows/hardware/ff550084)
[**WdfUsbTargetDeviceFormatRequestForString**](https://msdn.microsoft.com/library/windows/hardware/ff550086)
[**WdfUsbTargetDeviceFormatRequestForUrb**](https://msdn.microsoft.com/library/windows/hardware/ff550088)
[**WdfUsbTargetDeviceGetDeviceDescriptor**](https://msdn.microsoft.com/library/windows/hardware/ff550090)
[**WdfUsbTargetDeviceGetInterface**](https://msdn.microsoft.com/library/windows/hardware/ff550092)
[**WdfUsbTargetDeviceGetNumInterfaces**](https://msdn.microsoft.com/library/windows/hardware/ff550094)
[**WdfUsbTargetDeviceIsConnectedSynchronous**](https://msdn.microsoft.com/library/windows/hardware/ff550095)
[**WdfUsbTargetDeviceQueryString**](https://msdn.microsoft.com/library/windows/hardware/ff550096)
[**WdfUsbTargetDeviceResetPortSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff550097)
[**WdfUsbTargetDeviceRetrieveConfigDescriptor**](https://msdn.microsoft.com/library/windows/hardware/ff550098)
[**WdfUsbTargetDeviceRetrieveCurrentFrameNumber**](https://msdn.microsoft.com/library/windows/hardware/ff550099)
[**WdfUsbTargetDeviceRetrieveInformation**](https://msdn.microsoft.com/library/windows/hardware/ff550100)
[**WdfUsbTargetDeviceSelectConfig**](https://msdn.microsoft.com/library/windows/hardware/ff550101)
[**WdfUsbTargetDeviceSendControlTransferSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff550104)
[**WdfUsbTargetDeviceSendUrbSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff550105)
[**WdfUsbTargetDeviceWdmGetConfigurationHandle**](https://msdn.microsoft.com/library/windows/hardware/ff551127)
[**WdfUsbTargetPipeAbortSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff551129)
[**WdfUsbTargetPipeConfigContinuousReader**](https://msdn.microsoft.com/library/windows/hardware/ff551130)
[**WdfUsbTargetPipeFormatRequestForAbort**](https://msdn.microsoft.com/library/windows/hardware/ff551132)
[**WdfUsbTargetPipeFormatRequestForRead**](https://msdn.microsoft.com/library/windows/hardware/ff551136)
[**WdfUsbTargetPipeFormatRequestForReset**](https://msdn.microsoft.com/library/windows/hardware/ff551138)
[**WdfUsbTargetPipeFormatRequestForUrb**](https://msdn.microsoft.com/library/windows/hardware/ff551139)
[**WdfUsbTargetPipeFormatRequestForWrite**](https://msdn.microsoft.com/library/windows/hardware/ff551141)
[**WdfUsbTargetPipeGetInformation**](https://msdn.microsoft.com/library/windows/hardware/ff551142)
[**WdfUsbTargetPipeGetType**](https://msdn.microsoft.com/library/windows/hardware/ff551148)
[**WdfUsbTargetPipeIsInEndpoint**](https://msdn.microsoft.com/library/windows/hardware/ff551151)
[**WdfUsbTargetPipeIsOutEndpoint**](https://msdn.microsoft.com/library/windows/hardware/ff551153)
[**WdfUsbTargetPipeReadSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff551155)
[**WdfUsbTargetPipeResetSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff551156)
[**WdfUsbTargetPipeSendUrbSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff551158)
[**WdfUsbTargetPipeSetNoMaximumPacketSizeCheck**](https://msdn.microsoft.com/library/windows/hardware/ff551160)
[**WdfUsbTargetPipeWdmGetPipeHandle**](https://msdn.microsoft.com/library/windows/hardware/ff551162)
[**WdfUsbTargetPipeWriteSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff551163)
 

 





