---
title: UMDF 驱动程序为什么会消耗过多内存
description: 介绍如何使用 Wudfext.dll 来确定 UMDF 版本1驱动程序为什么会消耗大量内存。
keywords:
- 调试方案 WDK UMDF，UMDF 驱动程序占用过多内存
- UMDF WDK，调试方案，UMDF 驱动程序占用过多内存
- UMDF WDK，UMDF 驱动程序占用过多内存
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9aa55ba1797d7274d540991b24c744676df09c6a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828971"
---
# <a name="determining-why-a-umdf-driver-consumes-an-excessive-amount-of-memory"></a>确定 UMDF 驱动程序使用过多内存的原因

[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

本主题介绍如何将 Wudfext.dll 调试程序扩展与 User-Mode Driver Framework (UMDF) 版本1驱动程序结合使用，以确定 UMDF 驱动程序消耗大量内存的原因。

从 UMDF 版本2开始，你应该改用 Wdfkd.dll 调试程序扩展。 有关详细信息，请参阅 [Windows Driver Framework extension ( # A0) ](../debugger/kernel-mode-driver-framework-extensions--wdfkd-dll-.md)。

若要调查内存使用情况，请使用以下步骤：

1.  使用 **！ wudfext wudfobject** UMDF 调试器扩展在对象树中查看未完成的对象。

    **！ Wudfext wudfobject** 扩展显示有关 WDF 对象的信息，其中包括其父关系和子关系。 如果将 *Flags* 参数的位0设置为 1 (0x01) ， **！ wudfext。 wudfobject** 执行对象树的递归转储，该对象树以你传递的对象为根。 若要查看完整的对象树，请使用下面的示例命令：

    **！ wudfext. wudfobject &lt; IWDFDriver \* &gt; 1**

2.  确定所显示的对象是否比预期更多。

    你的驱动程序可能最终会泄漏这些对象 (有关泄漏 WDF 对象的详细信息，请参阅 [确定驱动程序是否泄漏框架对象](determining-if-a-driver-leaks-framework-objects.md)) 。

    这些对象可能在对象树中，因此最终会被释放。 但是，它们不需要进行累积。 这些对象可能需要：

    -   更正其父对象。
    -   使用 [**IWDFObject：:D eletewdfobject**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfobject-deletewdfobject) 方法的显式删除。

 

