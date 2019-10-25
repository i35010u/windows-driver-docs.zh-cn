---
title: 使用 IStiUSD 转义方法
description: 使用 IStiUSD 转义方法
ms.assetid: f9b1ede6-8311-4cc9-8bf7-20018cb35a3d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eccea0d85fad4d376ee7c69bae100e6642802a9f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840727"
---
# <a name="using-the-istiusd-escape-method"></a>使用 IStiUSD 转义方法





调用[**IStiUSD：： Escape**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-escape)方法将信息直接传递到硬件。 只有 Windows XP 和更高版本的操作系统才支持此方法。

与 TWAIN 兼容的应用程序和 WIA 驱动程序之间的所有通信都首先进入数据源管理器（*TWAIN\_32 .dll*），而后者又调用了 TWAIN 兼容层（*wiadss*）。 然后，TWAIN 兼容层调用 WIA 驱动程序的[**IStiUSD：： Escape**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-escape)方法，并向方法传递以下两个转义代码之一：

[ESC\_TWAIN\_功能转义代码](esc-twain-capability-escape-code.md)

[ESC\_TWAIN\_PRIVATE\_支持\_大写转义代码](esc-twain-private-supported-caps-escape-code.md)

当 TWAIN 应用程序请求 WIA 驱动程序的私有功能列表时，TWAIN 兼容层会调用驱动程序的**IStiUSD：： Escape**方法，并在调用中传递 ESC\_TWAIN\_PRIVATE\_支持\_cap。 如果驱动程序不支持传递功能，它将返回 TWAIN 兼容层的静态（默认）功能列表。 否则，驱动程序将向 TWAIN 兼容层返回受支持的私有功能的列表。

当 TWAIN 应用程序发送不在 TWAIN 兼容层的默认列表中的功能操作时，TWAIN 兼容层会调用驱动程序的**IStiUSD：： Escape**方法，这次将 ESC 传递\_TWAIN\_调用中的功能。

不过，上述说明有点 oversimplified。 当 TWAIN 应用程序要求提供驱动程序的私有功能列表时，TWAIN 兼容层实际上会对驱动程序的**IStiUSD：： Escape**方法进行两次调用。 在第一次调用中，TWAIN 兼容层要求 WIA 驱动程序存储功能列表所需的内存量。 然后，TWAIN 兼容性层为 WIA 驱动程序分配要使用的内存量。 在第二次调用中，TWAIN 兼容层向功能列表请求 WIA 驱动程序，WIA 驱动程序会将其复制到前面提到的内存中。 TWAIN 兼容层负责分配和释放 TWAIN WIA 事务中使用的所有内存。 这种安排可防止 WIA 驱动程序释放 TWAIN 兼容层所使用的内存。

当通过 ESC\_TWAIN\_功能，并且其目的是获取功能时，TWAIN 兼容层还会调用驱动程序的**IStiUSD：： Escape**方法两次。 第一次调用会询问 WIA 驱动程序存储功能所需的内存量，而第二次调用则返回该功能。 请注意，SET 功能操作只需调用**IStiUSD：： Escape**，因为无需分配任何内存。

对**IStiUSD：： Escape**方法的所有调用都应按以下顺序进行验证：

1.  验证*EscapeFunction*函数代码。 如果无效，则立即失败。 这可以防止在驱动程序中处理错误代码。

2.  验证传入缓冲区*lpInData*。 如果无效，则立即失败。 无效的传入缓冲区可能导致 WIA 驱动程序崩溃。

3.  验证传出缓冲区*pOutData*。 如果无效，则立即失败。 如果驱动程序无法通过编写必要的数据来完成请求，则不需要处理该数据。

4.  验证输出缓冲区的大小。 如果驱动程序无法向传出缓冲区写入正确的数据量，则调用方无法正确处理这些数据。

以下部分中的代码示例演示如何使用传递功能，并支持具有私有功能的 TWAIN 应用程序。 代码示例使用头文件*wiatwcmp*中定义的两个转义代码，ESC\_TWAIN\_PRIVATE\_支持\_CAP 和 ESC\_TWAIN\_功能。

[ESC\_TWAIN\_PRIVATE\_支持\_大写转义代码](esc-twain-private-supported-caps-escape-code.md)

[ESC\_TWAIN\_功能转义代码](esc-twain-capability-escape-code.md)

 

 




