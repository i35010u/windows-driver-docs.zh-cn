---
title: 内核中的 COM
description: 内核中的 COM
keywords:
- 音频微型端口驱动程序 WDK，COM
- 微型端口驱动程序 WDK 音频，COM
- COM 接口 WDK 音频
- IUnknown 接口
- 端口类驱动程序 WDK 音频
- PortCls WDK 音频，COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca5f3693ac5f25ee5c9553a1b63233be31361dec
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784921"
---
# <a name="com-in-the-kernel"></a>内核中的 COM


## <span id="com_in_the_kernel"></span><span id="COM_IN_THE_KERNEL"></span>


音频端口和微型端口驱动程序将 (DDIs) 的导出设备驱动程序接口，这些接口符合组件对象模型 (COM) 。 有关 COM 接口的背景信息，请参阅 Microsoft Windows SDK 文档的 COM 部分。

所有 COM 接口都继承自 **IUnknown** 接口，该接口具有 **AddRef**、 **QueryInterface** 和 **Release** 方法。 由于这些方法对于所有 COM 接口都是通用的，所以 WDM 音频驱动程序接口的引用页不会显式描述它们。

本部分介绍以下主题：

[适用于微型端口驱动程序的函数表](function-tables-for-miniport-drivers.md)

[创建音频驱动程序对象](creating-audio-driver-objects.md)

[COM 对象的引用计数约定](reference-counting-conventions-for-com-objects.md)

 

 




