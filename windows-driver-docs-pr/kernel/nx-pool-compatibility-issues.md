---
title: NX 池兼容性问题
description: 当你使用 NX Windows 8 的驱动程序二进制文件中的非分页缓冲的池，你将发现兼容性问题如果您在早期版本的 Windows 上运行这些二进制文件。
ms.assetid: 652AE9A2-D733-4EC2-9D49-B95DDABE42B1
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 67a23d8b593d0bcd944e187980ef25e7f021cc07
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365419"
---
# <a name="nx-pool-compatibility-issues"></a>NX 池兼容性问题


当你使用 NX Windows 8 的驱动程序二进制文件中的非分页缓冲的池，你将发现兼容性问题如果您在早期版本的 Windows 上运行这些二进制文件。

Windows 8 是第一个版本的 Windows 支持 NX 非分页缓冲的池。 但是，大量现有的内核模式驱动程序二进制文件是适用于 Windows 7 和早期版本的 x86、 x64 和 IA64 处理器体系结构运行的 Windows。 若要分配非分页的内存，这些驱动程序可执行文件的非分页缓冲的池改为使用 NX 非分页缓冲的池。 为了向后兼容，内核模式驱动程序的二进制文件和某些早期版本的 Windows，Windows 7 上的运行和的非分页池中分配的内存将运行 Windows 8 上无需修改即可。 但是，这些驱动程序不会利用可用性的 NX Windows 8 中的非分页缓冲的池。

## <a name="running-existing-driver-binaries-on-windows8"></a>运行现有 Windows 8 上的驱动程序二进制文件


驱动程序二进制文件生成适用于 Windows 7 （或可能是针对 Windows 的早期版本），并使用**非分页池**库类型，则不会阻止从 Windows 8 上运行。 若要启用向后兼容性**NonPagedPoolExecute**常数定义为具有相同的值**非分页池**常量中[**池\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_pool_type)枚举。 因此，在任何版本的 Windows 中此驱动程序的运行，该驱动程序从非分页缓冲池分配的内存始终是可执行文件。

Windows 8 是 Windows，以支持 ARM 体系结构的第一个版本。 因此，没有驱动程序二进制文件的 ARM 内置于早期版本的 Windows，这需要进行向后兼容性。 相反，应为 Windows 编写在 ARM 上的所有驱动程序指定**NonPagedPoolNx**而不是**NonPagedPoolExecute**中其非分页缓冲池分配，除非它们明确要求使用可执行文件内存。

如果从 x86、 x64 或 IA64，驱动程序移植到 ARM[池\_NX\_OPTIN\_自动](multiple-binary-opt-in-pool-nx-optin-auto.md)选择机制自动应用驱动程序生成过程。 此选择机制使用预处理器要替换的所有实例，默认情况下**非分页池**使用的常量名称**NonPagedPoolNx**。 如有必要，您可以使用[池\_NX\_OPTOUT](selective-opt-out-pool-nx-optout.md)选择退出机制以覆盖每个文件基于此选择机制。

## <a name="other-compatibility-issues"></a>其他兼容性问题


**NonPagedPoolNx**从 Windows 8 开始支持池类型。 不要使用此池类型中的驱动程序的早期版本的 Windows。 在这些早期版本的 Windows 中的池分配器无法正常运行时驱动程序会请求使用的分配**NonPagedPoolNx**池类型。

在 Windows 8 之前的 Windows 版本**NonPagedPoolExecute**池类型可以自由地用来替代**非分页池**池类型。 [**池\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_pool_type)枚举定义**非分页池**并**NonPagedPoolExecute**以具有相同的值。

## <a name="nx-pool-type-porting-guidelines"></a>NX 池类型移植指南


当你移植到 Windows 8 或更高版本从早期版本的 Windows 驱动程序代码时，有几种方法来添加对支持**NonPagedPoolNx**并**NonPagedPoolExecute**池类型。 从以下列表中，选择最适合你需求的方法：

-   如果您的驱动程序不应早于 Windows 8 的 Windows 版本上运行，大多数或所有实例替换为**非分页池**与**NonPagedPoolNx**。 仅开发人员很少应替换的实例**非分页池**与**NonPagedPoolExecute。**

-   如果驱动程序源代码面向 Windows 8 和早期版本的 Windows，并提供不同的驱动程序二进制文件为每个版本，使用池\_NX\_OPTIN\_自动选择机制。 此方法不需要的实例替换**非分页池**驱动程序源中。 有关详细信息，请参阅[NX 池选择的机制](nx-pool-opt-in-mechanisms.md)。

-   如果驱动程序源代码面向 Windows 8 和早期版本的 Windows，并提供单个驱动程序二进制文件以在所有受支持版本上运行，使用池\_NX\_OPTIN 选择机制。 此方法不需要的实例替换**非分页池**驱动程序源中。 有关详细信息，请参阅[NX 池选择的机制](nx-pool-opt-in-mechanisms.md)。

通过使用以下三种方法之一，大多数驱动程序可以快速地不费吹灰之力移植。

避免只需替换的所有实例**非分页池**将驱动程序代码中**NonPagedPoolExecute**。 使用**NonPagedPoolExecute**池类型仅用于必须是可执行文件的池分配 (例如，若要运行代码生成的只是时间或 JIT，编译器)。

 

 




