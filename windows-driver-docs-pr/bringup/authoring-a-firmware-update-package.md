---
title: 创作固件更新包
description: 每个固件更新包都包含单个二进制文件，其中包含完整的固件负载 (例如，) 以及 Windows 用于验证固件的安全目录。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 368c0eb96a0026f2bb4a3660b29746aab26e71c8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789143"
---
# <a name="authoring-a-firmware-update-package"></a>创作固件更新包


每个固件更新包都包含单个二进制文件，其中包含完整的固件负载 (例如，) 以及 Windows 用于验证固件的安全目录。 有关安全目录和驱动程序的详细信息，请参阅 [目录文件和数字签名](../install/catalog-files.md) 和 [为 PnP 驱动程序包创建编录文件](../install/creating-a-catalog-file-for-a-pnp-driver-package.md)。

固件更新包必须能够更新以下一种或多种固件类型：

-   UEFI 系统固件。
-   系统中单个设备的固件。

建议每个固件更新包都以单一固件资源为 (UEFI 系统固件或单个设备) 为目标，但是在某些情况下，具有更新系统固件和一个或多个设备的单个固件更新包非常有利。

**注意**  一个设备不能作为多个固件更新包的目标。 如果设备被包含系统固件的固件更新包作为目标，则它不能以仅面向设备的第二个固件更新包为目标。

 

1.  若要允许固件更新包以固件更新为适当的系统硬件，Windows 会为 ESRT 中的每个条目提供一个设备实例，其中，此类设备实例将公开一个将其标识为属于 ESRT 条目的硬件 ID。

2.  安装固件更新包后，Windows 会将其作为驱动程序包进行处理。 Windows 将每个更新包的固件负载复制到系统目录下的一个安全位置，准备系统以执行固件更新，并触发系统重启。

    Windows 不支持驱动程序包之间的依赖关系。 因此，在创作新的固件更新包时必须遵守以下要求：

    -   固件更新包必须能够自行安装成功，且不依赖于其他设备固件、系统固件或其他固件更新包。
    
    -   建议将每个更新包定向到系统上的单个设备或 ESRT) 中定义的 UEFI 系统固件 (。
    
    -   每个更新包都必须包含单一固件更新二进制文件 (例如) 的固件。

3.  每个更新包中的固件更新有效负载需要包含在单个二进制文件中。 在系统重新启动时，操作系统加载程序会将每个固件更新包的每个固件更新二进制文件加载到物理内存中，并生成一个指向为安装设置的每个负载文件的指针的数组， (UEFI 2.3.1 规范将此数组称为 CapsuleHeaderArray) 。

4.  此数组是在对 EFI UpdateCapsule ( # A1 函数的调用中传递的。 UpdateCapsule ( # A1 用作邮箱，将每个驱动程序包的固件更新负载传递到平台固件。

5.  每个胶囊 (固件更新负载) 由固件资源的 ESRT 项指定的固件 ID 标识。

6.  收到每个固件更新有效负载后，将处理并应用固件更新请求（如果适用）。

    CapsuleHeaderArray 中的每个条目都是单个连续的数据块，其中包含系统中单个设备的固件驱动程序包的固件更新有效负载。 对于每个目标固件资源，固件更新负载必须包含固件映像以及平台验证所需的所有信息。

    所有固件更新驱动程序包的固件有效负载通过 UEFI UpdateCapsule 服务传递到平台固件。 由于集成设备源自各种不同的 Ihv，因此系统 OEM (和 SoC 制造商) 将需要直接使用这些 Ihv，以确保对给定系统正确编写设备固件更新。 此外，系统 OEM 需要确保 ESRT 条目允许将 UpdateCapsule 包定向到适当的系统。

    例如，许多 Oem 可能会为其系统选择相同型号的移动宽带 (MBB) 设备。 尽管每个系统中的 MBB 设备都是相同的，但每个 OEM 都必须与 MBB IHV 协作，以便为其系统编写自定义的固件更新包。 设备固件更新的这一级别需要在 OEM 系统中处理变量。

    -   根据 OEM 选择的 SoC 以及设备如何连接到 SoC，对设备进行寻址可能会有所不同。
    
    -   系统 OEM 可能会将系统销售到多个移动网络操作员 (Mno) 供经销使用者使用。 MBB 设备必须是 o 感知的，需要将固件自定义并认证到特定 o 的要求。
    
    -   系统可能会出售到全球的多个市场中，每个市场都有不同的射频法规和射频分配。 MBB 设备固件可能需要对其进行自定义以满足这些市场需求。

    每个 OEM 都必须仔细考虑这种特定于设备的要求，并采取必要的措施来确保设备固件可以进行适当的定向和更新。 这需要仔细管理 ESRT 条目以确保可以正确部署设备固件。

7.  编写更新包后，需要将其提交到 Microsoft 进行认证和签名。

## <a name="related-topics"></a>相关主题
[通过固件驱动程序包进行的系统和设备固件更新](system-and-device-firmware-updates-via-a-firmware-driver-package.md)  
[填充 ESRT 表](populating-the-esrt-table.md)  
[自定义不同地理区域的固件](customizing-firmware-for-different-geographic-regions.md)  
[认证和签署更新包](certifying-and-signing-the-update-package.md)  
[安装更新](installing-the-update.md)
