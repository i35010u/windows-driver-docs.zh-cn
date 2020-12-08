---
title: 内部兼容性层
description: 内部兼容性层
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22f8e1bdc91075a7068de2a36c5639b6556b3435
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828701"
---
# <a name="internal-compatibility-layer"></a>内部兼容性层


开发要在 Windows Vista 上运行的驱动程序时，必须考虑兼容性的两个方面：

-   适用于 Windows XP 或更早版本的操作系统的应用程序与 Windows Vista 驱动程序通信时

-   如果 Windows Vista 应用程序与 Windows XP 驱动程序通信 (即 *旧驱动* 程序) 

您无需考虑其他情况，例如，当 Windows Vista 应用程序与 Windows Vista 驱动程序通信时，或 Windows XP 应用程序与 Windows XP 驱动程序通信时，因为这些情况不需要任何兼容组件。

WIA 提供了执行所有必需转换的内部兼容层。 因此，在 Windows Vista 上运行的 Windows XP 应用程序将能够与 Windows Vista 驱动程序通信，Windows Vista 应用程序将能够与 windows Vista 上运行的 Windows XP 驱动程序通信。

兼容性层有几个限制：

-   对于 Windows Vista WIA 应用程序，只翻译旧驱动程序。

-   对于旧的 WIA 应用程序，仅将实现平板和送纸器的 Windows Vista 扫描仪驱动程序作为其基础项 (WIA \_ 类别 \_ 平板和 wia \_ 类别 \_ 进纸器) 。

 

 




