---
title: 'DoubleFetch 规则 (wdm) '
description: 了解 (wdm) 的 DoubleFetch 规则。
ms.assetid: 2DCDB0E1-AE62-4951-8029-E9557BCC0DDB
ms.date: 10/21/2020
keywords:
- 'DoubleFetch 规则 (wdm) '
topic_type:
- apiref
api_name:
- doublefetch
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8719bc18790196f9e1dea455d4ed84ff5c948de9
ms.sourcegitcommit: 1690ad77580a2cfc47debb9751fd109a5991dd52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92346138"
---
# <a name="doublefetch-rule-wdm"></a>DoubleFetch 规则 (wdm) 

**DoubleFetch**规则是一项重要的安全规则，它检查驱动程序是否安全访问通过 irp 传递到用户空间的缓冲区。  若要在驱动程序和用户模式组件之间安全发送数据，请参阅 [使用未缓冲和直接 i/o](../kernel/using-neither-buffered-nor-direct-i-o.md)中所述的适当方法。

驱动程序应遵循 [访问数据缓冲区的方法](../kernel/methods-for-accessing-data-buffers.md)中所述的指导原则和最佳做法，来访问数据缓冲区。

此规则检查是否从用户模式内存指针进行双重提取。 用户模式内存的双内核模式访问可能导致争用条件安全问题。  访问用户模式数据时，内核模式代码需要在本地创建用户模式数据的副本，并避免多次访问用户模式数据。  否则，会导致一种称为 "双重提取" 的问题，在首次访问数据后，数据可能会发生更改。

此规则从 Windows 10 WDK 开始提供，版本20236。 此规则仅适用于 *WDM* 和 *通用* 驱动程序类型。

**驱动程序模型： WDM、泛型**

## <a name="how-to-test"></a>如何测试

在编译时：

1. 运行 [静态驱动程序验证程序](./static-driver-verifier.md) 并指定 **doublefetch** 规则。
2. 使用以下步骤 (在 [使用静态驱动程序验证器查找 Windows 驱动程序中的缺陷](./using-static-driver-verifier-to-find-defects-in-drivers.md)) 运行代码分析：

    - [准备你的代码 (使用) 的角色类型声明。](./using-static-driver-verifier-to-find-defects-in-drivers.md#preparing-your-source-code)
    - [运行静态驱动程序验证程序。](./using-static-driver-verifier-to-find-defects-in-drivers.md#running-static-driver-verifier)
    - [查看并分析结果。](./using-static-driver-verifier-to-find-defects-in-drivers.md#viewing-and-analyzing-the-results)

有关详细信息，请参阅 [使用静态驱动程序验证器查找驱动程序中的缺陷](./using-static-driver-verifier-to-find-defects-in-drivers.md)。