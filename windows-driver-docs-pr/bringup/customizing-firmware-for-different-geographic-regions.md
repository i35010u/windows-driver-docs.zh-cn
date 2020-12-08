---
title: 自定义不同地理区域的固件
description: 系统将销售在世界各地的各种市场和地区。 若要启用此项，Oem 必须为这些设备/系统固件定义唯一的 GUID 值，这些值可能需要特定于区域的固件。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f10e38d17ea63b18fdf914965e77c31a005b32aa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803421"
---
# <a name="customizing-firmware-for-different-geographic-regions"></a>自定义不同地理区域的固件


系统将销售在世界各地的各种市场和地区。 若要启用此项，Oem 必须为这些设备/系统固件定义唯一的 GUID 值，这些值可能需要特定于区域的固件。

例如，移动宽带 (MBB) 设备经常需要特定于区域的固件。 MBB 设备固件通常是针对特定地区的特定移动网络)  (运营商自定义的，以满足本地 o 和政府法规要求。 若要允许将固件定向到此类设备，OEM 必须在制造时在 ESRT 中为该设备分配一个唯一的 GUID。

![针对不同地理区域设置的两个硬件相同的 soc 系统](images/socsfordifferentlocales.png)

请注意，在上图中，系统在所有方面都是相同的，但系统会在不同的地理区域转售。 因此，每个系统中的 MBB 设备固件必须单独不再并在 ESRT 中分配一个不同的 GUID。 这使 o 可以将固件更新以其在其工作区域中销售的系统进行目标。 必须考虑到任何设备可能需要地域或经销通道提供自定义固件的类似注意事项。

## <a name="related-topics"></a>相关主题
[通过固件驱动程序包进行的系统和设备固件更新](system-and-device-firmware-updates-via-a-firmware-driver-package.md)  
[填充 ESRT 表](populating-the-esrt-table.md)  
[创作固件更新包](authoring-a-firmware-update-package.md)  
[认证和签署更新包](certifying-and-signing-the-update-package.md)  
[安装更新](installing-the-update.md)  



