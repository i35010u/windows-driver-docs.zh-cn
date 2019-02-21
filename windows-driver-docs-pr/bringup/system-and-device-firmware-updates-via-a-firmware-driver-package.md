---
title: 通过固件驱动程序包的系统和设备固件更新
description: 部署使用固件驱动程序包的固件更新遵循一个相对较简单的过程，可以分为三个阶段
ms.assetid: D649234A-B757-41A6-B2C1-6D43775FF999
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e614ca76be6790021f5b037d42625e2d5be8a09d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519948"
---
# <a name="system-and-device-firmware-updates-via-a-firmware-driver-package"></a>通过固件驱动程序包的系统和设备固件更新


部署使用固件驱动程序包的固件更新遵循一个相对较简单的过程，可以分为三个阶段：

1.  作者固件更新包。
2.  认证和签名的更新包。
3.  安装更新。

下图演示了更详细地介绍此过程。

![系统和设备固件更新过程](images/systemanddevicefirmwareupdateprocess.png)

此过程假定 UEFI 固件更新有效负载已开发、 测试和签名。

1.  固件驱动程序包只需包含固件更新的有效负载，并允许与所有 Windows 驱动程序相同的方式进行分布的固件更新有效负载。
2.  驱动程序包部署到系统后，固件更新有效负载传递给平台固件通过 UEFI UpdateCapsule 服务。
3.  收到的固件更新有效负载，平台固件识别有效负载，并将更新应用。
4.  平台固件更新代码的实现是专有，按原样固件更新有效负载的格式。

设备驱动程序包包含描述包适用的设备的 INF 文件。 固件驱动程序包是相同的。 设备和系统固件资源支持此更新机制必须唯一地标识本身要绑定到固件驱动程序包。 下一节介绍标识机制。

## <a name="in-this-section"></a>本部分内容


-   [填充 ESRT 表](populating-the-esrt-table.md)
-   [自定义不同的地理区域的固件](customizing-firmware-for-different-geographic-regions.md)
-   [创作固件更新包](authoring-a-firmware-update-package.md)
-   [认证和签名的更新包](certifying-and-signing-the-update-package.md)
-   [安装更新](installing-the-update.md)

 

 




