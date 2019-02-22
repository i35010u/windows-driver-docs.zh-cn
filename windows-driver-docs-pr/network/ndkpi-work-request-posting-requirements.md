---
title: NDKPI 工作请求发布要求
description: 本部分介绍 NDKPI 工作请求发布要求
ms.assetid: 2BF6F253-FCB4-4A61-9A67-81092F3C44E4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c063b33f5396498d020e4150a1ffc71f35fb6755
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522002"
---
# <a name="ndkpi-work-request-posting-requirements"></a>NDKPI 工作请求发布要求


## <a name="work-request-posting-rules-for-the-consumer"></a>对于使用者发布规则的工作请求


NDK 使用者会发起方队列中发布以下类型的工作请求：

-   *NdkBind* ([*NDK\_FN\_BIND*](https://msdn.microsoft.com/library/windows/hardware/hh439859))
-   *NdkFastRegister* ([*NDK\_FN\_FAST\_REGISTER*](https://msdn.microsoft.com/library/windows/hardware/hh439887))
-   *NdkInvalidate* ([*NDK\_FN\_INVALIDATE*](https://msdn.microsoft.com/library/windows/hardware/hh439901))
-   *NdkRead* ([*NDK\_FN\_READ*](https://msdn.microsoft.com/library/windows/hardware/hh439906))
-   *NdkSend* ([*NDK\_FN\_SEND*](https://msdn.microsoft.com/library/windows/hardware/hh439914))
-   *NdkSendAndInvalidate* ([*NDK\_FN\_SEND\_AND\_INVALIDATE*](https://msdn.microsoft.com/library/windows/hardware/dn265507))
-   *NdkWrite* ([*NDK\_FN\_WRITE*](https://msdn.microsoft.com/library/windows/hardware/hh439917))

使用者将发布*使 NdkReceive* ([*NDK\_FN\_接收*](https://msdn.microsoft.com/library/windows/hardware/hh439907)) 上接收队列的请求。

使用者将发布所有这些请求到相同的单个队列上[ **NDK\_QP** ](https://msdn.microsoft.com/library/windows/hardware/hh439933)或[ **NDK\_SRQ** ](https://msdn.microsoft.com/library/windows/hardware/hh439939)以序列化的方式。 换而言之，使用者再也不会对请求的任何工作函数的两个并发调用上属于同一个单个队列**NDK\_QP**或**NDK\_SRQ**。

这意味着，例如，该并发*使 NdkReceive*的调用不会颁发、 并发*NdkSend*并*NdkWrite*不会发出调用，但并发*使 NdkReceive*并*NdkWrite*调用可能会对相同发出[ **NDK\_QP**](https://msdn.microsoft.com/library/windows/hardware/hh439933)。

## <a name="work-request-posting-rules-for-the-provider"></a>为提供程序发布规则的工作请求


提供程序不应具有更高版本的工作请求函数内部的任何冗余锁，因为可确保由使用者要序列化。

提供程序必须能够处理*NdkFlush* ([*NDK\_FN\_刷新*](https://msdn.microsoft.com/library/windows/hardware/hh439889)) 可能与工作并发调用的调用上请求调用相同[ **NDK\_QP**](https://msdn.microsoft.com/library/windows/hardware/hh439933)。

提供程序必须能够处理**NdkCloseConnector**调用 (在后续任务[ **NDK\_连接器**](https://msdn.microsoft.com/library/windows/hardware/hh439852)对象[ **NDK\_QP**](https://msdn.microsoft.com/library/windows/hardware/hh439933))，不能与工作请求调用同时对调用相同**NDK\_QP**。

## <a name="related-topics"></a>相关主题


[网络直接内核提供程序接口 (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






