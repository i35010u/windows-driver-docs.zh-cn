---
title: '[可选]注册回调例程'
description: '[可选]注册回调例程'
ms.assetid: 59d15b37-e31e-45fc-bdb0-fed6f791839c
keywords:
- 注册回调例程
- 回调例程 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee6a020b27dd40fcabfb4a10d3b1aad20144895d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525868"
---
# <a name="optional-registering-callback-routines"></a>\[可选\]注册回调例程


## <span id="ddk_registering_callback_routines_if"></span><span id="DDK_REGISTERING_CALLBACK_ROUTINES_IF"></span>


筛选器驱动程序可以调用[ **IoRegisterFsRegistrationChange** ](https://msdn.microsoft.com/library/windows/hardware/ff548499)若要注册的文件系统驱动程序调用时要调用的回调例程[ **IoRegisterFileSystem** ](https://msdn.microsoft.com/library/windows/hardware/ff548494)或[ **IoUnregisterFileSystem** ](https://msdn.microsoft.com/library/windows/hardware/ff548552)注册或取消注册自身。 筛选器驱动程序注册此回调例程，以便他们可以看到输入系统，并选择是否要向其附加新的文件系统。

**请注意**  永远不会调用文件系统筛选器驱动程序必须[ **IoRegisterFileSystem** ](https://msdn.microsoft.com/library/windows/hardware/ff548494)或者[ **IoUnregisterFileSystem**](https://msdn.microsoft.com/library/windows/hardware/ff548552). 这些例程仅适用于文件系统。

 

仅当显式定向 （例如，由用户模式应用程序） 时的卷将附加的筛选器驱动程序不应调用[ **IoRegisterFsRegistrationChange**](https://msdn.microsoft.com/library/windows/hardware/ff548499)。 但请注意，使用此例程的筛选器的该卷已装载后立即将附加到任何给定卷的功能。 使用此例程不保证该筛选器将直接关联到卷设备对象。 但它确保此类筛选附加之前 （并因此下面） 改为将等待命令从用户模式应用程序，因为筛选器可以仅在当前文件系统卷设备堆栈的顶部将附加的筛选器。

 

 




