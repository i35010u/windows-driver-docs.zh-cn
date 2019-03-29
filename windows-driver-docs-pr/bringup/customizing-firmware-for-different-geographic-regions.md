---
title: 自定义不同地理区域的固件
description: 系统将销售各种市场和地理位置全球范围内。 若要启用此功能，Oem 必须定义这些设备/系统固件，这可能需要特定于区域的固件的唯一 GUID 值。
ms.assetid: 47E1C9EC-ED6E-4626-B61F-A19D1546FA08
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9cc960e400fa4ecc40af77cc28ecd8e34b41ba53
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562866"
---
# <a name="customizing-firmware-for-different-geographic-regions"></a>自定义不同地理区域的固件


系统将销售各种市场和地理位置全球范围内。 若要启用此功能，Oem 必须定义这些设备/系统固件，这可能需要特定于区域的固件的唯一 GUID 值。

例如，特定于区域的固件是通常需要对移动宽带 (MBB) 设备。 MBB 设备固件通常是自定义的特定移动网络运算符 (MNO) 在特定区域中，以符合本地 m n O 和政府法规。 若要允许此类设备的固件的目标，OEM 必须分配一个唯一的 GUID ESRT 中该设备在制造时。

![发往不同的地理区域设置的两个硬件相同 soc 系统](images/socsfordifferentlocales.png)

在上图中，请注意，系统并在所有方面，系统为目标的转售在不同的地理区域中的异常使用完全相同。 因此，每个系统中的 MBB 设备固件必须是独立定目标，并分配 ESRT 中不同的 GUID。 这样将固件更新发布到在其操作的区域中销售它们的系统 m n O。 按地理位置或零售渠道，类似还必须考虑到这可能需要自定义固件的任何设备。

## <a name="related-topics"></a>相关主题
[通过固件驱动程序包的系统和设备固件更新](system-and-device-firmware-updates-via-a-firmware-driver-package.md)  
[填充 ESRT 表](populating-the-esrt-table.md)  
[创作固件更新包](authoring-a-firmware-update-package.md)  
[认证和签名的更新包](certifying-and-signing-the-update-package.md)  
[安装更新](installing-the-update.md)  



