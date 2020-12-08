---
title: 示例 IDE 控制器微型驱动程序
description: 示例 IDE 控制器微型驱动程序
keywords:
- IDE 控制器微型驱动程序 WDK 存储，示例
- 存储 IDE 控制器微型驱动程序 WDK，示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0f27a5d97ad24f04f2787ce6f4447553e24d5f0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802183"
---
# <a name="sample-ide-controller-minidrivers"></a>示例 IDE 控制器微型驱动程序


## <span id="ddk_sample_ide_controller_minidrivers_kg"></span><span id="DDK_SAMPLE_IDE_CONTROLLER_MINIDRIVERS_KG"></span>


本部分介绍 Microsoft Windows 驱动程序工具包附带的示例 IDE 控制器微型驱动程序 (WDK) 。

WDK 包括 *pciide.sys* 通用控制器微型驱动程序的源代码。 请参阅 \\ WDK 的 src 存储目录中的示例代码 \\ 。

此示例的兼容性为64位。 它是用 Microsoft Visual C 6.0 生成的，不实现即插即用或电源管理。

*pciide.sys* 示例在 windows 95/98/me 和基于 nt 的操作系统版本之间是二进制兼容的，但前提是没有 windows 95/98/me VxD 调用，也不会在微型驱动程序中嵌入任何基于 nt 的系统调用。

 

 




