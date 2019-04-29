---
title: 减少 I/O 资源使用
description: 减少 I/O 资源使用
ms.assetid: ad83856c-ad1a-42fc-97f0-7881f745174d
keywords:
- I/O 资源使用率减少 WDK
- 资源使用情况 WDK
- WDK 的 I/O 资源
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9dd8e2275454ce40ab7afab5195fe834b41b8701
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380546"
---
# <a name="io-resource-usage-reduction"></a>减少 I/O 资源使用


Microsoft 已实现支持，以帮助减少 PCI、 PCI X 和 PCI Express 设备对 I/O 基址寄存器 （条形图） 访问的输入/输出 (I/O) 空间地址的使用情况的依赖。 使用个人计算机上的 I/O 资源数量逐渐增加多年。 此 PCI、 PCI 的 X 和 PCI Express 总线上的 I/O 资源使用率逐渐成为资源争用问题的原因。 这些问题会变得更糟的是使用 PCI Express 总线，相比那些使用 PCI 和 PCI X 总线，由于客户端和服务器系统中使用的虚拟 PCI PCI 桥数为系统。 因此变得更加必要转换离开在 I/O 资源，到使用内存资源，这是更大量的依赖的硬件设计。 有关如何设备制造商、 驱动程序开发人员、 固件工程师和系统制造商可以禁用未使用的 I/O 条和减少或消除的 I/O 在计算机上使用的空间量的详细信息，请参阅[I/O 资源使用情况减少](https://go.microsoft.com/fwlink/p/?linkid=74197)白皮书。

若要减少 I/O 资源使用情况在 Windows 10 中，将设备驱动程序的 INF 文件中放置以下条目：

```cpp
[DDInstall.HW]
Include=pci.inf
Needs=PciIoSpaceNotRequired.HW
```

在 Windows 8.1 及更早版本，请改为使用此项：

```cpp
[DDInstall.HW]
Include=machine.inf
Needs=PciIoSpaceNotRequired
```
