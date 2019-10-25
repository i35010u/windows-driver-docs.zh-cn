---
title: 创建导出驱动程序
description: 创建导出驱动程序
ms.assetid: 60ce7d0d-0eab-4af6-890a-45ab206816aa
keywords:
- 导出驱动程序 WDK 内核
- 正在加载导出驱动程序 WDK 内核
- 导入导出驱动程序函数
- 模块定义文件 WDK 内核
- .def 文件
- def 文件
- 内核模式驱动程序 WDK，导出驱动程序
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3147712503f4356519c41b5dbc09b6a96d70742b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828450"
---
# <a name="creating-export-drivers"></a>创建导出驱动程序





Microsoft Windows 驱动程序通常定义为一对组件，例如端口/微型端口驱动程序对或 class/miniclass 驱动程序对。 通常，Microsoft 提供独立于硬件的类或端口驱动程序，并且供应商提供硬件相关的 miniclass 或微型端口驱动程序。

内核模式导出驱动程序特别适用于实现与基础堆栈和硬件特征无关的驱动程序对部分，因为导出驱动程序是可以由各种其他项加载的内核模式 DLL特定于硬件或设备堆栈的组件。 Microsoft 附带多个驱动程序，同时提供属于此类别的 Windows 操作系统。 例如，SCSI 端口驱动程序、磁带类驱动程序、IDE 控制器驱动程序都是由其他驱动程序加载的系统提供的导出驱动程序。

导出驱动程序缺少完整的内核模式驱动程序的很多特性。 导出驱动程序没有调度表，它在驱动程序堆栈中没有位置，并且在将其定义为系统服务的服务控制管理器数据库中没有条目。 导出驱动程序具有[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程，但绝不会调用其**DriverEntry**例程。 （例程只是一个存根来满足生成脚本的要求。）

请注意，尽管导出驱动程序没有调度表，但它可以向标准驱动程序提供调度例程。 标准驱动程序将调度例程插入其自己的调度表中。

标准驱动程序还可以充当导出驱动程序。 若要使驱动程序以这两种方式运行，必须将其构建为导出驱动程序并作为常规驱动程序加载。

### <a name="building-an-export-driver"></a>构建导出驱动程序

若要构建驱动程序作为导出驱动程序，必须在驱动程序的源文件中定义多个生成实用工具宏。

首先，必须为**TARGETTYPE**宏分配适当的值，如下所示：

```cpp
TARGETTYPE=EXPORT_DRIVER
```

还必须使用**DLLDEF**宏指定模块定义（.def）文件。 例如：

```cpp
DLLDEF="c:\project\driver.def"
```

模块定义文件提供编译器和链接器，其中包含导出的例程列表和其他信息。 有关模块定义文件的详细信息，请参阅 Microsoft Visual C++文档。

构建内核模式 DLL 时，不能使用生成用户模式 DLL 时所使用的许多生成实用工具宏。 

例如，内核模式 DLL 的入口点始终为**DllInitialize**。 加载 DLL 后，系统立即调用内核模式 DLL 的 DllInitialize 例程。 导出驱动程序必须提供**DllInitialize**例程。 可以使用**DllInitialize**例程获取或初始化 DLL 中其他例程所需的资源。 

不能使用**DLLENTRY**宏指定入口点。 

```cpp
NTSTATUS DllInitialize(
  _In_ PUNICODE_STRING RegistryPath
);
```
RegistryPath 是一个指向已计数的 Unicode 字符串的指针，该字符串指定 DLL 的注册表项**HKEY_LOCAL_MACHINE\CurrentControlSet\Services\DllName**的路径。 DLL 例程可以使用此密钥来存储特定于 DLL 的信息。 **DllInitialize**退出后，RegistryPath 所指向的缓冲区将被释放。 因此，如果 DLL 使用该密钥，则**DllInitialize**必须复制该密钥名称。 


生成过程将生成一个扩展名为 .lib 的导出库，并生成一个扩展名为 .sys 的导出驱动程序。

### <a name="importing-functions-from-an-export-driver"></a>从导出驱动程序导入函数

若要导入导出驱动程序导出的函数，应使用在 Ntdef 中定义的 DECLSPEC\_IMPORT 宏声明函数。 例如：

```cpp
DECLSPEC_IMPORT int LoadPrinterDriver (int arg1); 
```

此宏可在必要时解析到这些平台上的 **\_\_declspec**（dllimport）存储类声明，无需在这些平台上进行任何操作。

在导出驱动程序中，应通过 DECLSPEC\_导出宏声明要导出的函数。 此宏可在必要时解析到这些平台上的 **\_\_declspec**（dllexport）存储类声明，无需在这些平台上进行任何操作。 如果导出驱动程序为标准驱动程序提供了调度例程，则不需要导出该例程。

### <a name="loading-and-unloading-an-export-driver"></a>加载和卸载导出驱动程序

导出驱动程序必须安装在% Windir%\\System32\\驱动程序目录中。 从 Windows 2000 开始，操作系统会保留一个引用计数，指示其他驱动程序导入了导出驱动程序的函数的次数。 当卸载其中一个导入驱动程序时，系统会减少此计数。 当引用计数降为零时，系统卸载导出驱动程序。 但是，导出驱动程序必须包含标准入口点和卸载例程、 **DllInitialize**和**DllUnload**，或者操作系统不会激活此引用计数机制。

当系统卸载 DLL 时，系统会调用内核模式 DLL 的 DllUnload 例程。

```cpp
NTSTATUS DllUnload(void);
```
导出驱动程序必须提供 DllUnload 例程。 您可以使用 DllUnload 例程来释放由 DLL 中的例程使用的所有资源。 








