---
title: 初始化 UMDF 中的常规 I/O 目标
description: 初始化 UMDF 中的常规 I/O 目标
ms.assetid: cf1b39c3-4c82-411b-8eef-117ac0fe793e
keywords:
- 常规 I/O 面向 WDK UMDF，初始化
- 初始化常规 I/O 面向 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85099a67f1f3fb14c468b184f9fcebf248236777
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545663"
---
# <a name="initializing-a-general-io-target-in-umdf"></a>初始化 UMDF 中的常规 I/O 目标


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

您的驱动程序使用来初始化常规 I/O 目标的步骤取决于 I/O 目标是否[本地](general-i-o-targets-in-umdf.md)或远程。

### <a name="initializing-a-local-io-target"></a>初始化本地 I/O 目标

本地 I/O 目标包括设备的[默认 I/O 目标](general-i-o-targets-in-umdf.md)和基于文件句柄的 I/O 目标。

当驱动程序调用时，框架初始化设备驱动程序的默认 I/O 目标[ **IWDFDriver::CreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff558899)方法。 若要检索[IWDFIoTarget](https://msdn.microsoft.com/library/windows/hardware/ff559170)接口，使驱动程序来访问设备的默认 I/O 目标，驱动程序调用[ **IWDFDevice::GetDefaultIoTarget** ](https://msdn.microsoft.com/library/windows/hardware/ff558831)方法。

大多数驱动程序将请求发送到其默认 I/O 目标仅。

如果 UMDF 驱动程序必须将 I/O 请求发送到基于句柄的接口，如网络套接字接口，该驱动程序必须创建一个基于文件句柄的 I/O 目标对象。 若要创建基于文件的句柄的 I/O 目标对象，该驱动程序必须执行以下操作：

1.  调用**QueryInterface**设备的方法[IWDFDevice](https://msdn.microsoft.com/library/windows/hardware/ff556917)接口来检索一个指向[IWDFFileHandleTargetFactory](https://msdn.microsoft.com/library/windows/hardware/ff558926)接口。

2.  通过调用 Win32 获取 Win32 句柄到文件、 命名的管道或套接字[ **CreateFile**](https://msdn.microsoft.com/library/windows/desktop/aa363858)， **CreateNamedPipe**，或者**套接字**函数.

3.  调用[ **IWDFFileHandleTargetFactory::CreateFileHandleTarget** ](https://msdn.microsoft.com/library/windows/hardware/ff558930)方法来创建文件、 管道或套接字的基于文件句柄的 I/O 目标对象。

有关代码示例演示如何检索[IWDFFileHandleTargetFactory](https://msdn.microsoft.com/library/windows/hardware/ff558926)接口、 获取 Win32 句柄，并创建一个基于文件句柄的 I/O 目标对象、 在代码示例，请参阅[ **IWDFFileHandleTargetFactory::CreateFileHandleTarget**](https://msdn.microsoft.com/library/windows/hardware/ff558930)。

该驱动程序创建基于文件句柄的 I/O 目标后，该驱动程序可以将 I/O 请求发送到 I/O 目标。

### <a name="initializing-a-remote-io-target"></a>初始化远程 I/O 目标

您的驱动程序可以使用远程 I/O 目标之前，它必须创建一个远程目标对象和打开目标，按如下所示：

1.  调用[ **IWDFDevice2::CreateRemoteTarget** ](https://msdn.microsoft.com/library/windows/hardware/ff556928)创建一个远程目标对象。

2.  调用[ **IWDFRemoteTarget::OpenFileByName** ](https://msdn.microsoft.com/library/windows/hardware/ff560273) （适用于文件） 或[ **IWDFRemoteTarget::OpenRemoteInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff560276) （对于[设备接口](using-device-interfaces-in-umdf-drivers.md)) 以打开 I/O 操作的目标。

 

 





