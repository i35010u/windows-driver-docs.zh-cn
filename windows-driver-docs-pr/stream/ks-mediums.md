---
title: KS 媒体
description: KS 媒体
ms.assetid: c94c738c-66c6-491b-9157-28cccf95af4d
keywords:
- 流式处理媒体 WDK 内核
- KSPIN_MEDIUM
- WDK、 媒体流式处理的内核
- KS WDK 介质
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2fd901b614f4809751baf801972721b370d6d50d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569494"
---
# <a name="ks-mediums"></a>KS 媒体





一个*中等*定义一种类型的通信总线。 微型驱动程序指示 pin 支持通过提供指向的数组的指针的媒介[ **KSPIN\_MEDIUM** ](https://msdn.microsoft.com/library/windows/hardware/ff563538)中的相关结构[ **KSPIN\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff563533)结构。 KSPIN\_中等标识通信总线上的特定连接。

客户端指定要通过设置用于连接的介质**中等**中的成员[ **KSPIN\_CONNECT** ](https://msdn.microsoft.com/library/windows/hardware/ff563531)它们对的调用中提供的结构[**KsCreatePin**](https://msdn.microsoft.com/library/windows/hardware/ff561652)。

客户端请求一系列媒体通过使用支持的筛选器或 pin [ **KSPROPERTY\_PIN\_媒介**](https://msdn.microsoft.com/library/windows/hardware/ff565202)属性。

 

 




