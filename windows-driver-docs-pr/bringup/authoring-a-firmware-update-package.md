---
title: 创作固件更新包
description: 每个固件更新包中包含单个二进制文件包含整个固件负载 (例如 firmware.bin) 和 Windows 用来验证 firmware.bin 安全目录。
ms.assetid: 672F5E45-C0AB-4C19-BB0A-C8B5A66D8EED
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd76f1220c932406313166bc44e3ba1d14772614
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364589"
---
# <a name="authoring-a-firmware-update-package"></a>创作固件更新包


每个固件更新包中包含单个二进制文件包含整个固件负载 (例如 firmware.bin) 和 Windows 用来验证 firmware.bin 安全目录。 有关安全目录和驱动程序的详细信息，请参阅[目录文件和数字签名](https://docs.microsoft.com/windows-hardware/drivers/install/catalog-files)并[为 PnP 驱动程序包创建编录文件](https://docs.microsoft.com/windows-hardware/drivers/install/creating-a-catalog-file-for-a-pnp-driver-package)。

必须能够更新一个或多个以下类型的固件的固件更新包：

-   UEFI 系统固件。
-   用于在系统中的单个设备的固件。

建议每个固件更新包 （UEFI 系统固件或单个设备），将单个固件资源作为目标，但可能会有情况会在便利有更新系统固件，一个单一的固件更新包或更多设备。

**请注意**  设备不能由多个固件更新包目标。 如果固件更新包，其中也包括系统固件设定目标设备，则它不能由第二个固件更新包仅面向设备为目标。

 

1.  若要允许的固件更新包，以面向的 ESRT，此类设备实例在其中公开硬件 ID，用于标识为属于 ESRT 条目中每个条目的设备实例的固件更新到相应的系统硬件，Windows 图面。

2.  安装固件更新包时，它是由 Windows 处理为驱动程序包。 Windows 会将每个更新包的固件有效负载复制到系统目录下的安全位置，准备系统以执行固件更新，并触发重新启动系统。

    Windows 不支持驱动程序包之间的依赖关系。 因此，创建新的固件更新包时，必须遵守以下要求：

    -   必须能够成功安装在其自身，且不依赖于其他设备的固件、 系统固件或其他固件更新包的固件更新包。
    
    -   建议每个更新包针对单个设备在系统上或 UEFI 系统固件 （ESRT 中定义）。
    
    -   每个更新包必须包含单个固件更新二进制文件 (例如 firmware.bin)。

3.  每个更新包中的固件更新有效负载需要包含在单个二进制文件中。 在系统重新启动时，操作系统加载程序将每个固件更新包每个固件更新二进制文件加载到物理内存，并生成指向每个安装预配的有效负载文件的指针的数组 (配有 UEFI 2.3.1 规范指的是为此数组CapsuleHeaderArray)。

4.  此数组传递到 EFI UpdateCapsule() 函数调用中。 UpdateCapsule() 用作邮箱，将每个驱动程序程序包的固件更新负载传递给平台固件。

5.  指定由固件资源 ESRT 条目的固件 ID 由标识每个 capsule （固件更新负载）。

6.  收到的每个固件更新有效负载，固件更新请求处理和应用时适用。

    CapsuleHeaderArray 中的每个条目是在系统中包含单个设备的固件驱动程序包中的固件更新有效负载数据的单一、 连续的块。 对于每个目标的固件资源，固件更新有效负载必须包含固件映像和所需的用于验证的平台的所有信息。

    通过 UEFI UpdateCapsule 服务情况下，所有固件更新驱动程序包的固件有效负载传递给平台固件。 由于集成的设备将源自各种不同 Ihv，系统 OEM （和可能是 SoC 制造商） 需要直接处理这些 Ihv 以确保给定系统的适当地创作设备固件更新。 此外，系统 OEM 必须确保 ESRT 条目允许 UpdateCapsule 包定向到相应的系统。

    例如，多个 Oem 可能会选择其系统的相同模型移动宽带 (MBB) 设备。 即使 MBB 设备是在每个系统完全相同，每个 OEM 必须与 MBB IHV 创作为他们的系统自定义的固件更新包进行协作。 此级别的自定义设备固件更新的是跨多个 OEM 系统所需地址变量。

    -   解决设备可能会因选择的 OEM 和如何将设备连接到 SoC.SoC
    
    -   系统 OEM 可能多个移动网络运营商 (Mno) 的转售给使用者向销售系统。 MBB 设备必须 m n O 知道，需要同时自定义和经过认证的特定 m n O 的要求的固件。
    
    -   该系统可能会在多个全球市场，每个都有不同的 RF 规章要求和射频分配销售。 MBB 设备固件可能需要自定义以满足这些市场需求。

    每个 OEM 必须仔细考虑此类特定于设备的要求，并采取必要的步骤以确保可以作为目标并相应地更新设备固件。 这需要仔细管理 ESRT 条目，确保设备固件才能正确部署。

7.  创作的更新包后，需要对其提交给 Microsoft 进行认证和签名。

## <a name="related-topics"></a>相关主题
[通过固件驱动程序包的系统和设备固件更新](system-and-device-firmware-updates-via-a-firmware-driver-package.md)  
[填充 ESRT 表](populating-the-esrt-table.md)  
[自定义不同的地理区域的固件](customizing-firmware-for-different-geographic-regions.md)  
[认证和签名的更新包](certifying-and-signing-the-update-package.md)  
[安装更新](installing-the-update.md)  



