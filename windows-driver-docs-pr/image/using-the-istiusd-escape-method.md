---
title: 使用 IStiUSD 转义方法
description: 使用 IStiUSD 转义方法
ms.assetid: f9b1ede6-8311-4cc9-8bf7-20018cb35a3d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 963accfe0d2908aab78faabd35d778ac49f128ee
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521092"
---
# <a name="using-the-istiusd-escape-method"></a>使用 IStiUSD 转义方法





[ **IStiUSD::Escape** ](https://msdn.microsoft.com/library/windows/hardware/ff543815)调用方法将信息传递给硬件直接。 仅在 Windows XP 和更高版本操作系统上支持此方法。

TWAIN 兼容的应用程序和 WIA 驱动程序之间的所有通信将首先都转到数据源管理器 (*twain\_32.dll*)，这反过来调用 TWAIN 兼容性层 (*wiadss.dll*). TWAIN 兼容性层然后调用 WIA 驱动[ **IStiUSD::Escape** ](https://msdn.microsoft.com/library/windows/hardware/ff543815)方法，并传递一个以下两个转义代码的方法：

[ESC\_TWAIN\_功能转义码](esc-twain-capability-escape-code.md)

[ESC\_TWAIN\_专用\_支持\_CAPS 转义代码](esc-twain-private-supported-caps-escape-code.md)

TWAIN 兼容性层 TWAIN 应用程序请求 WIA 驱动程序的专用功能列表，当调用的驱动程序**IStiUSD::Escape**方法，传递 ESC\_TWAIN\_专用\_支持\_的调用中的上限。 如果该驱动程序不支持传递功能，它将返回 TWAIN 兼容性层的静态 （默认值） 功能列表。 否则，该驱动程序返回 TWAIN 兼容性层支持的专用功能的列表。

TWAIN 兼容性层 TWAIN 应用程序发送的功能操作中，不是 TWAIN 兼容性层的默认列表时, 调用的驱动程序**IStiUSD::Escape**方法，这一次传递 ESC\_TWAIN\_的调用中的功能。

但是，在上述说明进行了某种程度上过度简化。 当 TWAIN 应用程序请求驱动程序的专用功能列表时，TWAIN 兼容性层实际上可以对驱动程序的两次调用**IStiUSD::Escape**方法。 在第一个调用中，TWAIN 兼容性层要求 WIA 驱动程序存储功能列表所需的内存量。 TWAIN 兼容性层然后会分配该 WIA 驱动程序使用的内存量。 在第二个调用中，TWAIN 兼容性层的功能列表中，WIA 驱动程序将复制到前面提到的内存要求 WIA 驱动程序。 TWAIN 兼容性层负责分配和释放 TWAIN WIA 的事务中使用的所有内存。 这种排列方式可防止 WIA 驱动程序释放的内存使用了 TWAIN 兼容性层。

TWAIN 兼容性层还会调用驱动程序的**IStiUSD::Escape**方法两次时 ESC\_TWAIN\_传递功能，其目的是获取一项功能。 第一次调用要求 WIA 驱动程序存储功能，所需的内存量和第二次调用返回的功能。 请注意，设置功能操作需要仅调用一次**IStiUSD::Escape**，因为需分配任何内存。

所有调用的**IStiUSD::Escape**应按以下顺序验证方法：

1.  验证*EscapeFunction*函数代码。 如果不是有效的立即失败。 这可以防止在驱动程序处理不正确的代码。

2.  验证传入缓冲区*lpInData*。 如果不是有效的立即失败。 无效的传入缓冲区可能会导致崩溃的 WIA 驱动程序。

3.  验证输出缓冲区*pOutData*。 如果不是有效的立即失败。 如果通过编写必要的数据，该驱动程序无法完成请求，它不会不需要处理这些数据。

4.  验证传出的缓冲区的大小。 如果该驱动程序不能向输出缓冲区写入正确的数据量，调用方不能正确处理该数据。

以下各节中的代码示例说明如何通过使用-尽管 TWAIN 与专用功能的应用程序提供支持的功能。 代码示例使用两个标头文件中定义的转义码*wiatwcmp.h*，ESC\_TWAIN\_专用\_支持\_帽的直线和 ESC\_TWAIN\_功能。

[ESC\_TWAIN\_专用\_支持\_CAPS 转义代码](esc-twain-private-supported-caps-escape-code.md)

[ESC\_TWAIN\_功能转义码](esc-twain-capability-escape-code.md)

 

 




