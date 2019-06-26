---
title: 映射不需更改的 WIA 属性 - 特殊案例
description: 映射不需更改的 WIA 属性 - 特殊案例
ms.assetid: 4ed02c01-efe8-4728-a54a-26fe27aa403c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9261968858e110a09f1ef491b68458cb349e9ff7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376587"
---
# <a name="mapping-wia-properties-that-need-no-changes---special-cases"></a>映射不需更改的 WIA 属性 - 特殊案例


其中的兼容性层可能会失败的情形是：

-   与所需的 Windows Vista 属性相关的丢失/损坏 Windows XP 属性可能会使兼容性层不可用。 在这些情况下，当前会话将失败;由于项目结构和属性中 （应用程序的 COM 代理将不能在这种情况下） 的 Windows XP 和 Windows Vista 驱动程序和应用程序之间的差异继续的选项不可用。 [ **WIA\_DPS\_文档\_处理\_选择**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-document-handling-select)并[ **WIA\_DPS\_文档\_处理\_功能**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-document-handling-capabilities)属性是一种特殊情况; 如果它们不受 Windows XP 驱动程序，只有平板项将被转换为 theWindows Vista应用程序

-   某些 Windows XP 根属性依赖于特定的上下文 （平板、 送纸器或属性上下文） 可能会不提供除非设置该特定上下文，或者这些属性可能具有不同的有效和当前值为每个上下文。 WIA\_DPS\_文档\_处理\_选择将用于设置正确的送纸器/平板上下文; 它会设置为送纸器 （以及双工在必要时） 或 Windows XP 驱动程序的根项平板。 在所有其他情况下，应将上下文设置但相应的属性。 Windows XP 设备支持送纸器以及平板、 和根的所有属性无法都转换为 Windows Vista 中的平板和送纸器项时，这也是如此。

-   对于从/向 Windows XP 的唯一属性翻译的 Windows Vista 属性重复，WIA 服务必须确定如何处理这种情况，其中相同的属性设置为不同的值从不同的 Windows Vista 项目。 解决方法是每次更改的上下文重新初始化所有 Windows XP 的 AIT 项属性。 这种方式可从 Windows XP 应用程序的 Windows Vista 驱动程序的送纸器以及平板项协商单独的属性集。

-   如果 Windows Vista 驱动程序不会实现送纸器或平板项 （例如，驱动程序可能会实现只是电影胶片/TPA(transparency adapter) 和/或存储的项），兼容性层将不可用。 它是不安全假设，泛型的 Windows XP 子项目始终可以创建 Windows Vista 电影/TPA 和/或存储项。 此外，Windows Vista 驱动程序实现的电影胶片/TPA 和存储项可能会发生更多复杂。 因此，兼容性层不适用于 Windows Vista 驱动程序未实现至少一个平板或送纸器项。

-   如果 Windows XP 驱动程序未实现正确的 Windows XP 项结构 （根加上子扫描项），示例中，如果驱动程序部分实现了对新的 Windows Vista 项结构支持，但无法提供完整支持 Windows Vista 映像将禁用传输，属性/项兼容性层，当前会话将失败。

 

 




