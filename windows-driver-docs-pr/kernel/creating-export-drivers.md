---
title: 创建导出驱动程序
description: 创建导出驱动程序
ms.assetid: 60ce7d0d-0eab-4af6-890a-45ab206816aa
keywords:
- 导出驱动程序 WDK 内核
- 加载导出驱动程序 WDK 内核
- 导入导出驱动程序函数
- 模块定义文件 WDK 内核
- .def 文件
- def 文件
- 内核模式驱动程序 WDK，导出驱动程序
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: dabe8d5d1cd4aaba5ace84bc66acb2f2830699e9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525980"
---
# <a name="creating-export-drivers"></a>创建导出驱动程序





Microsoft Windows 驱动程序通常定义为一对组件，如端口/微型端口驱动程序对或类/miniclass 驱动程序对。 通常情况下，Microsoft 提供了独立于硬件的类或端口驱动程序和供应商提供依赖于硬件的 miniclass 或微型端口驱动程序。

内核模式导出驱动程序尤其适合于实现的一部分是独立于基础堆栈和硬件特征，因为导出驱动程序是一个内核模式 DLL，它可以通过多种其他加载的驱动程序对特定于硬件的或特定于设备的堆栈的组件。 Microsoft 提供多个的驱动程序与 Windows 操作系统一起属于此类别。 例如，SCSI 端口驱动程序、 磁带类驱动程序，IDE 控制器驱动程序是由其他驱动程序加载的所有系统提供的导出驱动程序。

导出驱动程序缺少很多完整的内核模式驱动程序的特征。 导出驱动程序不具有调度表，它不具有驱动程序堆栈中的一个位置和它在其定义为系统服务的服务控制管理器的数据库中没有条目。 导出驱动程序不必[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程，但其**DriverEntry**永远不会调用例程。 （该例程是仅以满足需求的生成脚本的存根。）

请注意，虽然导出驱动程序不具有调度表，则它可以提供给标准驱动程序的调度例程。 标准驱动程序在自己的调度表中插入的调度例程。

标准驱动程序还能够根据导出驱动程序。 这两种方式中对函数的驱动程序，它必须生成作为导出驱动程序并作为常规驱动程序加载。

### <a name="building-an-export-driver"></a>生成导出驱动程序

若要生成作为导出驱动程序的驱动程序必须驱动程序的源文件中定义多个生成实用工具宏。

首先，必须将分配到适当的值**TARGETTYPE**宏，如下所示：

```cpp
TARGETTYPE=EXPORT_DRIVER
```

此外必须指定模块定义 (.def) 文件使用**DLLDEF**宏。 例如：

```cpp
DLLDEF="c:\project\driver.def"
```

模块定义文件提供了编译器和链接器的其他信息一起导出的例程的列表。 有关模块定义文件的详细信息，请参阅 Microsoft Visual c + + 文档。

许多生成用户模式 DLL 中采用的生成实用工具宏无法生成内核模式 DLL 时使用。 

例如，内核模式 DLL 的入口点是始终**DllInitialize**。 系统加载 DLL 后立即调用内核模式 DLL 的 DllInitialize 例程。 导出驱动程序必须提供**DllInitialize**例程。 可以使用**DllInitialize**例程，以获取或初始化由 DLL 中其他例程所需的资源。 

不能指定入口点使用**DLLENTRY**宏。 

```cpp
NTSTATUS DllInitialize(
  _In_ PUNICODE_STRING RegistryPath
);
```
RegistryPath 是指向一个计数的 Unicode 字符串，指定 DLL 的注册表项的路径**HKEY_LOCAL_MACHINE\CurrentControlSet\Services\DllName**。 DLL 例程可以使用此密钥来存储特定于 DLL 的信息。 一次释放由 RegistryPath 指向的缓冲区**DllInitialize**退出。 因此，如果 DLL 使用的密钥**DllInitialize**必须重复的键的名称。 


生成过程生成一个扩展名为.lib 的导出库和.sys 扩展名为导出驱动程序。

### <a name="importing-functions-from-an-export-driver"></a>从导出驱动程序导入函数

若要导入导出驱动程序导出的函数，应声明函数使用 DECLSPEC\_导入宏，Ntdef.h 中定义。 例如：

```cpp
DECLSPEC_IMPORT int LoadPrinterDriver (int arg1); 
```

此宏解析为 **\_ \_declspec**(dllimport) 存储类声明这些平台上的，在需要和为这些平台上执行任何操作在不需要。

在导出驱动程序，应使用 DECLSPEC 声明要导出的函数\_导出宏。 此宏解析为 **\_ \_declspec**(dllexport) 存储类声明这些平台上的，在需要和为这些平台上执行任何操作在不需要。 如果导出驱动程序提供标准的驱动程序的调度例程，该例程没有要导出。

### <a name="loading-and-unloading-an-export-driver"></a>加载和卸载导出驱动程序

导出驱动程序必须安装在 %windir%\\System32\\驱动程序目录。 操作系统从 Windows 2000 开始，将保留引用计数，该值指示的其他驱动程序导入导出驱动程序的函数的次数。 系统递减只要其中一个导入驱动程序将卸载此计数。 如果引用计数降为零，系统中卸载导出驱动程序。 但是，导出驱动程序必须包含标准的入口点，并且卸载例程**DllInitialize**并**DllUnload**，或操作系统将不会激活此引用计数机制。

卸载 DLL 时，系统将调用内核模式 DLL 的 DllUnload 例程。

```cpp
NTSTATUS DllUnload(void);
```
导出驱动程序必须提供的 DllUnload 例程。 可用的 DllUnload 例程来释放例程在 DLL 中使用的任何资源。 








