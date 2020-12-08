---
title: 安装更新
description: 可以使用安装 Windows 驱动程序的任何工具安装固件更新包。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25eff384da21e0e34cce3f0ada149c66ce941e41
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784229"
---
# <a name="installing-the-update"></a>安装更新


可以使用安装 Windows 驱动程序的任何工具安装固件更新包。 安装过程会将固件更新有效负载 (固件复制) 到众所周知的系统目录，并创建告诉 Windows 有新的更新可用所需的注册表项。 安装完成后，需要重新启动才能触发实际固件更新过程。

![固件更新包安装过程](images/updateinstallprocess.png)

在下一次启动过程中，在调用 ExitBootServices ( # A1 之前，操作系统加载程序将检查众所周知的注册表项位置以确定是否有新的固件更新负载可用。 如果新的更新有效负载可用，操作系统加载程序会对照随驱动程序包一起提供的安全目录来验证固件的哈希。 如果签名有效，则固件会通过 UEFI UpdateCapsule ( # A1 服务传递到平台固件。

**重要提示**  此时，平台固件只负责完成固件更新。

 

如果安装了多个固件更新包，操作系统加载程序将使用每个可用更新的有效负载 ( # A1 调用 UpdateCapsule。 每个固件负载都将是一个单独的胶囊，每个都由目标固件更新包的 ESRT 条目的 GUID 标识。

EFI 系统资源表提供当前固件版本以及上次尝试更新的状态。 操作系统加载器使用此信息来评估更新是否已成功应用。 固件状态信息将保留在操作系统中，使其可用于在 Windows 中运行的固件更新应用程序。 最后，操作系统加载程序将继续执行启动过程。

## <a name="related-topics"></a>相关主题
[通过固件驱动程序包进行的系统和设备固件更新](system-and-device-firmware-updates-via-a-firmware-driver-package.md)  
[填充 ESRT 表](populating-the-esrt-table.md)  
[自定义不同地理区域的固件](customizing-firmware-for-different-geographic-regions.md)  
[创作固件更新包](authoring-a-firmware-update-package.md)  
[认证和签署更新包](certifying-and-signing-the-update-package.md)  

