---
title: 示例11启用页堆验证
description: 示例11启用页堆验证
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 13488b9142dbfcf98e4a732303c974a28106b25b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840837"
---
# <a name="example-11-enabling-page-heap-verification"></a>示例11：启用页堆验证


## <span id="ddk_example_11___enabling_page_heap_verification_dtools"></span><span id="DDK_EXAMPLE_11___ENABLING_PAGE_HEAP_VERIFICATION_DTOOLS"></span>


以下命令为 myapp.exe （一种虚构程序）启用完整和标准页堆验证。

第一个命令对 myapp.exe 启用 *标准* 页堆验证。 它使用 **/p** 参数启用进程的页堆。 默认情况下， **/p** 启用标准页堆。

```console
gflags /p /enable myapp.exe 
```

以下命令启用对 myapp.exe 程序的 *完整* 页面堆验证。 尽管这些命令会在注册表中创建不同的设置，但它们在功能上等效于 "**全局标志**" 对话框中 myapp.exe 映像文件的 "**启用页堆**" 复选框。 这些方法可互换使用。

```console
gflags /p /enable myapp.exe /full
gflags /i myapp.exe +hpa
gflags /i myapp.exe +02000000
```

以下命令禁用 myapp.exe 程序的完整或标准页堆验证，而不考虑用于启用页堆验证的命令或对话框方法。

```console
gflags /p /disable myapp.exe
gflags /i myapp.exe -hpa
gflags /i myapp.exe -02000000
```

**注意**   使用 **/debug** 或 **/kdebug** 参数时，请使用 **/p/disable** 参数关闭页堆验证， (不) 的 **/i-hpa** 参数。 **/P/disable** 参数禁用页堆验证并删除调试器读取的注册表项。

 

 

 





