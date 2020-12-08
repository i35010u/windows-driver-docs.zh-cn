---
title: 通过固件驱动程序包进行的系统和设备固件更新
description: 使用固件驱动程序包部署固件更新遵循一个相对简单的过程，该过程可分为三个阶段
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a79dedd0eab8b2ba94340e3f5b6645246d6db2b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803649"
---
# <a name="system-and-device-firmware-updates-via-a-firmware-driver-package"></a>通过固件驱动程序包进行的系统和设备固件更新


使用固件驱动程序包部署固件更新遵循一个相对简单的过程，该过程可分为三个阶段：

1.  创作固件更新包。
2.  验证更新包并对其进行签名。
3.  安装更新。

下图更详细地演示了此过程。

![系统和设备固件更新过程](images/systemanddevicefirmwareupdateprocess.png)

此过程假定已开发、测试和签名 UEFI 固件更新有效负载。

1.  固件驱动程序包只包含固件更新的负载，并允许按照与所有 Windows 驱动程序相同的方式分发固件更新负载。
2.  将驱动程序包部署到系统后，固件更新负载将通过 UEFI UpdateCapsule 服务传递到平台固件。
3.  收到固件更新有效负载后，平台固件会识别负载并应用更新。
4.  平台固件更新代码的实现是专用的，因为固件更新负载的格式。

设备驱动程序包包含一个 INF 文件，用于描述包适用的设备。 固件驱动程序包是相同的。 支持此更新机制的设备和系统固件资源必须唯一标识自己以绑定到固件驱动程序包。 下一节将介绍标识机制。

## <a name="in-this-section"></a>在本节中


-   [填充 ESRT 表](populating-the-esrt-table.md)
-   [自定义不同地理区域的固件](customizing-firmware-for-different-geographic-regions.md)
-   [创作固件更新包](authoring-a-firmware-update-package.md)
-   [认证和签署更新包](certifying-and-signing-the-update-package.md)
-   [安装更新](installing-the-update.md)

 

 




