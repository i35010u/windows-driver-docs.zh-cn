---
title: 映射不需更改的 WIA 属性 - 特殊案例
description: 映射不需更改的 WIA 属性 - 特殊案例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd701da078f7b8717aecd145c2c6ced06593a7c2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803863"
---
# <a name="mapping-wia-properties-that-need-no-changes---special-cases"></a>映射不需更改的 WIA 属性 - 特殊案例


兼容层可能会失败的情况如下：

-   与所需的 Windows Vista 属性相关的 Windows XP 属性丢失/损坏可能会导致兼容层不可用。 在这些情况下，当前会话将失败;由于 Windows XP 和 Windows Vista 驱动程序与 (应用程序之间的项结构和属性之间存在差异，因此无法继续使用该选项) 。 [**WIA \_ dps \_ 文档 \_ 处理 \_ 选择**](./wia-dps-document-handling-select.md)和 [**WIA \_ dps \_ 文档 \_ 处理 \_ 功能**](./wia-dps-document-handling-capabilities.md)是一种特殊情况; 如果 Windows XP 驱动程序不支持这些属性，则只会为 windows Vista 应用程序翻译平板项目

-   某些依赖于特定上下文 (平板、进纸器或属性上下文) 的 Windows XP 根属性可能不可用，除非已设置该特定上下文，或者这些属性对于每个上下文可能具有不同的有效值和当前值。 WIA \_ DPS \_ 文档 \_ 处理 \_ 选择将用于设置正确的进纸器/平板上下文; 当需要在 Windows XP 驱动程序的根项上) 或平板时，它将设置为送纸器 (和双工。 在所有其他情况下，应通过适当的属性来设置上下文。 如果 Windows XP 设备同时支持送纸器和平板，并且所有根属性都可以转换为 Windows Vista 中的平板和进纸器项，也会出现这种情况。

-   对于翻译自/到唯一 Windows XP 属性的重复 Windows Vista 属性，WIA 服务必须确定如何将同一属性设置为不同 Windows Vista 项中不同值的情况。 解决方案是在每次更改上下文时重新初始化所有 Windows XP A AIT 项属性。 这样一来，就可以从 Windows XP 应用程序中为 Windows Vista 驱动程序的送纸器和平板项协商不同的属性集。

-   如果 Windows Vista 驱动程序未实现进纸器或平板项目 (例如，驱动程序可能只实现胶片/TPA (透明适配器) 和/或存储项目) ，兼容层将不可用。 假设始终可以为 Windows Vista 胶卷/TPA 和/或存储项目创建通用 Windows XP 子项，这是不安全的。 此外，如果 Windows Vista 驱动程序同时实现了胶卷/TPA 和存储项，则可能会出现更复杂的情况。 因此，兼容层不适用于未实现平板或进纸器项的 Windows Vista 驱动程序。

-   如果 Windows XP 驱动程序未实现正确的 Windows XP 项结构 (根加子扫描项) ，例如，如果驱动程序部分实现了对新的 Windows Vista 项结构的支持，但未能提供对 Windows Vista 映像传输的完整支持，则将禁用属性/项兼容性层，当前会话将失败。

 

