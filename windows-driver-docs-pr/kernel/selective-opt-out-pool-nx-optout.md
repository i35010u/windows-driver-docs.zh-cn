---
title: 选择性选择退出 POOL_NX_OPTOUT
description: 可以全局启用一种不执行 (NX) 池参加机制的一套驱动程序源文件，然后，重写为一个或多个选定的源文件与 POOL_NX_OPTOUT 此选择机制。
ms.assetid: 15AA7CFA-5BEC-4E45-B222-0DE2D620E099
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 90f09acf6967dc08997ece19f0b37011f8195188
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543911"
---
# <a name="selective-opt-out-poolnxoptout"></a>选择性退出：池\_NX\_OPTOUT


可以全局启用的机制之一来不执行 (NX) 池参加驱动程序源文件，一组，然后，重写与池的一个或多个选定的源代码文件的此选择机制\_NX\_OPTOUT。 这样，所选的源代码文件，以继续使用可执行文件的非分页的内存。 可以使用池中\_NX\_OPTOUT 选择退出机制与每个池\_NX\_OPTIN 或池\_NX\_OPTIN\_自动选择机制。 有关详细信息，请参阅[NX 池选择的机制](nx-pool-opt-in-mechanisms.md)。

若要使用的池\_NX\_输出选择退出机制，若要覆盖选定的源代码文件中选择的机制，请向此文件添加以下定义：

`#define POOL_NX_OPTOUT 1`

此定义重写全局选择加入设置中所选文件，并阻止的实例**非分页池**从被替换的常量名称。 此定义插入的第一个实例之前的文件**非分页池**文件中。

使用该池的替代方法\_NX\_OPTOUT 源文件中的选择退出机制是显式的每个实例替换为**非分页池**文件中带有**NonPagedPoolExecute**.

 

 




