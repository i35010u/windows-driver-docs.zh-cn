---
title: 包含 IP 帮助程序的标头文件
description: 包含 IP 帮助程序的标头文件
keywords:
- IP 帮助程序 WDK 网络，包括头文件
- 标头文件 WDK IP 帮助程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd2be3e8016e259f739b5386b59d8f074bb05c79
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840639"
---
# <a name="including-header-files-for-ip-helper"></a>包含 IP 帮助程序的标头文件


使用在 Netioapi 中声明的内核模式 IP Helper 函数、MIB 结构和枚举的驱动程序代码在以下序列中必须具有 **\# include** 语句。

```C++
#include <ntddk.h>
#include <netioapi.h>
```

**注意**  请勿在驱动程序代码中包含 Iphlpapi。 它仅用于用户模式应用程序。

 

当 Netioapi 用于内核模式驱动程序时，它已经包含用于定义 Winsock 内核、网络接口信息、网络层和网络驱动程序接口规范 (NDIS) 类型的网络标头文件。

因此，请不要在驱动程序代码中包含以下标头文件：

- Ifdef。h
- Nldef
- Ws2def.h
- Ws2ipdef

有关 IP Helper 函数和 MIB 结构的用户模式版本的信息，请参阅 Windows SDK 文档。

 

 





