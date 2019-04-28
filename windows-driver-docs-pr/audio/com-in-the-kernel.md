---
title: 内核中的 COM
description: 内核中的 COM
ms.assetid: 2ce13ef1-9868-4f6d-9c42-b71f9e3d5615
keywords:
- 音频的微型端口驱动程序 WDK COM
- 微型端口驱动程序 WDK 音频 COM
- COM 接口 WDK 音频
- IUnknown 接口
- 端口类驱动程序 WDK 音频
- PortCls WDK 音频 COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf62cac5151f7c102eb29a7f0252bdfe2c772100
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333878"
---
# <a name="com-in-the-kernel"></a>内核中的 COM


## <span id="com_in_the_kernel"></span><span id="COM_IN_THE_KERNEL"></span>


音频的端口和微型端口驱动程序将符合的设备驱动程序接口 (DDIs) 导出到组件对象模型 (COM)。 有关 COM 接口的背景信息，请参阅 Microsoft Windows SDK 文档的 COM 部分。

所有 COM 接口都继承自**IUnknown**接口，它将具有方法**AddRef**， **QueryInterface**，以及**版本**。 由于这些方法是公用的所有 COM 接口，WDM 音频驱动程序接口的参考页不显式描述它们。

本部分讨论以下主题：

[函数表的微型端口驱动程序](function-tables-for-miniport-drivers.md)

[创建音频驱动程序对象](creating-audio-driver-objects.md)

[COM 对象的引用计数约定](reference-counting-conventions-for-com-objects.md)

 

 




