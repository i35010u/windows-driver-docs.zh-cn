---
title: IKeywordDetectorOemAdapter 接口
description: IKeywordDetectorOemAdapter 是用于与语音激活驱动程序接口进行交互的组件对象模型 (COM) 接口。 在 Windows 10 和更高版本的 Windows 支持 IKeywordDetectorOemAdapter 接口。
ms.assetid: FB243792-C0B0-4BCA-B4C4-B6E17FDB615C
keywords:
- IKeywordDetectorOemAdapter 接口音频设备
- 描述 IKeywordDetectorOemAdapter 接口音频设备
topic_type:
- apiref
api_name:
- IKeywordDetectorOemAdapter
api_type:
- COM
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: aabd2d129a43d7add6b7e19d8097f68da2b8d915
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359952"
---
# <a name="ikeyworddetectoroemadapter-interface"></a>IKeywordDetectorOemAdapter 接口


**IKeywordDetectorOemAdapter**是用于与语音激活驱动程序接口进行交互的组件对象模型 (COM) 接口。 **IKeywordDetectorOemAdapter**接口支持 Windows 10 和更高版本的 Windows 中。

OEM 提供充当中介的操作系统和驱动程序，帮助计算或分析是读取和写入到通过音频驱动程序的不透明数据的 COM 对象实现[ **KSPROPERTY\_SOUNDDETECTOR\_模式**](ksproperty-sounddetector-patterns.md)并[ **KSPROPERTY\_SOUNDDETECTOR\_MATCHRESULT**](ksproperty-sounddetector-matchresult.md)。

COM 对象的类标识符 (CLSID) 是检测程序模式类型返回的 GUID [ **KSPROPERTY\_SOUNDDETECTOR\_SUPPORTEDPATTERNS**](ksproperty-sounddetector-supportedpatterns.md)。 操作系统调用[ **CoCreateInstance** ](https://docs.microsoft.com/windows/desktop/api/combaseapi/nf-combaseapi-cocreateinstance)传递要实例化与关键字模式类型兼容，并在对象上调用方法的相应 COM 对象的模式类型 GUID**IKeywordDetectorOemAdapter**接口。 操作系统提供的代理存根**IKeywordDetectorOemAdapter**。 OEM 的实现可能会选择任何 COM 线程模型。

接口设计会试图保持无状态的对象实现。 换而言之，实现应要求存储方法调用之间没有状态。 事实上，内部C++类可能不需要除一般情况下实现 COM 对象所需之外的所有成员变量。

<a name="members"></a>成员
-------

**IKeywordDetectorOemAdapter**接口继承自[ **IUnknown** ](https://docs.microsoft.com/windows/desktop/api/unknwn/nn-unknwn-iunknown)接口，但不包含其他成员。

 

 





