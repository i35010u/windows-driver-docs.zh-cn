---
title: NDKPI 完成处理要求
description: NDK 使用者和 NDK 提供程序必须遵循这些要求才能完成 NDKPI 处理。
ms.assetid: 87150E2F-64F2-4EAB-A8B3-8E77622BE36C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d2e55f0f08707caf6bb26e334c61b00f62503a3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831906"
---
# <a name="ndkpi-completion-handling-requirements"></a>NDKPI 完成处理要求


NDK 使用者和 NDK 提供程序必须遵循这些要求才能完成 NDKPI 处理。

## <a name="the-rules-for-ndkgetcqresults-ndkgetcqresultsex-and-ndkarmcq-functions"></a>用于 NdkGetCqResults、NdkGetCqResultsEx 和 NdkArmCq 函数的规则


使用者将始终在同一完成队列（CQ）对象（[**NDK\_CQ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_cq)）上对这些提供程序函数的调用进行序列化：

-   *NdkGetCqResults* （[*NDK\_FN\_获取\_CQ\_结果*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_get_cq_results)）
-   *NdkGetCqResultsEx* （[*NDK\_FN\_获取\_CQ\_结果\_EX*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_get_cq_results_ex)）
-   *NdkArmCq* （[*NDK\_FN\_ARM\_CQ*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_arm_cq)）

这意味着，不仅使用者将不会同时调用相同的提供程序函数，还会永远不会从多个线程同时调用相同 CQ 的这些函数的任何组合。

由于远程*NdkSendAndInvalidate* （[*NDK\_FN\_发送\_和\_无效*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_send_and_invalidate)）调用而导致的**NdkOperationTypeReceiveAndInvalidate**完成仍必须使用*NdkGetCqResults* （Not *NdkGetCqResultsEx*n）。 这样做仍必须使接收方上的指定令牌无效，但不会通知接收使用者此失效（使用者必须使用*NdkGetCqResultsEx*来获取此信息）。 对于同一令牌，更高版本的*NdkInvalidate* （[*NDK\_FN\_无效*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_invalidate)）会照常发生。

## <a name="the-rules-for-notification-callbacks"></a>通知回调的规则


提供程序必须调用*NdkCqNotificationCallback* （[*NDK\_FN\_CQ\_通知\_回调*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_cq_notification_callback)）回调一次，并且仅在使用者通过调用*NdkArmCq*。 也就是说，当调用*NdkCqNotificationCallback*回调的条件发生时（即，请求完成在 CQ 中排队时），提供程序必须清除 arm 并调用*NdkCqNotificationCallback*回调。

如果当使用者调用*NdkArmCq*时，CQ 中已存在完成，则提供程序的行为如下所示：

-   如果自上次调用*NdkCqNotificationCallback*回调后，在 CQ 中至少有一个完成项已新放入到中，则提供程序必须立即满足 arm 请求（有关序列化的要求，请参阅下文）。
-   但是，如果 CQ 中的所有完成项也在调用最后一个*NdkCqNotificationCallback*回调时也存在（换言之，使用者调用*NdkArmCq* ，但不删除所有完成，且无新的完成进入 CQ），则提供程序可能会立即满足 arm 请求。

当提供程序需要调用*NdkCqNotificationCallback*回调时，如果已有*NdkCqNotificationCallback*回调正在进行，则提供程序必须延迟对*NdkCqNotificationCallback*的调用。回调到对*NdkCqNotificationCallback*回调的现有调用之后，会将控制权返回给提供程序。 换言之，提供程序负责序列化*NdkCqNotificationCallback*回调。

下表显示了在满足上一个*NdkArmCq*请求之前再次调用*NdkArmCq*的情况下生成的 arm 类型：

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
<th align="left">第二个 arm</th>
<th align="left">第二个 arm 错误</th>
<th align="left">第二个 arm 请求</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>第一 arm</p></td>
<td align="left"><p>随时</p></td>
<td align="left"><p>随时</p></td>
<td align="left"><p>随时</p></td>
</tr>
<tr class="even">
<td align="left"><p>第一 arm 错误</p></td>
<td align="left"><p>随时</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>请求</p></td>
</tr>
<tr class="odd">
<td align="left"><p>请求第一 arm</p></td>
<td align="left"><p>随时</p></td>
<td align="left"><p>请求</p></td>
<td align="left"><p>请求</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题


[网络直接内核提供程序接口（NDKPI）](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






