---
title: Ws2def.h
description: 本部分包含 Ws2def.h 标头的内核模式网络驱动程序主题。
ms.assetid: D84A448E-5810-485F-9CAC-4366E4223DBE
keywords:
- Ws2def.h 网络驱动程序
ms.date: 08/08/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e2098970cf0809c610199f0940d1bb4c92045e1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359726"
---
# <a name="ws2defh"></a>Ws2def.h

本部分包含 Ws2def.h 标头的内核模式网络驱动程序主题。 此标头包括在 Windows SDK 中，因为它也与用户模式应用程序的网络共享。

Ws2def.h 标头包含 Winsock2 规范的定义。 它包含在 Winsock2.h。 用户模式应用程序应包括 Winsock2.h，而不是无需直接包括 Ws2def.h。 不能由模块，它还包括 Winsock.h 包含 Ws2def.h。

> [!IMPORTANT]
> 本部分的主题包含用于定义、 宏、 Oid、 状态指示和不是网络驱动程序参考 （结构、 枚举、 函数和回调） 的一部分的其他数据结构的页。 
>
> 有关适用于此标头的网络驱动程序参考的详细信息，请参阅[Ws2def.h （参考）](https://msdn.microsoft.com/library/windows/hardware/mt808757)。

## <a name="in-this-section"></a>本节内容

* [AF_INET](af-inet.md)
* [AF_INET6](af-inet6.md)
* [SIO_ADDRESS_LIST_CHANGE](sio-address-list-change.md)
* [SIO_ADDRESS_LIST_QUERY](sio-address-list-query.md)
* [SO_BROADCAST](so-broadcast.md)
* [SO_CONDITIONAL_ACCEPT](so-conditional-accept.md)
* [SO_EXCLUSIVEADDRUSE](so-exclusiveaddruse.md)
* [SO_KEEPALIVE](so-keepalive.md)
* [SO_RCVBUF](so-rcvbuf.md)
* [SO_REUSEADDR](so-reuseaddr.md)



