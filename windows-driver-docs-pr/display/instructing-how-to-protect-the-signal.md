---
title: 指示如何保护信号
description: 指示如何保护信号
ms.assetid: d55a3660-5b7c-43e9-b1c5-b61f8b997a1a
keywords:
- 复制保护 WDK COPP，信号保护
- 视频复制保护 WDK COPP，信号保护
- COPP WDK DirectX va，因此信号保护
- 受保护视频 WDK COPP，信号保护
- 信号保护 WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59af9881f94de79b0a890342d1ba5ecad180ee59
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561509"
---
# <a name="instructing-how-to-protect-the-signal"></a>指示如何保护信号


**本部分仅适用于 Windows Server 2003 SP1 和更高版本，和 Windows XP SP2 及更高版本。**

COPP 命令可以提供有关如何保护信号，它们将通过与 DirectX VA COPP 设备相关联的物理连接器的说明。 若要设置信号保护，微型端口驱动程序[ *COPPCommand* ](https://msdn.microsoft.com/library/windows/hardware/ff539642)函数接收指向[ **DXVA\_COPPCommand** ](https://msdn.microsoft.com/library/windows/hardware/ff563141)结构**guidCommandID**成员设置为 DXVA\_COPPSetSignaling GUID 并**CommandData**成员设置为一个指向[ **DXVA\_COPPSetSignalingCmdData** ](https://msdn.microsoft.com/library/windows/hardware/ff563146)结构，它指定如何保护信号。

 

 





