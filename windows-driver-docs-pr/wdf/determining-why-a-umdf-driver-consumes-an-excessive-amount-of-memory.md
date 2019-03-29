---
title: 为什么 UMDF 驱动程序会占用过多的内存
description: 介绍如何使用 Wudfext.dll 来确定为何 UMDF 版本 1 驱动程序消耗过多的内存。
ms.assetid: 01316c4e-24e8-467c-af52-900b3fe042db
keywords:
- 调试方案 WDK UMDF，UMDF 驱动程序会占用过多的内存
- UMDF WDK，调试方案，UMDF 驱动程序会占用过多的内存
- UMDF WDK UMDF 驱动程序会占用过多的内存
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b3bf4f5cf10096e5ab756084414a0e5c98eac80
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568142"
---
# <a name="determining-why-a-umdf-driver-consumes-an-excessive-amount-of-memory"></a>确定 UMDF 驱动程序使用过多内存的原因

[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

本主题介绍如何结合使用用户模式驱动程序框架 (UMDF) 版本 1 驱动程序中使用 Wudfext.dll 调试器扩展来确定为何 UMDF 驱动程序消耗过多的内存。

从 UMDF 版本 2 开始，应改为使用 Wdfkd.dll 调试器扩展。 有关详细信息，请参阅[Windows 驱动程序框架扩展 (Wdfkd.dll)](https://msdn.microsoft.com/library/windows/hardware/ff551876)。

若要调查内存使用情况，请使用以下步骤：

1.  通过在对象树中查看未完成的对象 **！ wudfext.wudfobject** UMDF 调试器扩展。

    **！ Wudfext.wudfobject**扩展显示有关 WDF 对象，其中包括其父级和子级关系的信息。 如果您设置位 0 个，共*标志*参数为 1 (0x01) **！ wudfext.wudfobject**执行递归转储的对象树的根节点的您传递的对象。 若要查看完整的对象树，请使用下面的示例命令：

    **!wudfext.wudfobject &lt;IWDFDriver\*&gt; 1**

2.  确定是否您将看到与预期的更多未解决对象。

    您的驱动程序可能最终会泄漏这些对象 (泄漏 WDF 对象的详细信息，请参阅[确定是否驱动程序泄漏 Framework 对象](determining-if-a-driver-leaks-framework-objects.md))。

    这些对象可能在对象树中，最终将因此释放。 但是，要累计不必要地。 可能需要这些对象：

    -   更正到其父对象。
    -   通过使用显式删除[ **IWDFObject::DeleteWdfObject** ](https://msdn.microsoft.com/library/windows/hardware/ff560210)方法。

 

 





