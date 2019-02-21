---
title: WMI 数据和事件块的 MOF 语法
description: WMI 数据和事件块的 MOF 语法
ms.assetid: 247037b7-d62e-4f74-8fa4-57e74f6c412f
keywords:
- WMI WDK 内核，事件块
- 事件阻止 WDK WMI
- 数据将阻止 WDK WMI
- WMI WDK 内核，数据块
- 块 WDK WMI
- MOF 文件 WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9afa4b343242215a3d724f37e4bcec3e6221413
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533627"
---
# <a name="mof-syntax-for-wmi-data-and-event-blocks"></a>WMI 数据和事件块的 MOF 语法





驱动程序的 WMI 架构描述其数据块，用于定义可以提供一个驱动程序并能够响应 WMI 请求以执行方法的信息。 驱动程序的架构还介绍了其事件块，它们是驱动程序确定事件发生 WMI 客户端用户已为其请求通知时，该驱动程序将发送到 WMI 的数据块。

驱动程序编写器定义驱动程序的架构中托管对象格式 (MOF)。 MOF 是经过编译的语言创建的桌面管理任务组 (DMTF) 和基于接口定义语言 (IDL)。 驱动程序的 MOF 文件包含每个数据块和驱动程序向 WMI 公开的事件块的 MOF 类定义。

WMI 数据块的 MOF 类定义使用以下语法：

**\[**<em>必需和可选类限定符</em>**\]**

**类 * * * ClassName* :*OptionalBaseClass*
 **{**
**\[密钥，请阅读\]**
**字符串 InstanceName;**
 **\[读取\]**
**布尔处于活动状态;**
 ** \[ ** *必需和可选属性限定符* ** \] ** 
 <em>数据类型 itemname1</em>* *;**
 ** \[ ** *必需和可选属性限定符* ** \] ** 
 <em>数据类型 itemnameN</em>**;**
 **};** 下面的主题介绍上面所示的语法元素：

[WMI 类限定符](wmi-class-qualifiers.md)

[WMI 类名和基类](wmi-class-names-and-base-classes.md)

[WMI 类中的必需的项](required-items-in-wmi-classes.md)

[WMI 属性限定符](wmi-property-qualifiers.md)

[驱动程序定义的 WMI 数据项目](driver-defined-wmi-data-items.md)

[WMI 类示例](wmi-class-examples.md)

有关 MOF 语法的一般讨论，因为这关系到 WMI 客户端和其他类型的应用程序，请参阅 Microsoft Windows SDK。

 

 




