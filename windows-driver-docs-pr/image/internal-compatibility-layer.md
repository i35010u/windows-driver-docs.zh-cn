---
title: 内部的兼容性层
description: 内部的兼容性层
ms.assetid: 6cfb3842-751e-4f4c-9fac-daba70245b81
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d6d97c48d5501223d35caddc281b5cc740fafd2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520456"
---
# <a name="internal-compatibility-layer"></a>内部的兼容性层


开发驱动程序在 Windows Vista 上运行时，您必须考虑兼容性的两个的方面：

-   适用于 Windows XP 或更早的操作系统的应用程序与 Windows Vista 驱动程序的通信时

-   Windows Vista 应用程序与 Windows XP 驱动程序的通信时 (即*旧式驱动程序*)

不需要考虑其他情况下，如 Windows Vista 应用程序与 Windows Vista 驱动程序的通信时或当 Windows XP 应用程序与 Windows XP 驱动程序，因为这种情况下不需要任何兼容性组件。

WIA 提供了一个内部的兼容性层，用于执行所有必要的转换。 因此，在 Windows Vista 运行的 Windows XP 应用程序将能够与 Windows Vista 驱动程序进行通信和 Windows Vista 应用程序将能够与在 Windows Vista 运行的 Windows XP 驱动程序进行通信。

有几个限制的兼容性层：

-   旧驱动程序将转换为 Windows Vista WIA 应用程序。

-   仅 Windows Vista 扫描仪的驱动程序实现平板和送纸器作为其基项 (WIA\_类别\_平板和 WIA\_类别\_送纸器) 将转换为旧版 WIA 应用程序。

 

 




