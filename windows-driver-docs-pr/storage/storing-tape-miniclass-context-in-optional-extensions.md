---
title: 将磁带微型类上下文存储在可选扩展中
description: 将磁带微型类上下文存储在可选扩展中
ms.assetid: 9b259403-2fae-4708-8765-2d998a535620
keywords:
- 磁带驱动程序 WDK 存储，上下文存储
- 存储磁带驱动程序 WDK，上下文存储
- WDK 存储上下文
- 上下文存储 WDK 磁带
- 特定于驱动程序 minitape 扩展 WDK 磁带
- 特定于命令的命令扩展 WDK 磁带
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9a3330ca4ee4770a4bb3bfbb47c45e103b9f217
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376466"
---
# <a name="storing-tape-miniclass-context-in-optional-extensions"></a>将磁带微型类上下文存储在可选扩展中


## <span id="ddk_storing_tape_miniclass_context_in_optional_extensions_kg"></span><span id="DDK_STORING_TAPE_MINICLASS_CONTEXT_IN_OPTIONAL_EXTENSIONS_KG"></span>


磁带 miniclass 驱动程序可以将上下文存储在两个可选扩展：

1.  特定于驱动程序 minitape 扩展

    使用时，此扩展通常将存储有关设备功能 （SCSI 查询数据或等效） 的信息。 支持多个设备的驱动程序可以存储每个设备的详细信息而不是重复查询设备。

    Miniclass 驱动程序指定的 minitape 扩展中的大小**MinitapeExtensionSize**磁带成员\_INIT\_数据\_EX 结构，它将传递给**TapeClassInitialize**从其**DriverEntry**例程。 磁带类驱动程序分配请求的存储代表 miniclass 驱动程序。 Miniclass 驱动程序初始化 TapeMiniExtensionInit 例程的可选扩展。 Minitape 扩展保持有效，直到卸载该驱动程序为止。

2.  特定于命令的命令扩展

    使用时，此扩展存储可能会超过一次调用，以处理单个请求的磁带 miniclass 例程的调用之间的特定于命令的上下文。 例如，从测试状态可能存储磁带 miniclass 驱动程序的 TapeMiniGetStatus 例程\_单元\_准备命令时它确定是否在磁带驱动器还需要清理的命令扩展中。

    Miniclass 驱动程序指定的命令扩展中的大小**CommandExtensionSize**磁带成员\_INIT\_数据\_EX 结构，它将传递给**TapeClassInitialize**从其**DriverEntry**例程。

    处理设备控制请求的特定于设备的方面的所有磁带 miniclass 例程都被赋予一个指针，命令扩展时调用它们。 磁带类驱动程序之前调用此类 miniclass 例程分配命令扩展的存储。 Miniclass 例程初始化到给定的请求; 进程在首次调用的命令扩展也就是说，当*CallNumber*到例程的参数等于零。 命令扩展一直有效，直到磁带 miniclass 例程将返回任一磁带\_状态\_成功或错误状态。

 

 




