---
title: PF 微型端口驱动程序的 INF DDInstall.HW 节
description: PF 微型端口驱动程序的 INF DDInstall.HW 节
ms.assetid: 65399462-4AF1-401C-87CB-BF387CA0B053
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b29a7c827b68e0bc6726d6a94693e682c2ab951
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380897"
---
# <a name="inf-ddinstallhw-section-for-pf-miniport-drivers"></a>PF 微型端口驱动程序的 INF DDInstall.HW 节


INF <em>DDInstall</em> **。HW**部分通常用于设置在注册表中，任何特定于设备的信息是否显式**AddReg**指令或使用**Include**和**需要**条目。

PCI Express (PCIe) 物理函数 (PF) 网络适配器的微型端口驱动程序的 INF 文件必须具有<em>DDInstall</em> **。HW**节，其中包含以下 INF 条目：

-   **Include**指定 Windows 操作系统附带的 pci.inf 文件的条目。

-   一个**需要**指定的条目**PciSriovSupported.HW**部分以包含从 pci.inf 文件。 本部分将定义标准 INF 设置适用于支持的单个根 I/O 虚拟化 (SR-IOV) 接口的网络适配器的所有 PF 微型端口驱动程序。

以下是一种<em>DDInstall</em> **。HW** PF 微型端口驱动程序的部分：

``` syntax
[Device_Inst.NT.HW]

Include=pci.inf
Needs=PciSriovSupported.HW
```

有关详细信息*DDInstall*部分中，请参阅[DDInstall 网络 INF 文件中的部分](ddinstall-section-in-a-network-inf-file.md)。

有关详细信息*DDInstall*。硬件部分中，请参阅[ **INF DDInstall.HW 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-hw-section)。

 

 





