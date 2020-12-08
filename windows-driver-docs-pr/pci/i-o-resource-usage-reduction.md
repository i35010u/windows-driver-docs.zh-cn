---
title: 减少 I/O 资源使用
description: 减少 I/O 资源使用
keywords:
- I/o 资源使用率降低 WDK
- 资源使用情况 WDK
- I/o 资源 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9cc2e4f47886b7ca226e9b718c28055e1a9f7bc0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812557"
---
# <a name="io-resource-usage-reduction"></a>减少 I/O 资源使用


Microsoft 已经实现了支持，有助于降低 PCI、PCI-X 和 PCI Express 设备使用输入/输出 (i/o 基址注册 (条) 所访问的 i/o) 空间地址的依赖关系。 个人计算机上使用的 i/o 资源数已持续超过多年。 PCI、PCI-X 和 PCI Express 总线上的此 i/o 资源使用情况越来越导致了资源争用问题。 由于客户端和服务器系统中使用的虚拟 PCI 到 PCI 桥，与使用 pci Express 总线的系统相比，这些问题会变得更糟，因为这两个系统使用 pci Express 总线。 因此，更有必要将硬件设计转换为依赖 i/o 资源和使用内存资源，这要大量得多。 若要详细了解设备制造商、驱动程序开发人员、固件工程师和系统制造商如何禁用未使用的 i/o 栏以及减少或消除计算机中使用的 i/o 空间量，请参阅 [I/o 资源使用情况缩减](https://go.microsoft.com/fwlink/p/?linkid=74197) 白皮书。

若要减少 Windows 10 中的 i/o 资源使用情况，请将以下条目放入设备驱动程序的 INF 文件中：

```cpp
[DDInstall.HW]
Include=pci.inf
Needs=PciIoSpaceNotRequired.HW
```

在 Windows 8.1 和更早版本中，请改为使用此项：

```cpp
[DDInstall.HW]
Include=machine.inf
Needs=PciIoSpaceNotRequired
```
