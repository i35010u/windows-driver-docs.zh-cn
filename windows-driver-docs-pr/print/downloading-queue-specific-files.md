---
title: 下载队列特定的文件
description: 下载队列特定的文件
ms.assetid: b6aad46a-2934-461a-ad11-6ad699687fc1
keywords:
- 下载特定于队列的打印机文件
- 点和打印 WDK，特定于队列的文件
- 特定于队列的文件 WDK 打印机
- 打印队列 WDK 中，指向并打印
- 队列 WDK 打印机，指向并打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f96e29981841ccda93d675da69bec12d6b077517
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387268"
---
# <a name="downloading-queue-specific-files"></a>下载队列特定的文件





如果用户决定从他或她的客户端系统创建的打印机连接连接到打印服务器，并安装应用程序已创建的注册表项中所述[支持点和打印打印机安装期间](supporting-point-and-print-during-printer-installations.md)将发生以下事件：

1.  用户应用程序调用**AddPrinterConnection**，Microsoft Windows SDK 文档中所述。

2.  客户端的远程打印提供程序 (Win32spl.dll) 创建到服务器的连接。

3.  服务器的后台处理程序将发送到客户端的驱动程序文件。

4.  客户端的 Win32spl.dll 调用 EnumPrinterKey 和 EnumPrinterDataEx 将打印机的注册表条目复制在服务器上。

5.  服务器的后台处理程序处理 EnumPrinterDataEx 期间枚举注册表值，它执行以下操作遇到的子项的打印机的每次**CopyFiles**键，如**CopyFiles\\ICM**:
    -   加载[点和打印 DLL](point-and-print-dlls.md)，如果指定，并调用其[ **GenerateCopyFilePaths** ](https://msdn.microsoft.com/library/windows/hardware/ff549896)函数，可以修改源和/或目标路径。
    -   创建**SourceDir**并**TargetDir**键，基于返回的源和目标路径**GenerateCopyFilePaths**，并将它们返回到作为客户端后台处理程序EnumPrinterDataEx 数据。 （这些密钥不真正存在的服务器上。）

6.  客户端的 Win32spl.dll 缓存收到响应 EnumPrinterData 打印机密钥和 EnumPrinterDataEx 调用。

7.  打印机的每个子项**CopyFiles**键，如**CopyFiles\\ICM**，客户端的 Win32spl.dll 执行以下操作：
    -   加载本地点和打印 DLL，如果提供，并调用其**GenerateCopyFilePaths**函数，可以修改源和/或目标路径。 (输入**SourceDir**并**TargetDir**从服务器收到的密钥。)
    -   将下载所有文件与相关联**文件**密钥服务器。
    -   记录的事件，指示已下载指向并打印文件。
    -   调用点和打印 DLL [ **SpoolerCopyFileEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff562681)函数，如果提供一个 DLL，则指定 COPYFILE\_事件\_文件\_CHANGED 事件。

8.  客户端后台处理程序调用的驱动程序[ **DrvPrinterEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff548564)函数，并指定打印机\_事件\_缓存\_刷新事件。

9.  客户端后台处理程序调用的驱动程序[ **DrvPrinterEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff548564)函数，指定打印机\_事件\_添加\_连接事件。

10. 如果提供的点和打印 DLL，则客户端后台处理程序调用其[ **SpoolerCopyFileEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff562681)函数，并指定 COPYFILE\_事件\_添加\_打印机\_连接事件。

### <a name="connection-example"></a>连接示例

例如，假设安装应用程序定义了服务器注册表项安装示例中所述。 此外，假定服务器名为 NTPRINT 和客户端名为 MyClient。

若要连接到名为 HpColor NTPRINT，MyClient 调用上的用户应用程序上的打印队列**AddPrinterConnection** ，如下所示：

```cpp
AddPrinterConnection("\\NTPRINT\HpColor")
```

在服务器上，后台处理程序加载 Mscms.dll 并调用[ **GenerateCopyFilePaths** ](https://msdn.microsoft.com/library/windows/hardware/ff549896) ，如下所示：

```cpp
GenerateCopyFilePaths(
    "HpColor",
    "Color",
    &SplclientInfo1,
    1,
    \\NTPRINT\PRINT$\Color,
    &dwSourceDirSize,
    "Color",
    &dwDestDirSize,
    COPYFILE_FLAG_SERVER_SPOOLER)
```

Microsoft ICM Mscms.dll 模块不会修改源或目标路径，因此它只是返回错误\_成功。

服务器后台处理程序返回 MyClient 以下项：

```cpp
SourceDir: \\NTPRINT\PRINT$\Color
TargetDir: "Color"
```

在客户端的值**TargetDir**扩展到 c:\\Winnt\\System32\\Spool\\驱动程序\\颜色。

MyClient 上的后台处理程序执行以下操作：

-   下载 Mscms.dll 并调用[ **GenerateCopyFilePaths** ](https://msdn.microsoft.com/library/windows/hardware/ff549896) ，如下所示：

    ```cpp
    GenerateCopyFilePaths(
        "\\NTPRINT\HpColor",
        "Color",
        &SplclientInfo1,
        1,
        \\NTPRINT\PRINT$\Color,
        &dwSourceDirSize,
        "C:\Winnt\System32\Spool\Drivers\Color",
        &dwDestDirSize,
        COPYFILE_FLAG_CLIENT_SPOOLER)
    ```

    Microsoft ICM Mscms.dll 模块不会修改源或目标路径，因此它只是返回错误\_成功。

-   下载到 c: Hpclrlsr.icm\\Winnt\\System32\\假脱机\\驱动程序\\颜色。

-   记录的事件，指示已下载指向并打印文件。

-   调用[ **SpoolerCopyFileEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff562681) Mscms.dll，指定 COPYFILE 中的函数\_事件\_文件\_CHANGED 事件。

-   打印机驱动程序将调用[ **DrvPrinterEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff548564)函数，并指定打印机\_事件\_缓存\_刷新事件。

-   打印机驱动程序将调用[ **DrvPrinterEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff548564)函数，指定打印机\_事件\_添加\_连接事件。

-   调用[ **SpoolerCopyFileEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff562681) Mscms.dll，指定 COPYFILE 中的函数\_事件\_添加\_打印机\_连接事件。

 

 




