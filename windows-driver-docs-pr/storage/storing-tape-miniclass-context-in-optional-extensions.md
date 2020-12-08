---
title: 将磁带微型类上下文存储在可选扩展中
description: 将磁带微型类上下文存储在可选扩展中
keywords:
- 磁带驱动程序 WDK 存储，上下文存储
- 存储磁带驱动程序 WDK，上下文存储
- 上下文 WDK 存储
- 上下文存储 WDK 磁带
- 特定于驱动程序的 minitape 扩展 WDK 磁带
- 命令特定的命令扩展 WDK 磁带
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ebdf5028a1cdcd374ff0ebbc4837df27f43824d7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820543"
---
# <a name="storing-tape-miniclass-context-in-optional-extensions"></a>将磁带微型类上下文存储在可选扩展中


## <span id="ddk_storing_tape_miniclass_context_in_optional_extensions_kg"></span><span id="DDK_STORING_TAPE_MINICLASS_CONTEXT_IN_OPTIONAL_EXTENSIONS_KG"></span>


磁带 miniclass 驱动程序可以将上下文存储在两个可选扩展中：

1.  驱动程序特定的 minitape 扩展

    使用此扩展时，通常会将有关设备功能的信息存储 (SCSI 查询数据或等效) 。 支持多个设备的驱动程序可以存储有关每个设备的详细信息，而不是重复查询设备。

    Miniclass 驱动程序指定 minitape 扩展的大小，该扩展将 **MinitapeExtensionSize** \_ \_ \_ 从其 **DRIVERENTRY** 例程传递到 **TapeClassInitialize** 的磁带初始化数据 EX 结构的 MinitapeExtensionSize 成员中。 磁带类驱动程序代表 miniclass 驱动程序分配请求的存储。 Miniclass 驱动程序使用 TapeMiniExtensionInit 例程初始化可选扩展。 在卸载驱动程序之前，minitape 扩展保持有效。

2.  命令特定的命令扩展

    使用此扩展时，此扩展会在对磁带 miniclass 例程的调用之间存储命令特定的上下文，此例程可能会被调用多次来处理一个请求。 例如，磁带 miniclass 驱动程序的 TapeMiniGetStatus 例程可能会 \_ 在命令扩展中存储 "测试单元就绪" 命令的状态， \_ 同时确定磁带驱动器是否还需要清洗。

    Miniclass 驱动程序指定 **CommandExtensionSize** \_ \_ \_ 从其 **DRIVERENTRY** 例程传递到 **TapeClassInitialize** 的磁带初始化数据 EX 结构的 CommandExtensionSize 成员中命令扩展的大小。

    处理设备控制请求的特定于设备的方面的所有磁带 miniclass 例程在调用时都提供一个指向命令扩展的指针。 在调用此类 miniclass 例程之前，该磁带类驱动程序会为命令扩展分配存储空间。 Miniclass 例程在第一次调用时初始化命令扩展，以处理给定请求;也就是说，例程的 *CallNumber* 参数等于零。 此命令扩展始终有效，直到磁带 miniclass 例程返回 "磁带 \_ 状态 \_ 成功" 或 "错误状态"。

 

 




