---
title: 包含 IP 帮助程序的标头文件
description: 包含 IP 帮助程序的标头文件
ms.assetid: f4642717-223c-425a-8389-cbbc75567ae3
keywords:
- IP 帮助程序 WDK 网络，包括头文件
- 头文件 WDK IP 帮助程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96e9427cf63f510262c5704092267661f34edc0a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327779"
---
# <a name="including-header-files-for-ip-helper"></a>包含 IP 帮助程序的标头文件


使用内核模式 IP 帮助程序函数、 MIB 结构和 Netioapi.h 中声明的枚举的驱动程序代码必须具有**\#包括**语句按以下顺序。

```C++
#include <ntddk.h>
#include <netioapi.h>
```

**请注意**  驱动程序代码中不包括 Iphlpapi.h。 它仅用于用户模式应用程序。

 

当将 Netioapi.h 用于内核模式驱动程序时，它已包含网络定义 Winsock 内核、 网络接口信息、 网络层和网络驱动程序接口规范 (NDIS) 类型的标头文件。

因此，则驱动程序代码中包括以下标头文件：

- Ifdef.h
- Nldef.h
- Ws2def.h
- Ws2ipdef.h

IP 帮助程序函数和 MIB 结构的用户模式版本有关的信息，请参阅 Windows SDK 文档。

 

 





