---
title: 实现 NDKPI 函数
description: NDK 支持的微型端口驱动程序必须注册所有 NDK_FN_XXX 的回调函数的入口点。 所有 NDKPI 提供程序回调函数都是必需的;无是可选的。
ms.assetid: 9A7D5F77-C26A-47B6-9F8E-ECB80D4FF384
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bfdd195d03f2a5576b140f56b5eb08cda2b4581
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521435"
---
# <a name="implementing-ndkpi-functions"></a>实现 NDKPI 函数


NDK 支持的微型端口驱动程序必须注册所有的入口点[NDK\_FN\_*XXX*回调函数](https://msdn.microsoft.com/library/windows/hardware/jj206453)。 所有 NDKPI 提供程序回调函数都是必需的;无是可选的。

若要注册这些函数的支持，微型端口驱动程序存储其入口点在"对象的调度表"中列出的结构中的以下表的列：

| 对象类型                                               | 此函数所创建的                                                                                                       | 对象的调度表                                                      |
|-----------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------|
| [**NDK\_ADAPTER**](https://msdn.microsoft.com/library/windows/hardware/hh439848)                  | [*OPEN\_NDK\_ADAPTER\_HANDLER*](https://msdn.microsoft.com/library/windows/hardware/hh440105)                                                             | [**NDK\_适配器\_调度**](https://msdn.microsoft.com/library/windows/hardware/hh439850)                  |
| [**NDK\_连接器**](https://msdn.microsoft.com/library/windows/hardware/hh439852)              | [*NDK\_FN\_CREATE\_CONNECTOR*](https://msdn.microsoft.com/library/windows/hardware/hh439872)                                                               | [**NDK\_连接器\_调度**](https://msdn.microsoft.com/library/windows/hardware/hh439853)              |
| [**NDK\_CQ**](https://msdn.microsoft.com/library/windows/hardware/hh439854)                            | [*NDK\_FN\_CREATE\_CQ*](https://msdn.microsoft.com/library/windows/hardware/hh439873)                                                                             | [**NDK\_CQ\_DISPATCH**](https://msdn.microsoft.com/library/windows/hardware/hh439855)                            |
| [**NDK\_LISTENER**](https://msdn.microsoft.com/library/windows/hardware/hh439918)                | [*NDK\_FN\_CREATE\_LISTENER*](https://msdn.microsoft.com/library/windows/hardware/hh439874)                                                                 | [**NDK\_侦听器\_调度**](https://msdn.microsoft.com/library/windows/hardware/hh439919)                |
| [**NDK\_MR**](https://msdn.microsoft.com/library/windows/hardware/hh439922)                            | [*NDK\_FN\_CREATE\_MR*](https://msdn.microsoft.com/library/windows/hardware/hh439875)                                                                             | [**NDK\_MR\_DISPATCH**](https://msdn.microsoft.com/library/windows/hardware/hh439924)                            |
| [**NDK\_MW**](https://msdn.microsoft.com/library/windows/hardware/hh439926)                            | [*NDK\_FN\_CREATE\_MW*](https://msdn.microsoft.com/library/windows/hardware/hh439876)                                                                             | [**NDK\_MW\_DISPATCH**](https://msdn.microsoft.com/library/windows/hardware/hh439927)                            |
| [**NDK\_PD**](https://msdn.microsoft.com/library/windows/hardware/hh439931)                            | [*NDK\_FN\_CREATE\_PD*](https://msdn.microsoft.com/library/windows/hardware/hh439877)                                                                             | [**NDK\_PD\_调度**](https://msdn.microsoft.com/library/windows/hardware/hh439932)                            |
| [**NDK\_QP**](https://msdn.microsoft.com/library/windows/hardware/hh439933)                            | [*NDK\_FN\_创建\_QP* ](https://msdn.microsoft.com/library/windows/hardware/hh439878)或[ *NDK\_FN\_创建\_QP\_WITH\_SRQ*](https://msdn.microsoft.com/library/windows/hardware/hh439880)   | [**NDK\_QP\_调度**](https://msdn.microsoft.com/library/windows/hardware/hh439934)                            |
| [**NDK\_SHARED\_ENDPOINT**](https://msdn.microsoft.com/library/windows/hardware/hh439937) | [*NDK\_FN\_CREATE\_SHARED\_ENDPOINT*](https://msdn.microsoft.com/library/windows/hardware/hh439882)                                                  | [**NDK\_SHARED\_ENDPOINT\_DISPATCH**](https://msdn.microsoft.com/library/windows/hardware/hh439938) |
| [**NDK\_SRQ**](https://msdn.microsoft.com/library/windows/hardware/hh439939)                          | [*NDK\_FN\_创建\_SRQ* ](https://msdn.microsoft.com/library/windows/hardware/hh439883)或[ *NDK\_FN\_创建\_QP\_WITH\_SRQ*](https://msdn.microsoft.com/library/windows/hardware/hh439880) | [**NDK\_SRQ\_DISPATCH**](https://msdn.microsoft.com/library/windows/hardware/hh439940)                          |

 

## <a name="related-topics"></a>相关主题


[网络直接内核提供程序接口 (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






