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
ms.date: 10/14/2019
ms.localizationpriority: medium
ms.openlocfilehash: 78652fa0f3ccf232c4ecbd134a1ae4e741594d93
ms.sourcegitcommit: a59b63e84e6790af4c17b232f11a2f50f875c97a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/03/2020
ms.locfileid: "87527845"
---
# <a name="creating-export-drivers"></a>创建导出驱动程序



导出驱动程序是一种内核模式 DLL，它可以由各种特定于硬件或设备堆栈的其他组件加载，但不具有完整的内核模式驱动程序的某些特征。

具体而言，导出驱动程序没有调度表，它在驱动程序堆栈中没有位置，并且服务控制管理器的数据库中不存在将其定义为系统服务的条目。

尽管导出驱动程序没有调度表，但它可以向标准驱动程序提供调度例程。 标准驱动程序将调度例程插入其自己的调度表中。

导出驱动程序具有永远不会调用的存根[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)例程。

内核模式导出驱动程序特别适用于实现与基础堆栈和硬件特征无关的驱动程序对部分。

Windows 包含多个导出驱动程序。 例如，SCSI 端口驱动程序、磁带类驱动程序、IDE 控制器驱动程序都是由其他驱动程序加载的系统提供的导出驱动程序。

标准驱动程序还可以充当导出驱动程序。 若要使驱动程序以这两种方式运行，必须将其构建为导出驱动程序并作为常规驱动程序加载。

### <a name="building-an-export-driver"></a>构建导出驱动程序

若要在 Visual Studio 中创建导出驱动程序，请使用以下过程：

1. 通过模板创建新项目，例如**空的 WDM 驱动程序**。
2. 在 "项目设置" 中，将 "**常规-> 配置类型**" 设置为 "**动态库（.dll）**"。
3. 设置**链接器-> 高级-> 无入口点**设置为 **"是（/NOENTRY）"**。
4. 将模块定义文件添加到项目，例如：
  ```
  LIBRARY mydriver
  EXPORTS
    DllInitialize PRIVATE
    DllUnload PRIVATE
  ```

内核模式 DLL 的入口点始终为**DllInitialize**。 加载 DLL 后，系统立即调用内核模式 DLL 的 DllInitialize 例程。 导出驱动程序必须提供**DllInitialize**例程。 可以使用**DllInitialize**例程获取或初始化 DLL 中其他例程所需的资源。 

不能使用**DLLENTRY**宏指定入口点。 

```cpp
NTSTATUS DllInitialize(
  _In_ PUNICODE_STRING RegistryPath
);
```
RegistryPath 是一个指向指定了 DLL 的注册表项路径（ **HKEY_LOCAL_MACHINE \currentcontrolset\services\dllname**）的计数 Unicode 字符串的指针。 DLL 例程可以使用此密钥来存储特定于 DLL 的信息。 **DllInitialize**退出后，RegistryPath 所指向的缓冲区将被释放。 因此，如果 DLL 使用该密钥，则**DllInitialize**必须复制该密钥名称。 


生成过程将生成一个扩展名为 .lib 的导出库，并生成一个扩展名为 .sys 的导出驱动程序。

### <a name="importing-functions-from-an-export-driver"></a>从导出驱动程序导入函数

若要导入导出驱动程序导出的函数，应使用 \_ Ntdef 中定义的 DECLSPEC 导入宏来声明函数。 例如：

```cpp
DECLSPEC_IMPORT int LoadPrinterDriver (int arg1); 
```

此宏可在需要时将这些平台上的** \_ \_ declspec**（dllimport）存储类声明解析为无需的平台。

在导出驱动程序中，应通过 DECLSPEC 导出宏声明要导出的函数 \_ 。 如果需要，此宏可在这些平台上将** \_ \_ declspec**（dllexport）存储类声明解析为无需的平台。 如果导出驱动程序为标准驱动程序提供了调度例程，则不需要导出该例程。

### <a name="loading-and-unloading-an-export-driver"></a>加载和卸载导出驱动程序

导出驱动程序必须安装在% Windir% \\ System32 \\ 驱动程序目录中。 从 Windows 2000 开始，操作系统会保留一个引用计数，指示其他驱动程序导入了导出驱动程序的函数的次数。 当卸载其中一个导入驱动程序时，系统会减少此计数。 当引用计数降为零时，系统卸载导出驱动程序。 但是，导出驱动程序必须包含标准入口点和卸载例程、 **DllInitialize**和**DllUnload**，或者操作系统不会激活此引用计数机制。

当系统卸载 DLL 时，系统会调用内核模式 DLL 的 DllUnload 例程。

```cpp
NTSTATUS DllUnload(void);
```
导出驱动程序必须提供 DllUnload 例程。 您可以使用 DllUnload 例程来释放由 DLL 中的例程使用的所有资源。 








