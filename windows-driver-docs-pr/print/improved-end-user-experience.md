---
title: 改进了最终用户体验
description: 改进了最终用户体验
ms.assetid: d87062f2-2832-4443-b9f0-97e34f79c47f
keywords:
- 打印票证 WDK，XPSDrv
- XPSDrv 的打印机驱动程序 WDK，最终用户的改进
- 打印功能 WDK，XPSDrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b40d9aceb4d44ba1587f7a4d6f4eaefb69067aa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541394"
---
# <a name="improved-end-user-experience"></a>改进了最终用户体验


Windows Vista 引入了两个新技术以提高通信的设备功能和用户的意图：

-   **打印票证**。 基于 XML 的打印票证技术，以改善最终用户体验的应用程序和设备之间打印目的的更好的沟通。 此技术使打印的组件可以是更透明的更彻底地处理设置的迁移。 在新的应用程序框架，基于 Windows Vista 中的托管的代码对象，打印票证是描述打印作业设置的标准方式。

    通过使用明确定义的基于 XML 的格式，打印票证技术使所有组件和客户端打印子系统的启用透明访问当前存储在 DEVMODE 结构的公用和专用部分中的信息。 打印票证设计用于解决问题的降级或驱动程序升级后发生。 可以避免出现问题而导致的驱动程序版本不匹配方案与旨在使用的打印票证技术的打印驱动程序。 通过使用 PrintTicket 通信设置，可以避免在迁移工作的负客户体验。

-   **打印功能**。 基于 XML 的打印功能技术提供了一种方法来发布可配置设备功能，如分页装订选项和页面布局选项。 打印机可以使用 PrintCapabilities 来描述显式所有用户可配置属性的设备并为每个属性的允许设置。 打印架构 framework 使用可以精确描述并有效地比较设备的属性。 通过使用打印架构关键字文档和打印架构 framework 中定义的结构中的关键字，应用程序可以更有效地使用设备功能。

 

 




