---
title: NDKPI 完成处理要求
description: NDK 使用者和 NDK 提供程序必须遵循这些要求才能完成 NDKPI 处理。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 396f0eb62d07babe8d07840c9c3e8e20646b219d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799381"
---
# <a name="ndkpi-completion-handling-requirements"></a>NDKPI 完成处理要求


NDK 使用者和 NDK 提供程序必须遵循这些要求才能完成 NDKPI 处理。

## <a name="the-rules-for-ndkgetcqresults-ndkgetcqresultsex-and-ndkarmcq-functions"></a>用于 NdkGetCqResults、NdkGetCqResultsEx 和 NdkArmCq 函数的规则


使用者将始终在同一完成队列中序列化对这些提供程序函数的调用 (CQ) 对象 ([**NDK \_ CQ**](/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_cq)) ：

-   *NdkGetCqResults* ([*NDK \_ FN \_ GET \_ CQ \_ 结果*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_get_cq_results)) 
-   *NdkGetCqResultsEx* ([*NDK \_ FN \_ GET \_ CQ \_ 结果， \_ 如*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_get_cq_results_ex)) 
-   *NdkArmCq* ([*NDK \_ FN \_ \_ CQ*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_arm_cq)) 

这意味着，不仅使用者将不会同时调用相同的提供程序函数，还会永远不会从多个线程同时调用相同 CQ 的这些函数的任何组合。

由于远程 *NdkSendAndInvalidate* ([*NDK \_ FN \_ SEND \_ 和 \_ 无效*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_send_and_invalidate)) 调用而导致的 **NdkOperationTypeReceiveAndInvalidate** 完成仍必须使用 *NdkGetCqResults* (不 *NdkGetCqResultsEx* n) 来检索。 这样做仍必须使接收方上的指定令牌无效，但不会通知接收使用者此失效 (使用者必须使用 *NdkGetCqResultsEx* 来) 获取此信息。 更高版本的 *NdkInvalidate* ([*NDK \_ FN 会 \_ 使*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_invalidate) 同一令牌的) 失效。

## <a name="the-rules-for-notification-callbacks"></a>通知回调的规则


提供程序必须调用 *NdkCqNotificationCallback* ([*NDK \_ FN \_ CQ \_ 通知 \_ 回调*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_cq_notification_callback)仅) 回调一次，并且仅在使用者通过调用 *NdkArmCq* 获得 *NdkCqNotificationCallback* 回调后才调用。 也就是说，提供程序必须清除 arm，并在调用 NdkCqNotificationCallback *回调的* 条件 (时调用，否则 *NdkCqNotificationCallback* ，在 CQ) 中，请求完成将排队。

如果当使用者调用 *NdkArmCq* 时，CQ 中已存在完成，则提供程序的行为如下所示：

-   如果自上次调用 *NdkCqNotificationCallback* 回调后，将至少一个完成时间插入到 CQ 中，则提供程序必须立即满足 arm 请求 (参见下面的) 的序列化要求。
-   但是，如果 CQ 中的所有完成项也同时出现在 (*NdkCqNotificationCallback* 的情况下，则使用者调用 *NdkArmCq* ，而不会删除所有完成，且无新的完成操作进入 CQ) 中，则提供程序可能会立即满足 arm 请求。

当提供程序需要调用 *NdkCqNotificationCallback* 回调时，如果已有一个 *NdkCqNotificationCallback* 回调正在进行，则该提供程序必须延迟对 *NdkCqNotificationCallback* 回调的调用，直到 *对该访问* 接口的现有调用返回控制权。 换言之，提供程序负责序列化 *NdkCqNotificationCallback* 回调。

下表显示了在满足上一个 *NdkArmCq* 请求之前再次调用 *NdkArmCq* 的情况下生成的 arm 类型：

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
<td align="left"><p>ANY</p></td>
<td align="left"><p>ANY</p></td>
<td align="left"><p>ANY</p></td>
</tr>
<tr class="even">
<td align="left"><p>第一 arm 错误</p></td>
<td align="left"><p>ANY</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>请求</p></td>
</tr>
<tr class="odd">
<td align="left"><p>请求第一 arm</p></td>
<td align="left"><p>ANY</p></td>
<td align="left"><p>请求</p></td>
<td align="left"><p>请求</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题


[网络直接内核提供程序接口 (NDKPI)](./overview-of-network-direct-kernel-provider-interface--ndkpi-.md)

 

