---
title: 示例 IDE 控制器微型驱动程序
description: 示例 IDE 控制器微型驱动程序
ms.assetid: 3c8779ae-30d7-4ab8-b6d8-a711f917564c
keywords:
- IDE 控制器微型驱动程序 WDK 存储示例
- 存储 IDE 控制器微型驱动程序 WDK，示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0133cceaa9056fa98cf0840d7e221bebbd98f715
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524256"
---
# <a name="sample-ide-controller-minidrivers"></a>示例 IDE 控制器微型驱动程序


## <span id="ddk_sample_ide_controller_minidrivers_kg"></span><span id="DDK_SAMPLE_IDE_CONTROLLER_MINIDRIVERS_KG"></span>


本部分介绍示例 IDE 控制器微型驱动程序包含与 Microsoft Windows Driver Kit (WDK)。

WDK 包含的源代码*pciide.sys*泛型控制器微型驱动程序。 请参阅中的示例代码\\src\\WDK 的存储目录。

此示例是 64 位兼容。 它能够构建使用 Microsoft Visual C 6.0 和不实现插或电源管理。

*Pciide.sys*示例是 Windows 95/98/我和基于 NT 的操作系统，不提供任何 Windows 95/98/我 VxD 调用版本之间的二进制兼容，也不在微型驱动程序中嵌入任何基于 NT 的系统调用。

 

 




