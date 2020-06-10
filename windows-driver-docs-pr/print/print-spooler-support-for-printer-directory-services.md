---
title: 打印机目录服务的打印后台处理程序支持
description: 打印机目录服务的打印后台处理程序支持
ms.assetid: 23cd73a5-8628-4471-a6c6-e056536fcc75
keywords:
- 目录服务 WDK 打印机
- 打印后台处理程序目录服务支持 WDK
- 发布 WDK 打印机
ms.date: 06/09/2020
ms.localizationpriority: medium
ms.openlocfilehash: 71565b5891304d4493d95ff330aeeba699728517
ms.sourcegitcommit: 88f6e7355de9e0714057020557dc8c7831e90e7b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/10/2020
ms.locfileid: "84638449"
---
# <a name="print-spooler-support-for-printer-directory-services"></a>打印机目录服务的打印后台处理程序支持

目录服务的打印后台处理程序支持包括：

- 发布打印队列

- 维护三个注册表项

- 允许访问后台处理程序维护的注册表项

- 返回打印队列的发布状态

## <a name="publishing-print-queues"></a>发布打印队列

使用**SetPrinter**函数，调用方可以发布、取消发布或更新打印队列对象。 为此，必须使用打印机信息7的输入结构调用**SetPrinter**函数 \_ \_ 。

仅当打印队列对象与描述用户所连接到的打印服务器的计算机对象关联时，才能发布该对象。 用户发布打印队列的能力取决于用户的客户端安全上下文中的访问权限。 如果对打印队列具有 "管理打印机" 权限，则可以发布打印队列。

## <a name="maintaining-three-registry-keys"></a>维护三个注册表项

三个注册表项包含在打印队列对象中发布的所有信息的副本。 使用 winspool.drv 中定义的以下标识符引用这三个键：

| 密钥 | 定义 |
| --- | --- |
| SPLDS_DRIVER_KEY | 用于存储驱动程序特定的信息，这些信息可由后台处理程序或驱动程序提供。 |
| SPLDS_SPOOLER_KEY | 用于存储后台处理程序提供的特定于后台处理程序的信息。 |
| SPLDS_USER_KEY | 用于存储应用程序提供的用户特定的信息。 |

后台处理程序使用 SPLDS \_ 驱动程序 \_ 密钥来存储可通过调用 Microsoft Windows SDK **DeviceCapabilities**函数获取的驱动程序功能。 驱动程序负责存储后台处理程序无法获取的驱动程序功能，如打印机[驱动程序对打印机目录服务的支持](printer-driver-support-for-printer-directory-services.md)中所述。 存储在这些注册表项下的值必须**通过 \_ SPLDS**前缀常量标识，在 winspool.drv 中定义。

后台处理程序将跟踪自上次更新打印队列对象以来这些项下已修改了哪些值。 每次后台处理程序发布或更新打印队列对象时，都会将所有修改的值复制到对象中。

## <a name="allowing-access-to-spooler-maintained-registry-keys"></a>允许访问后台处理程序维护的注册表项

使用后台处理程序，打印机驱动程序可以通过调用**SetPrinterDataEx**、 **GetPrinterDataEx**和**EnumPrinterDataEx**函数来访问这三个后台处理程序维护的注册表项，Microsoft Windows SDK 文档中对这些功能进行了说明。 **SetPrinterDataEx**函数设置键下的值，而**GetPrinterDataEx**和**EnumPrinterDataEx**返回当前值。 （驱动程序不应在 SPLDS \_ 下设置值后台处理程序 \_ 密钥。）这些函数的调用方不指定完整的注册表路径;函数自动确定指定打印队列的注册表项的路径。

## <a name="returning-a-print-queues-publication-state"></a>返回打印队列的发布状态

使用**GetPrinter**函数，调用方可以确定当前是否已发布打印队列。 为此，必须使用打印机信息7的输入结构调用**GetPrinter**函数 \_ \_ 。 该函数返回打印队列的发布状态（已发布或未发布）和对象标识符。

Windows SDK 文档中介绍了前面提到的所有函数。 这些函数不是专门用于与 DS 相关的操作。
