---
title: 单个二进制参加 POOL_NX_OPTIN
description: 若要生成运行在 Windows 8 和 Windows 的早期版本中的单个驱动程序二进制文件，请使用 POOL_NX_OPTIN 参加机制。
ms.assetid: BE9D3C85-0212-4206-A59B-4D53FB842C39
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 00366b375a953a585acadf52f8cca8331f6ad943
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521518"
---
# <a name="single-binary-opt-in-poolnxoptin"></a>单个二进制参加：池\_NX\_OPTIN


若要生成单独的驱动程序二进制文件运行在 Windows 8 和 Windows 的早期版本中，使用该池\_NX\_OPTIN 选择机制。 这是第三方硬件供应商提供单个驱动程序支持多个 Windows 版本的二进制移植辅助工具。

若要使用此选择机制，请执行以下操作：

-   定义池\_NX\_OPTIN = 1 的所有源你想要参加的文件。 若要执行此操作，包括驱动程序项目的相应的属性页中的以下预处理器定义：

    `C_DEFINES=$(C_DEFINES) -DPOOL_NX_OPTIN=1`

-   在你[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113) （或等效） 例程，包括以下函数调用：

    `ExInitializeDriverRuntime(DrvRtPoolNxOptIn);`

    驱动程序，可以使用任何分配之前，必须进行此调用**非分页池**池类型或可以为任何调用[ **ExInitializeNPagedLookasideList** ](https://msdn.microsoft.com/library/windows/hardware/ff545301)例程。 **ExInitializeDriverRuntime**是强制内联函数，可以在 Windows 8 或更高版本的 Windows 上调用。

对于大多数驱动程序，这两项任务是足以让单个驱动程序二进制文件的选择的机制。

## <a name="implementation-details"></a>实现详细信息


池\_NX\_OPTIN 的工作原理是替换**非分页池**具有全局[**池\_类型**](https://msdn.microsoft.com/library/windows/hardware/ff559707)变量， `ExDefaultNonPagedPoolType`，这是初始化到**NonPagedPoolNx** （适用于 Windows 8 和更高版本的 Windows） 或**NonPagedPoolExecute** （适用于 Windows 的早期版本）。 此选择机制使您的内核模式驱动程序运行在 Windows 8 中，与增强保护 NX 池，并在早期版本的 Windows，不支持 NX 池。 实例之间进行转换的宏**非分页池**常量名称到**NonPagedPoolNx**也会将转换的实例**NonPagedPoolCacheAligned**到**NonPagedPoolNxCacheAligned**。

## <a name="support-for-static-libraries-lib-projects"></a>静态库 （.lib 项目） 的支持


可以使用池中\_NX\_.lib 项目，但通常链接到.lib 的项目的 OPTIN 选择机制还必须使用池\_NX\_OPTIN。 最小值，该项目，它实现[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程必须包含以下函数调用：

`ExInitializeDriverRuntime(DrvRtPoolNxOptIn);`

 

 




