---
title: COPP 简介
description: COPP 简介
ms.assetid: a5f77c60-418d-4931-8922-ca2ae080da2e
keywords:
- 复制保护 WDK COPP，有关 COPP
- 视频复制保护 WDK COPP，有关 COPP
- COPP WDK DirectX VA，有关 COPP
- 有关 COPP 的受保护视频 WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9200ff0ee6287779cc6b53daa634cb4e09338095
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522305"
---
# <a name="introduction-to-copp"></a>COPP 简介


## <span id="ddk_introduction_to_the_certified_output_protection_protocol_gg"></span><span id="DDK_INTRODUCTION_TO_THE_CERTIFIED_OUTPUT_PROTECTION_PROTOCOL_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 和更高版本和 Windows XP SP2 和更高版本。**

COPP 提供视频的图形适配器由输出应用复制保护的一种机制。 COPP 将各种链接保护要求发送到图形适配器以更好的保护方式相比，通过提供一种常见协议[ **IOCTL\_视频\_处理\_VIDEOPARAMETERS** ](https://msdn.microsoft.com/library/windows/hardware/ff567805) I/O 控制 (IOCTL) 代码。

下面的主题介绍 COPP:

[由 COPP 加密基元](cryptographic-primitives-used-by-copp.md)

[通过安全通道进行通信](communicating-through-a-secure-channel.md)

[支持 COPP 的图形适配器输出要求](graphics-adapter-output-requirements-to-support-copp.md)

 

 





