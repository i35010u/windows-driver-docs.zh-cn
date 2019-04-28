---
title: 设备安装期间的自动配置
description: 设备安装期间的自动配置
ms.assetid: 04b53767-4b5e-450d-96ab-b029cdf62b36
keywords:
- 自动配置 WDK 打印机，在设备安装过程
- 打印机自动配置 WDK 打印机，在设备安装过程
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d048827d1228847228f5203fb0cb41cc4e90cdc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350784"
---
# <a name="autoconfiguration-during-device-installation"></a>设备安装期间的自动配置


下图显示数据流中自动配置，安装设备时。

![当设备安装说明中自动配置的数据流关系图](images/autocfginstall.png)

1.  安装打印机时，后台处理程序初始化该驱动程序通过调用`DrvPrinterEvent`并传递打印机\_事件\_初始化的调用中。

2.  驱动程序使用[bidi 通信接口](https://msdn.microsoft.com/library/windows/hardware/ff545163)以获取感兴趣的其中包括可安装选项的值，例如数据\\Printer.Configuration.DuplexUnit:Installed 和\\Printer.Configuration.HardDisk:Installed。

3.  双向通信接口查询这些属性的值的端口的监视器。 端口监视器可能具有某些请求在其缓存中的数据。 以下步骤中演示的目的，假设的值\\Printer.Configuration.HardDisk:Installed 位于端口监视器的缓存，但为\\Printer.Configuration.DuplexUnit:Installed 不是。

4.  如果端口监视器有一个缓存，并且已在其中保存一个或多个请求的值，则端口监视器返回这些值到 bidi 通信接口。 对于不在其缓存中的任何值，将端口监视器返回错误\_否\_数据。 请注意，是否端口监视器实现一个缓存，但缓存为空，则 bidi 查询可能会失败。 若要避免此问题，端口监视器应填充其缓存时通知 bidi 通信接口。

5.  双向通信接口将传递给驱动程序收到来自端口监视器的信息。 如果端口监视器从 bidi 通信接口调用出于任何原因导致失败，该驱动程序应设置这些属性的默认值。 只要端口监视器接收请求的属性的相关信息，它应发送通知，其中包含此信息来 bidi 通信接口。

    该驱动程序使用的值更新注册表\\Printer.Configuration.HardDisk:Installed （从端口监视器的缓存中获得） 和默认值为\\Printer.Configuration.DuplexUnit:Installed。

6.  端口监视器查询适用于这两个值，包括已缓存的值的设备 (\\Printer.Configuration.HardDisk:Installed)。

7.  设备将查询属性及其值发送到端口监视器。 对于任何属性值已不存在于缓存中，或其值不同于缓存中，端口监视器将在其缓存中的新值。

8.  端口监视器将包含以前已不在缓存或更改任何值的通知发送到后台处理程序。 在此示例中，端口监视器将通知发送到后台处理程序有关的新值\\Printer.Configuration.DuplexUnit:Installed。 请注意，是否缓存的值已从设备收到的新值相同，端口监视器不会发送通知到后台处理程序。

9.  后台处理程序响应的通知从端口监视器通过调用`DrvPrinterEvent`，并传递打印机\_事件\_配置\_更新调用中的所有更改后的值有关的信息的补充。 此操作有两个用途： 以通知其值第一次放在缓存或更改其值的任何属性的值的驱动程序 (\\Printer.Configuration.DuplexUnit:Installed，在此示例中); 若要更新的注册表。 为每个打印机后台处理程序序列化到其调用`DrvPrinterEvent`，以便该驱动程序不需要是线程安全的。

    由于设备信息存储在注册表中，该驱动程序可以满足调用以更新 UI 或设备而无需直接与物理设备进行通信的功能信息。 该驱动程序可以确定存储在注册表中的信息是正确的因为更改通知触发的驱动程序查询设备并更新设备配置状态。

10. 该驱动程序更新根据最新的配置 UI。

    该驱动程序可以确定当在设备安装过程中发生了更改因为通知消息传送的更改的值。 但是，如果太大，无法通过的通知机制发送通知，通知将具有一个或多个 ReducedSchema 实例，每个这指示已更改设备特征，但没有它的新值的任何详细信息。

 

 




