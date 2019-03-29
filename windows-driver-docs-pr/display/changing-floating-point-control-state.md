---
title: 更改浮点控制状态
description: 更改浮点控制状态
ms.assetid: de1ace72-ee3c-4adc-8e40-0d687b18cc25
keywords:
- 浮点控制状态 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a1bec9472ee39917bc88f92a1ab8f9d90603a28
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567143"
---
# <a name="changing-floating-point-control-state"></a>更改浮点控制状态


显示微型端口驱动程序和用户模式显示驱动程序的所有函数必须保存浮点控制状态，例如，然后再更改浮点控制状态的舍入模式或精度，并且必须恢复到浮点控制状态以前保存在返回之前的设置。

 

 





