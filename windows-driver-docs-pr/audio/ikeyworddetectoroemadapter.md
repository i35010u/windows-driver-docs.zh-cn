---
title: IKeywordDetectorOemAdapter 接口
description: IKeywordDetectorOemAdapter 是一个组件对象模型 (COM) 接口，用于与语音激活驱动程序接口交互。 Windows 10 和更高版本的 Windows 支持 IKeywordDetectorOemAdapter 接口。
keywords:
- IKeywordDetectorOemAdapter 接口音频设备
- IKeywordDetectorOemAdapter 接口音频设备，描述
topic_type:
- apiref
api_name:
- IKeywordDetectorOemAdapter
api_type:
- COM
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb8fdae2082b06ca1633cb70ba953daae6341ba3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790729"
---
# <a name="ikeyworddetectoroemadapter-interface"></a>IKeywordDetectorOemAdapter 接口


**IKeywordDetectorOemAdapter** 是一个组件对象模型 (COM) 接口，用于与语音激活驱动程序接口交互。 Windows 10 和更高版本的 Windows 支持 **IKeywordDetectorOemAdapter** 接口。

OEM 提供一个 COM 对象实现，它充当操作系统和驱动程序之间的中介，有助于计算或分析通过 [**KSPROPERTY \_ SOUNDDETECTOR \_ 模式**](ksproperty-sounddetector-patterns.md) 和 [**KSPROPERTY \_ SOUNDDETECTOR \_ MATCHRESULT**](ksproperty-sounddetector-matchresult.md)写入和读取到音频驱动程序的不透明数据。

COM 对象的 CLSID)  (类标识符是由 [**KSPROPERTY \_ SOUNDDETECTOR \_ SUPPORTEDPATTERNS**](ksproperty-sounddetector-supportedpatterns.md)返回的探测器模式类型 GUID。 操作系统调用 [**CoCreateInstance**](/windows/win32/api/combaseapi/nf-combaseapi-cocreateinstance) ，传递模式类型 GUID 来实例化与关键字模式类型兼容的适当 COM 对象，并调用对象的 **IKeywordDetectorOemAdapter** 接口上的方法。 此操作为 **IKeywordDetectorOemAdapter** 提供代理存根。 OEM 的实现可以选择任何 COM 线程模型。

接口设计会尝试使对象实现保持无状态。 换句话说，实现应要求在方法调用之间不存储任何状态。 事实上，内部 c + + 类可能不需要除实现 COM 对象所需的所有成员变量。

<a name="members"></a>成员
-------

**IKeywordDetectorOemAdapter** 接口继承自 [**IUnknown**](/windows/win32/api/unknwn/nn-unknwn-iunknown)接口，但没有其他成员。

 

