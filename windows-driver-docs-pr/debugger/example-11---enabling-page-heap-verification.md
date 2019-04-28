---
title: 示例 11 启用页面堆验证
description: 示例 11 启用页面堆验证
ms.assetid: 5d0303a9-29f7-4759-ae7b-ad670eaee0ee
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: fbcf00019ca2620cb3883d868e90a72830207bef
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347819"
---
# <a name="example-11-enabling-page-heap-verification"></a>示例 11：启用页堆验证


## <span id="ddk_example_11___enabling_page_heap_verification_dtools"></span><span id="DDK_EXAMPLE_11___ENABLING_PAGE_HEAP_VERIFICATION_DTOOLS"></span>


以下命令启用为 myapp.exe，虚构程序完全和标准页面堆验证。

第一个命令启用*标准*页上为 myapp.exe 的堆验证。 它使用 **/p**参数，以便能够为进程页堆。 默认情况下 **/p**启用标准页面堆。

```console
gflags /p /enable myapp.exe 
```

以下命令启用*完整*页 myapp.exe 程序堆验证。 尽管这些命令在注册表中创建不同的设置，但它们是所有功能上等效于选择**启用页堆**myapp.exe 图像文件中的复选框**全局标志**对话框。 这些方法可以互换使用。

```console
gflags /p /enable myapp.exe /full
gflags /i myapp.exe +hpa
gflags /i myapp.exe +02000000
```

以下命令禁用 myapp.exe 程序，而不考虑用来启用页面堆验证的命令或对话框框中方法的完整或标准页堆验证。

```console
gflags /p /disable myapp.exe
gflags /i myapp.exe -hpa
gflags /i myapp.exe -02000000
```

**请注意**  使用时 **/debug**或 **/kdebug**参数，使用 **/p /disable**参数来关闭页面堆验证 （非 **/i hpa**参数)。 **/P /disable**参数禁用页堆验证和删除调试器读取的注册表项。

 

 

 





