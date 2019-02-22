---
title: 将源标记为可移动
description: 将源标记为可移动
ms.assetid: 7fe48a4b-25d2-4e2c-9c26-a425928947ce
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6e645c8f2454b9afe5190806172a5f1c8ac01db
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547412"
---
# <a name="marking-sources-as-removable"></a>将源标记为可移动


若要防止进行视频显示源的主视图的显示应用程序，应将标记为可移动的源。 若要指示的源是可移动，可以指定 DWORD Plug and Play (PnP) 值在注册表中名为**RemovableSources**。

**请注意**  不能将标记为可移动的 DWORD 位字段值中的源 0。

 

N<sup>th</sup>位的位字段值中指定源 n-1 是否可移动。 例如，若要将标记为可移动的源 1，可以到显示微型端口驱动程序的 INF 文件添加以下行：

```inf
HKR,, RemovableSources, %REG_DWORD%, 2
...
```

有关安装显示器驱动程序的详细信息，请参阅[显示微型端口和用户模式显示驱动程序的安装要求](installing-display-miniport-and-user-mode-display-drivers.md)。

 

 





