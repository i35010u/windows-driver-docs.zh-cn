---
title: 通过使用即插即用的 I/O 请求访问内存
description: 使用即插即用 I/O 请求访问 PCMCIA 属性内存
ms.assetid: ee2f9d9f-9e2b-4ecf-ba6d-4baad3653301
keywords:
- 属性内存 WDK PCMCIA 总线，插 I/O 请求
- 即插即用 WDK PCMCIA 总线
- 即插即用 WDK PCMCIA 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4be854b7d1eaa69ea3e086dcb93ea6d8e1ce8970
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564999"
---
# <a name="access-pcmcia-attribute-memory-by-using-a-plug-and-play-io-request"></a>使用即插即用 I/O 请求访问 PCMCIA 属性内存





本部分介绍如何 PC 卡或 Cardbus 卡驱动程序可以使用插 I/O 请求访问属性的内存。

驱动程序通常使用此方法初始化设备，配置设备，或从设备获取信息。 驱动程序应使用此方法，如果 I/O 开销是可以接受的并且访问可按 IRQL&lt;调度\_级别。

驱动程序只能在 IRQL 运行时使用此方法&lt;调度\_级别。

驱动程序将执行以下一系列操作：

-   创建并初始化新的 IRP\_MJ\_即插即用的请求。

    该驱动程序指定任一配置文件[ **IRP\_MN\_读取\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff551727)或[ **IRP\_MN\_编写\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff551769)较小函数。

-   获取下一步的堆栈位置。

-   设置的以下成员**Parameters.ReadWriteConfig**新的堆栈位置中的结构：

    <a href="" id="whichspace"></a>**WhichSpace**  
    指定的值 PCCARD\_特性\_内存。

    <a href="" id="buffer"></a>**缓冲区**  
    指向该驱动程序分配访问权限的分页内存缓冲区的指针。 写入操作，该缓冲区包含要写入到配置区域的数据。 对于读取操作，缓冲区是零填充缓冲区。 在请求完成后，此缓冲区包含从设备读取的属性内存的副本。

    <a href="" id="offset"></a>**Offset**  
    指定相对于基属性内存读取或写入操作的开始处的偏移量的单词。

    <a href="" id="length"></a>**长度**  
    指定以字节为单位的驱动程序将为请求分配的缓冲区的大小。

-   设置完成例程。

-   发送请求，关闭设备堆栈。

 

 





