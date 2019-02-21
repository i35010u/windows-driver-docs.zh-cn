---
title: 获取 NDIS 版本
description: 获取 NDIS 版本
ms.assetid: f7bbd11c-b6ec-4adb-8c42-ec438d518ed8
keywords:
- 操作系统版本与的 NDIS 版本信息 WDK，
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be779b52198253d9acc8bc7292c9d9169c25861d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545567"
---
# <a name="obtaining-the-ndis-version"></a>获取 NDIS 版本





NDIS 版本可能不会与操作系统版本相同。 例如，如果您使用[ **RtlGetVersion** ](https://msdn.microsoft.com/library/windows/hardware/ff561910)并[ **RtlVerifyVersionInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff563026)例程，从而获取操作系统版本中，执行操作获取与特定的 NDIS 版本的有保证的关联。 因此，NDIS 驱动程序必须获得 NDIS 版本和操作系统版本单独。 NDIS 驱动程序可以获取与的 NDIS 版本[ **NdisGetVersion** ](https://msdn.microsoft.com/library/windows/hardware/ff562680)函数。

## <a name="related-topics"></a>相关主题


[NDIS 版本的概述](overview-of-ndis-versions.md)

[指定 NDIS 版本信息](specifying-ndis-version-information.md)

 

 






