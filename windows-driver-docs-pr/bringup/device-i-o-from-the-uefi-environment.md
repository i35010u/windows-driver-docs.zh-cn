---
title: 来自 UEFI 环境的设备 I/O
description: 当 Windows 操作系统加载程序调用 UpdateCapsule 函数时，将执行 CapsuleHeaderArray 中包含的每个胶囊。
ms.assetid: 843B177F-CD1F-47E6-8F35-0A0FFA8FA192
ms.date: 05/21/2020
ms.localizationpriority: medium
ms.openlocfilehash: 87f54e308f84c6b96fb7b6564ab0197e7da577ba
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769383"
---
# <a name="device-io-from-the-uefi-environment"></a>来自 UEFI 环境的设备 I/O

当 Windows 操作系统加载程序调用 UpdateCapsule 函数时，将执行 CapsuleHeaderArray 中包含的每个胶囊。 胶囊执行的顺序取决于 UEFI 固件实现，并且胶囊无法对其相对于其他马蹄形执行的顺序进行任何假设，或对其他马蹄形执行任何依赖项。 每个胶囊都是一个自包含负载，同时包含可执行的 UEFI 代码来管理更新和固件映像。

调用胶囊后，胶囊中包含的可执行代码负责打开与目标设备的通信通道。 适当的通道将取决于系统的设备拓扑、目标设备的功能，以及特定 UEFI 实现提供的 UEFI 启动服务和驱动程序。 胶囊实现人员可能需要咨询 UEFI BIOS 供应商，了解目标 UEFI 环境中的可用选项。 通常，通过利用给定设备的 UEFI 设备驱动程序建立通信。 使用此驱动程序，胶囊更新代码可以通过已知的设备路径（使用适当的协议）绑定到设备。

建立通信后，更新管理代码会将固件映像写入目标设备。 完成更新后，相应的返回状态代码将写入到 ESRT 中设备的固件资源条目。 然后，更新管理代码将控制权返回给 UpdateCapsule 函数。

有关 UpdateCapsule 函数、胶囊结构和 UEFI 引导服务驱动程序和协议的详细信息，请参阅[uefi 规范](https://uefi.org/specifications)。

## <a name="related-topics"></a>相关主题

[ESRT 表定义](esrt-table-definition.md)  

[即插即用设备](plug-and-play-device.md)  

[创作更新驱动程序包](authoring-an-update-driver-package.md)  

[处理更新](processing-updates.md)

[无缝危机预防和恢复](seamless-crisis-prevention-and-recovery.md)

[固件更新状态](firmware-update-status.md)  
