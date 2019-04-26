---
title: 来自 UEFI 环境的设备 I/O
description: 当 Windows OS 加载程序调用 UpdateCapsule 函数时，将执行 CapsuleHeaderArray 中包含每个 capsule。
ms.assetid: 843B177F-CD1F-47E6-8F35-0A0FFA8FA192
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04ee06201013d4f4874021c3a1211b8586026dc5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328065"
---
# <a name="device-io-from-the-uefi-environment"></a>来自 UEFI 环境的设备 I/O


当 Windows OS 加载程序调用 UpdateCapsule 函数时，将执行 CapsuleHeaderArray 中包含每个 capsule。 封装的执行顺序是依赖于 UEFI 固件实现，并 capsule 无法进行任何这一假设条件及其执行顺序相对于其他马蹄形或依赖于其他马蹄形。 每个 capsule 是自包含的有效负载，其中包含这两个可执行 UEFI 代码来管理更新和固件映像。

当调用胶囊形时，capsule 中包含的可执行代码负责打开与目标设备的通信通道。 适当的信道将取决于系统的设备拓扑中，目标设备的 UEFI 引导服务和驱动程序由特定的 UEFI 实现提供的功能。 封装实现程序可能需要咨询有关目标的 UEFI 环境中可用选项的 UEFI BIOS 供应商。 通常情况下，通过利用给定的设备的 UEFI 设备驱动程序建立通信。 此驱动程序，用于将绑定到通过使用适当的协议的已知设备路径设备的封装更新代码。

建立通信后，更新管理代码将写入到目标设备的固件映像。 完成后更新，适当的返回状态代码将写入 ESRT 中的设备的固件资源项。 然后，更新管理代码将控制返回给 UpdateCapsule 函数。

有关 UpdateCapsule 函数的详细信息，请参阅 capsule 和 UEFI 启动服务驱动程序和协议的结构[UEFI 规范](https://go.microsoft.com/fwlink/p/?LinkId=218221)。

## <a name="related-topics"></a>相关主题
[ESRT 表定义](esrt-table-definition.md)  
[Plug and play 设备](plug-and-play-device.md)  
[创作更新驱动程序包](authoring-an-update-driver-package.md)  
[处理更新](processing-updates.md)  
[无缝危机预防和恢复](seamless-crisis-prevention-and-recovery.md)  
[固件更新状态](firmware-update-status.md)  



