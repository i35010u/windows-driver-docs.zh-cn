---
title: UMDF 驱动程序为什么会消耗过多内存
description: 介绍如何使用 Wudfext 来确定 UMDF 版本1驱动程序消耗大量内存的原因。
ms.assetid: 01316c4e-24e8-467c-af52-900b3fe042db
keywords:
- 调试方案 WDK UMDF，UMDF 驱动程序占用过多内存
- UMDF WDK，调试方案，UMDF 驱动程序占用过多内存
- UMDF WDK，UMDF 驱动程序占用过多内存
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4e98dd23a2328cd459773600f38ce16b88cf7df
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210473"
---
# <a name="determining-why-a-umdf-driver-consumes-an-excessive-amount-of-memory"></a>确定 UMDF 驱动程序使用过多内存的原因

[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

本主题介绍如何将 Wudfext 调试程序扩展与用户模式驱动程序框架（UMDF）版本1驱动程序结合使用，以确定 UMDF 驱动程序消耗大量内存的原因。

从 UMDF 版本2开始，你应该改用 Wdfkd 调试器扩展。 有关详细信息，请参阅[Windows 驱动程序框架扩展（Wdfkd）](https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-mode-driver-framework-extensions--wdfkd-dll-)。

若要调查内存使用情况，请使用以下步骤：

1.  使用 **！ wudfext wudfobject** UMDF 调试器扩展在对象树中查看未完成的对象。

    **！ Wudfext wudfobject**扩展显示有关 WDF 对象的信息，其中包括其父关系和子关系。 如果将*Flags*参数的位0设置为1（0x01）， **！ wudfext**将对以你传递的对象为根的对象树执行递归转储。 若要查看完整的对象树，请使用下面的示例命令：

    **！ wudfext. wudfobject &lt;IWDFDriver\*&gt; 1**

2.  确定所显示的对象是否比预期更多。

    你的驱动程序可能最终会泄漏这些对象（有关泄漏 WDF 对象的详细信息，请参阅[确定驱动程序是否泄漏框架对象](determining-if-a-driver-leaks-framework-objects.md)）。

    这些对象可能在对象树中，因此最终会被释放。 但是，它们不需要进行累积。 这些对象可能需要：

    -   更正其父对象。
    -   使用[**IWDFObject：:D eletewdfobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfobject-deletewdfobject)方法的显式删除。

 

 





