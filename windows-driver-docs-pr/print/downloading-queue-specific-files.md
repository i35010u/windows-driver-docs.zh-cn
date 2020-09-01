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
ms.date: 06/09/2020
ms.localizationpriority: medium
ms.openlocfilehash: c65508fd12cc97bb1a15622ab12d54d04f0a09e7
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218213"
---
# <a name="downloading-queue-specific-files"></a>下载队列特定的文件

如果用户决定创建从客户端系统到打印服务器的打印机连接，并且如果安装应用程序已创建在安装 [安装过程](supporting-point-and-print-during-printer-installations.md)中所述的注册表项，则会发生以下事件：

1. 用户应用程序调用 **AddPrinterConnection**，如 Microsoft Windows SDK 文档中所述。

1. 客户端的远程打印提供程序 ( # A0) 创建与服务器的连接。

1. 服务器的后台处理程序将驱动程序文件发送到客户端。

1. 客户端的 Win32spl.dll 调用服务器上的 EnumPrinterKey 和 EnumPrinterDataEx 来复制打印机的注册表项。

1. 当服务器的后台处理程序在处理 EnumPrinterDataEx 的过程中枚举注册表值时，它会在每次遇到打印机的 **CopyFiles** 密钥子项时执行以下操作，如 **CopyFiles \\ ICM**：

    - 加载 [点和打印 DLL](point-and-print-dlls.md)（如果已指定），并调用它的 [**GenerateCopyFilePaths**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-generatecopyfilepaths) 函数，该函数可以修改源路径和/或目标路径。

    - 基于**GenerateCopyFilePaths**返回的源路径和目标路径创建**SourceDir**和**TargetDir**键，并将它们作为 EnumPrinterDataEx 数据返回到客户端后台处理程序。  (在服务器上不存在这些密钥。 ) 

1. 客户端的 Win32spl.dll 会缓存接收的打印机密钥，以响应 EnumPrinterData 和 EnumPrinterDataEx 调用。

1. 对于打印机的 **CopyFiles** 键的每个子项（如 **CopyFiles \\ ICM**），客户端的 Win32spl.dll 执行以下操作：

    - 如果提供了本地点和打印 DLL，则加载它们，并调用它的 **GenerateCopyFilePaths** 函数，该函数可以修改源路径和/或目标路径。  (输入是从服务器接收的 **SourceDir** 和 **TargetDir** 键。 ) 

    - 从服务器下载所有与 **files** 密钥关联的文件。

    - 记录事件，指示下载了点和打印文件。

    - 如果提供了 DLL，则调用 Point 和打印 DLL 的 [**SpoolerCopyFileEvent**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-spoolercopyfileevent) 函数，并指定 COPYFILE \_ 事件 \_ 文件 \_ CHANGED 事件。

1. 客户端后台处理程序调用驱动程序的 [**DrvPrinterEvent**](/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvprinterevent) 函数，并指定打印机 \_ 事件 \_ 缓存 \_ 刷新事件。

1. 客户端后台处理程序再次调用驱动程序的 [**DrvPrinterEvent**](/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvprinterevent) 函数，并指定打印机 \_ 事件 \_ ADD \_ 连接事件。

1. 如果提供了一个点和打印 DLL，则客户端后台处理程序将调用其 [**SpoolerCopyFileEvent**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-spoolercopyfileevent) 函数，并指定 COPYFILE \_ 事件 " \_ 添加 \_ 打印机连接" \_ 事件。

## <a name="connection-example"></a>连接示例

例如，假定安装应用程序已定义安装示例中所述的服务器注册表项。 此外，假定服务器命名为 NTPRINT.INF，并且客户端名为 MyClient。

若要在 NTPRINT.INF 上连接到名为 HpColor 的打印队列，MyClient 上的用户应用程序会调用 **AddPrinterConnection** ，如下所示：

```cpp
AddPrinterConnection("\\NTPRINT\HpColor")
```

在服务器上，后台处理程序加载 Mscms.dll 并调用 [**GenerateCopyFilePaths**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-generatecopyfilepaths) ，如下所示：

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

Microsoft ICM 的 Mscms.dll 模块不会修改源路径或目标路径，因此它只会返回错误 \_ SUCCESS。

服务器后台处理程序将以下项返回到 MyClient：

```cpp
SourceDir: \\NTPRINT\PRINT$\Color
TargetDir: "Color"
```

在客户端上， **TargetDir** 的值扩展到 C： \\ Winnt \\ System32 \\ 假脱机 \\ 驱动程序 \\ 颜色。

MyClient 上的后台处理程序执行以下操作：

- 下载 Mscms.dll 并调用 [**GenerateCopyFilePaths**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-generatecopyfilepaths) ，如下所示：

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

    Microsoft ICM 的 Mscms.dll 模块不会修改源路径或目标路径，因此它只会返回错误 \_ SUCCESS。

- 将 Hpclrlsr 下载到 C： \\ Winnt \\ System32 \\ 假脱机 \\ 驱动程序 \\ 颜色。

- 记录事件，指示下载了点和打印文件。

- 在 Mscms.dll 中调用 [**SpoolerCopyFileEvent**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-spoolercopyfileevent) 函数，并指定 COPYFILE \_ 事件 \_ 文件 \_ CHANGED 事件。

- 调用打印机驱动程序的 [**DrvPrinterEvent**](/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvprinterevent) 函数，并指定打印机 \_ 事件 \_ 缓存 \_ 刷新事件。

- 再次调用打印机驱动程序的 [**DrvPrinterEvent**](/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvprinterevent) 函数，并指定打印机 \_ 事件 \_ ADD \_ 连接事件。

- 在 Mscms.dll 中调用 [**SpoolerCopyFileEvent**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-spoolercopyfileevent) 函数，指定 COPYFILE \_ 事件 " \_ 添加 \_ 打印机 \_ 连接事件"。