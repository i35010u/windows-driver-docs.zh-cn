---
title: NDKPI 完成处理要求
description: NDK 使用者和 NDK 提供程序必须遵循这些要求的 NDKPI 完成处理。
ms.assetid: 87150E2F-64F2-4EAB-A8B3-8E77622BE36C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fda94936acd396fa2f60ba70ddc4a1eeb2f18b9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376772"
---
# <a name="ndkpi-completion-handling-requirements"></a>NDKPI 完成处理要求


NDK 使用者和 NDK 提供程序必须遵循这些要求的 NDKPI 完成处理。

## <a name="the-rules-for-ndkgetcqresults-ndkgetcqresultsex-and-ndkarmcq-functions"></a>NdkGetCqResults、 NdkGetCqResultsEx 和 NdkArmCq 函数的规则


使用者始终会将序列化其调用与这些提供程序函数对相同的完成队列 (CQ) 对象 ([**NDK\_CQ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_cq)):

-   *NdkGetCqResults* ([*NDK\_FN\_GET\_CQ\_RESULTS*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_get_cq_results))
-   *NdkGetCqResultsEx* ([*NDK\_FN\_GET\_CQ\_RESULTS\_EX*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_get_cq_results_ex))
-   *NdkArmCq* ([*NDK\_FN\_ARM\_CQ*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_arm_cq))

这不仅意味着使用者将永远不会调用相同的提供程序函数多次并发，但还它将永远不会调用这些函数的任意组合同时在相同的 CQ 上从多个线程。

**NdkOperationTypeReceiveAndInvalidate**完成时，会出现远程*NdkSendAndInvalidate* ([*NDK\_FN\_发送\_AND\_INVALIDATE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_send_and_invalidate)) 调用必须仍是检索，则可以使用*NdkGetCqResults* (不*NdkGetCqResultsEx*n)。 执行此操作仍必须使接收方，在指定的标记，但不是会通知此失效的接收使用者 (使用者必须使用*NdkGetCqResultsEx*来获取此信息)。 更高版本*NdkInvalidate* ([*NDK\_FN\_INVALIDATE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_invalidate)) 的同一个令牌将失败，像往常一样。

## <a name="the-rules-for-notification-callbacks"></a>有关通知回调的规则


提供程序必须调用*NdkCqNotificationCallback* ([*NDK\_FN\_CQ\_通知\_回调*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_cq_notification_callback)) 回调仅一次，并仅在使用者已有后*NdkCqNotificationCallback*通过调用回调*NdkArmCq*。 也就是说，该提供程序必须清除 arm 并调用*NdkCqNotificationCallback*回调时调用的条件*NdkCqNotificationCallback*回调发生 （换句话说，当请求完成在中排队的 CQ）。

如果有完成的 CQ 中已存在时使用者调用*NdkArmCq*，提供程序的行为，如下所示：

-   如果至少一个完成了新放入 CQ 自上次*NdkCqNotificationCallback*调用回调时，该提供程序必须满足的 arm 请求立即 （请参阅下面有关序列化要求）。
-   但是，如果所有完成的 CQ 中都已存在还在上次*NdkCqNotificationCallback*调用回调 (换而言之，使用者调用*NdkArmCq*而不删除所有补全和任何新的完成已放入 CQ），则提供程序可能会立即满足 arm 请求。

提供程序需要调用*NdkCqNotificationCallback*回调，如果已经*NdkCqNotificationCallback*回调正在运行，则提供程序必须延迟的调用*NdkCqNotificationCallback*回调之后再对现有的调用直到, *NdkCqNotificationCallback*回调将控制权返回给该提供程序。 换而言之，提供程序负责序列化*NdkCqNotificationCallback*回调。

下表显示了如果键入生成 arm *NdkArmCq*调用之前上一次第二次*NdkArmCq*满足请求：

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"></th>
<th align="left">第二个 arm ANY</th>
<th align="left">第二个 arm 错误</th>
<th align="left">第二个 arm SOLICITED</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>第一个 arm ANY</p></td>
<td align="left"><p>任何</p></td>
<td align="left"><p>任何</p></td>
<td align="left"><p>任何</p></td>
</tr>
<tr class="even">
<td align="left"><p>第一个 arm 错误</p></td>
<td align="left"><p>任何</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>请求</p></td>
</tr>
<tr class="odd">
<td align="left"><p>第一个 arm SOLICITED</p></td>
<td align="left"><p>任何</p></td>
<td align="left"><p>请求</p></td>
<td align="left"><p>请求</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题


[网络直接内核提供程序接口 (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






