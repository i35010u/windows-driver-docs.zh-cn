---
title: 下载队列特定的文件
description: 下载队列特定的文件
ms.assetid: b6aad46a-2934-461a-ad11-6ad699687fc1
keywords:
- 下载队列特定的打印机文件
- 指向和打印 WDK，特定队列的文件
- 队列特定文件 WDK 打印机
- 打印队列-WDK，点和打印
- 队列 WDK 打印机，指向和打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9bb235322a128a1ab66a7623eb13c8494554e952
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837724"
---
# <a name="downloading-queue-specific-files"></a>下载队列特定的文件





如果用户决定创建一个从其客户端系统到打印服务器的打印机连接，并且如果安装应用程序已创建在安装安装过程中所述的注册表项[并在打印机安装过程中打印](supporting-point-and-print-during-printer-installations.md)，则以下事件就

1.  用户应用程序调用**AddPrinterConnection**，如 Microsoft Windows SDK 文档中所述。

2.  客户端的远程打印提供程序（Win32spl.dll）创建与服务器的连接。

3.  服务器的后台处理程序将驱动程序文件发送到客户端。

4.  客户端的 Win32spl.dll 在服务器上调用 EnumPrinterKey 和 EnumPrinterDataEx，以复制打印机的注册表项。

5.  当服务器的后台处理程序在处理 EnumPrinterDataEx 的过程中枚举注册表值时，它会在每次遇到打印机的**CopyFiles**密钥子项时执行以下操作，例如**CopyFiles\\ICM**：
    -   加载[点和打印 DLL](point-and-print-dlls.md)（如果已指定），并调用它的[**GenerateCopyFilePaths**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-generatecopyfilepaths)函数，该函数可以修改源路径和/或目标路径。
    -   基于**GenerateCopyFilePaths**返回的源路径和目标路径创建**SourceDir**和**TargetDir**键，并将它们作为 EnumPrinterDataEx 数据返回到客户端后台处理程序。 （这些密钥并不真正存在于服务器上。）

6.  客户端的 Win32spl.dll 会缓存接收的打印机密钥，以响应 EnumPrinterData 和 EnumPrinterDataEx 调用。

7.  对于打印机的**CopyFiles**键的每个子项（如**CopyFiles\\ICM**），客户端的 win32spl.dll 执行以下操作：
    -   如果提供了本地点和打印 DLL，则加载它们，并调用它的**GenerateCopyFilePaths**函数，该函数可以修改源路径和/或目标路径。 （输入是从服务器接收的**SourceDir**和**TargetDir**键。）
    -   从服务器下载所有与**files**密钥关联的文件。
    -   记录事件，指示下载了点和打印文件。
    -   如果提供了 DLL，则调用点和打印 DLL 的[**SpoolerCopyFileEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-spoolercopyfileevent)函数，指定 COPYFILE\_\_事件\_CHANGED 事件。

8.  客户端后台处理程序调用驱动程序的[**DrvPrinterEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvprinterevent)函数，并指定打印机\_事件\_缓存\_刷新事件。

9.  客户端后台处理程序再次调用驱动程序的[**DrvPrinterEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvprinterevent)函数，并指定打印机\_事件\_添加\_连接事件。

10. 如果提供了 Point 和打印 DLL，则客户端后台处理程序将调用其[**SpoolerCopyFileEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-spoolercopyfileevent)函数，指定 COPYFILE\_事件，\_添加\_打印机\_连接事件。

### <a name="connection-example"></a>连接示例

例如，假定安装应用程序已定义安装示例中所述的服务器注册表项。 此外，假定服务器命名为 NTPRINT.INF，并且客户端名为 MyClient。

若要在 NTPRINT.INF 上连接到名为 HpColor 的打印队列，MyClient 上的用户应用程序会调用**AddPrinterConnection** ，如下所示：

```cpp
AddPrinterConnection("\\NTPRINT\HpColor")
```

在服务器上，后台处理程序加载 Mscms 并调用[**GenerateCopyFilePaths**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-generatecopyfilepaths) ，如下所示：

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

Microsoft ICM 的 Mscms .dll 模块不会修改源路径或目标路径，因此它只会返回错误\_成功。

服务器后台处理程序将以下项返回到 MyClient：

```cpp
SourceDir: \\NTPRINT\PRINT$\Color
TargetDir: "Color"
```

在客户端上， **TargetDir**的值扩展到 C：\\Winnt\\System32\\假脱机\\驱动程序\\颜色。

MyClient 上的后台处理程序执行以下操作：

-   下载 Mscms 并调用[**GenerateCopyFilePaths**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-generatecopyfilepaths) ，如下所示：

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

    Microsoft ICM 的 Mscms .dll 模块不会修改源路径或目标路径，因此它只会返回错误\_成功。

-   将 Hpclrlsr 下载到 C：\\Winnt\\System32\\假脱机\\驱动程序\\颜色。

-   记录事件，指示下载了点和打印文件。

-   调用 SpoolerCopyFileEvent 中的[](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-spoolercopyfileevent)函数，并指定 COPYFILE\_\_事件\_CHANGED 事件。

-   调用打印机驱动程序的[**DrvPrinterEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvprinterevent)函数，并指定打印机\_事件\_缓存\_刷新事件。

-   再次调用打印机驱动程序的[**DrvPrinterEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvprinterevent)函数，指定打印机\_事件\_添加\_连接事件。

-   调用 SpoolerCopyFileEvent 中的[](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-spoolercopyfileevent)函数，指定 COPYFILE\_事件，\_添加\_打印机\_连接事件。

 

 




