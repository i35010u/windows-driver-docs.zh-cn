---
title: 在 UMDF 1.x 驱动程序中读取和写入设备注册
description: 在 UMDF 1.x 驱动程序中读取和写入设备注册
ms.assetid: A0640E60-B0DF-4CAD-B292-CC1875EF7F7D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 189fa29ee87fa0214b34a6201b27dcf13e7e906b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546310"
---
# <a name="reading-and-writing-to-device-registers-in-umdf-1x-drivers"></a>在 UMDF 1.x 驱动程序中读取和写入设备注册


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

从开始 UMDF 1.11 版中，框架提供一的组例程访问的内存空间和 I/O 端口空间中的寄存器。 [UMDF 注册/端口访问例程](https://msdn.microsoft.com/library/windows/hardware/hh463975)非常类似于使用的内核模式驱动程序的 HAL 例程。 驱动程序已映射的寄存器，如中所述后[查找和 UMDF 驱动程序中映射硬件资源](https://msdn.microsoft.com/library/windows/hardware/hh439594)，则驱动程序使用读/写\_注册\_Xxx 例程以读取和写入单个注册。 对于 I/O 端口，该驱动程序调用读/写\_端口\_Xxx 例程。

此示例演示如何将写入到内存映射的注册。

```cpp
VOID
CMyQueue::WriteToDevice(
    __in IWDFDevice3* pWdfDevice,
    __in UCHAR Value
    )
{
    //
    // Write the UCHAR value at offset 2 from register base
    //
    WRITE_REGISTER_UCHAR(pWdfDevice, 
                      (m_MyDevice->m_RegBase)+2, 
                       Value);
}
```

默认情况下，UMDF 在内部使用系统调用来访问映射的内存空间中或 I/O 端口空间中的寄存器。 始终通过系统调用访问 I/O 端口空间的寄存器中。 但是，在访问内存映射寄存器，UMDF 驱动程序可能导致框架可以通过设置 INF 指令映射到用户模式地址空间的内存映射寄存器**UmdfRegisterAccessMode**到**RegisterAccessUsingUserModeMapping**。 某些驱动程序可能需要执行此操作的性能方面的原因。 请参阅[INF 文件中指定 WDF 指令](specifying-wdf-directives-in-inf-files.md)有关 UMDF INF 指令的完整列表。

该驱动程序应使用读/写\_注册\_Xxx 例程即使它已映射到用户模式下的寄存器。 这些例程验证驱动程序输入，并确保该驱动程序不请求访问无效的位置。 很少，驱动程序可能需要映射用户模式下寄存器直接访问，而无需使用这些例程。 若要执行此操作，驱动程序检索的用户模式映射地址，通过调用[ **IWDFDevice3::GetHardwareRegisterMappedAddress** ](https://msdn.microsoft.com/library/windows/hardware/hh451219)上映射的基址。 因为 UMDF 不会验证读取和写入访问以这种方式执行，这种技术不建议用于注册访问权限。

 

 





