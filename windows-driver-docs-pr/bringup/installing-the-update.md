---
title: 安装更新
description: 可以使用任何工具安装 Windows 驱动程序安装固件更新包。
ms.assetid: 51C50910-8AA3-4ED9-B469-2325BBD2FB31
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e0f2d08f0cfbd59d55a01c2f925eedaffc3e4e9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534507"
---
# <a name="installing-the-update"></a>安装更新


可以使用任何工具安装 Windows 驱动程序安装固件更新包。 安装过程将固件更新有效负载 (firmware.bin) 复制到已知的系统目录，并创建注册表项必须告诉 Windows 有可用的新更新。 安装完成后，重新启动，以触发实际固件更新过程。

![固件更新包安装过程](images/updateinstallprocess.png)

在下一步启动，并已调用 ExitBootServices() 之前，操作系统加载程序会检查已知的注册表项的位置，以确定新的固件更新负载是否可用。 如果可用的新更新有效负载，OS 加载程序将验证 firmware.bin 针对随驱动程序包的 security 目录的哈希。 如果签名有效，firmware.bin 将传递给通过 UEFI UpdateCapsule() 服务平台固件。

**重要**  目前为止，在平台固件是负责完成固件更新。

 

如果安装了多个固件更新包，OS 加载程序使用的每个可用更新的有效负载调用 UpdateCapsule()。 每个固件负载会单独 capsule，每个目标的固件更新包的 ESRT 条目的 guid 标识。

EFI 系统资源表提供了当前的固件版本和上次更新状态尝试。 操作系统加载程序将使用此信息来评估是否已成功应用更新。 固件状态信息将保留到 OS 中，这样便可用于在 Windows 中运行的固件更新应用程序。 最后，OS 加载程序继续执行启动过程。

## <a name="related-topics"></a>相关主题
[通过固件驱动程序包的系统和设备固件更新](system-and-device-firmware-updates-via-a-firmware-driver-package.md)  
[填充 ESRT 表](populating-the-esrt-table.md)  
[自定义不同的地理区域的固件](customizing-firmware-for-different-geographic-regions.md)  
[创作固件更新包](authoring-a-firmware-update-package.md)  
[认证和签名的更新包](certifying-and-signing-the-update-package.md)  

