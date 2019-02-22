---
title: 启用和禁用 NDK 功能
description: 若要启用或禁用 NDK 功能，NDIS 发出 OID_NDK_SET_STATE OID 请求。 NDK 支持的微型端口驱动程序必须在其 MiniportOidRequest 函数中注册此 OID 的支持。
ms.assetid: A72AD98E-FF84-48FF-B627-5534231244B0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2fa59ae52b875619e834720e95194eab9ddbc424
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546907"
---
# <a name="enabling-and-disabling-ndk-functionality"></a>启用和禁用 NDK 功能


若要启用或禁用 NDK 功能，NDIS 问题[OID\_NDK\_设置\_状态](https://msdn.microsoft.com/library/windows/hardware/hh451812)OID 请求。 NDK 支持的微型端口驱动程序必须注册支持，使此 OID 中其[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)函数。

## <a name="determining-whether-ndk-functionality-can-be-enabled"></a>确定是否可以启用 NDK 功能


 **\*NetworkDirect**关键字确定是否可以启用 NDK 微型端口驱动程序的功能。

如果该关键字的值设置为 1 （"已启用"），可以启用 NDK 功能。

如果设置为 0 ("Disabled")，则不能启用 NDK 功能。

安装微型端口驱动程序时，其 INF 文件设置为 1 （"已启用"） 具有默认情况下该关键字的值。 有关详细信息，请参阅[NDKPI INF 要求](inf-requirements-for-ndkpi.md)。

安装微型端口驱动程序后，管理员可以更新 **\*NetworkDirect**中设置新值的关键字值**高级**适配器属性页。 有关高级属性的详细信息，请参阅[的高级属性页指定配置参数](specifying-configuration-parameters-for-the-advanced-properties-page.md)。

**请注意**  中进行更改后的微型端口驱动程序将自动重启**高级**适配器属性页。

 

## <a name="when-to-enable-or-disable-ndk-functionality"></a>何时启用或禁用 NDK 功能


此状态更改可由触发[OID\_NDK\_设置\_状态](https://msdn.microsoft.com/library/windows/hardware/hh451812)OID 请求或成功或失败适配器本身。

## <a name="enabling-or-disabling-ndk-functionality"></a>启用或禁用 NDK 功能


若要启用或禁用其 NDK 功能，微型端口驱动程序必须发送**NetEventNDKEnable**或**NetEventNDKDisable**到 NDIS 插即用 (PnP) 事件。

若要发送即插即用事件，微型端口驱动程序调用[ **NdisMNetPnPEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff563616)函数，设置**NetPnPEvent**隶属[ **NET\_PNP\_事件\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff568752)结构*NetPnPEvent*参数，如下所示指向：

-   **NetEventNDKEnable**如果 NDK 功能才可用。

-   **NetEventNDKDisable**如果 NDK 功能将被禁用。

**NetEventNDKDisable**即插即用事件触发 NDIS 和上层驱动程序以启动关闭其打开[ **NDK\_适配器**](https://msdn.microsoft.com/library/windows/hardware/hh439848)通过适配器的实例其中的 NDK 功能被禁用。 即插即用事件将保持挂起状态直至将所有打开的**NDK\_适配器**通过适配器的实例闭合。

## <a name="related-topics"></a>相关主题


[网络直接内核提供程序接口 (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






