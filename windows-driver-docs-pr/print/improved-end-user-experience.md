---
title: 改进的最终用户体验
description: 改进的最终用户体验
keywords:
- 打印票证 WDK，XPSDrv
- XPSDrv 打印机驱动程序 WDK，最终用户改进
- 打印功能 WDK，XPSDrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f41ad54b7edeae258f40743f01c91b04aa1966e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835723"
---
# <a name="improved-end-user-experience"></a>改进的最终用户体验


Windows Vista 引入了两种新技术来改善设备功能的通信和用户意向：

-   **打印票证**。 使用基于 XML 的打印票证技术可以更好地在应用程序和设备之间进行打印意向的通信，从而改善最终用户体验。 此技术使打印组件更透明，并更干净地处理设置迁移。 在 Windows Vista 的托管代码对象上构建的新应用程序框架中，打印票证是描述打印作业设置的标准方法。

    通过使用定义完善的 XML 格式，打印票证技术使打印子系统的所有组件和客户端都可以透明地访问当前存储在 DEVMODE 结构的公共和私有部分中的信息。 打印票证设计解决了驱动程序升级或降级后可能出现的问题。 您可以避免由于驱动程序版本不匹配方案所导致的问题，打印驱动程序设计为使用打印票证技术。 通过使用 PrintTicket 传达设置，可以避免客户对迁移工作产生负面体验。

-   **打印功能**。 基于 XML 的打印功能技术提供了一种方法，用于发布可配置的设备功能，如装帧选项和页面布局选项。 打印机可以使用 PrintCapabilities 显式描述设备的所有用户可配置属性和每个属性允许的设置。 利用 Print Schema framework，可以精确描述和高效地比较设备属性。 通过使用 "打印架构关键字" 文档中的关键字和在打印架构框架中定义的结构，应用程序可以更有效地使用设备功能。

 

 




