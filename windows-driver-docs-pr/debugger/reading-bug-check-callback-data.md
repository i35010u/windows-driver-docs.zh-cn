---
title: 读取 Bug 检查回调数据
description: 读取 Bug 检查回调数据
ms.assetid: 638074bb-5133-4edc-86c5-33aafa837a0c
keywords:
- 错误检查的执行的回调数据
- 为了进行错误检查，显示回调数据的回调数据
- 为了进行错误检查，显示辅助的数据的回调数据
- 辅助 bug 检查回调数据
- 错误检查，回调例程
- dbgeng.h 标头文件 IDebugDataSpaces3
- dbgeng.h 标头文件 ReadTagged
- dbgeng.h 标头文件 StartEnumTagged
- dbgeng.h 标头文件 GetNextTagged
ms.date: 10/25/2018
ms.localizationpriority: medium
ms.openlocfilehash: abef0e9bf286e913af4f77c979e05db2bff24796
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534580"
---
# <a name="reading-bug-check-callback-data"></a>读取 Bug 检查回调数据


许多驱动程序提供*bug 检查回调例程*。 当 Windows 发出的 bug 检查时，它调用这些例程之前关闭系统。 这些例程可以指定和写入的内存称为领域*回调数据*并*辅助回调数据*。

<span id="BugCheckCallback"></span><span id="bugcheckcallback"></span><span id="BUGCHECKCALLBACK"></span>[BugCheckCallback](https://go.microsoft.com/fwlink/p/?LinkID=254479)  
此例程所写入数据变得回调数据的一部分。 数据不包括故障转储文件中。 

<span id="BugCheckSecondaryDumpDataCallback"></span><span id="bugchecksecondarydumpdatacallback"></span><span id="BUGCHECKSECONDARYDUMPDATACALLBACK"></span>[BugCheckSecondaryDumpDataCallback](https://go.microsoft.com/fwlink/p/?LinkID=254481)  
此例程所写入数据将成为辅助回调数据的一部分。 崩溃转储文件中包含数据。

<span id="BugCheckAddPagesCallback"></span><span id="bugcheckaddpagescallback"></span><span id="BUGCHECKADDPAGESCALLBACK"></span>[BugCheckAddPagesCallback](https://go.microsoft.com/fwlink/p/?LinkID=254480)  
此例程所指定的页成为回调数据的一部分。 在这些网页中的数据包含在崩溃转储文件中。

回调和可供调试器辅助回调数据的数量取决于几个因素：

-   如果您正在执行的已崩溃系统，已通过写入的回调数据的实时调试[BugCheckCallback](https://go.microsoft.com/fwlink/p/?LinkID=254479)或者指定[BugCheckAddPagesCallback](https://go.microsoft.com/fwlink/p/?LinkID=254480)将可用。 辅助回调数据将不能，因为它不存储在任何固定的内存位置。

-   如果你正在调试的完整内存转储或内核内存转储，通过指定回调数据[BugCheckAddPagesCallback](https://go.microsoft.com/fwlink/p/?LinkID=254480)和写入辅助回调数据[BugCheckSecondaryDumpDataCallback](https://go.microsoft.com/fwlink/p/?LinkID=254481)将可用。 所写入的回调数据[BugCheckCallback](https://go.microsoft.com/fwlink/p/?LinkID=254479)将不可用。 

-   如果你正在调试小型内存转储，回调数据将不可用。 辅助回调数据将可用。

请参阅[内核模式转储文件的种类](varieties-of-kernel-mode-dump-files.md)有关这些不同的转储文件大小的详细信息。


## <span id="ddk_reading_bug_check_callback_data_dbg"></span><span id="DDK_READING_BUG_CHECK_CALLBACK_DATA_DBG"></span>


### <a name="span-iddisplaying-callback-dataspanspan-iddisplaying-callback-dataspandisplaying-callback-data"></a><span id="displaying-callback-data"></span><span id="DISPLAYING-CALLBACK-DATA"></span>显示回调数据

若要显示 bug 检查回调数据，可以使用[ **！ bugdump** ](-bugdump.md)扩展。

不带任何参数， [ **！ bugdump** ](-bugdump.md)将显示所有的回调数据。

若要查看一个特定的回调例程的数据，请使用[ **！ bugdump**](-bugdump.md)*组件*，其中*组件*是相同的参数传递给**KeRegisterBugCheckCallback**注册该例程时。

### <a name="span-iddisplaying-secondary-callback-dataspanspan-iddisplaying-secondary-callback-dataspandisplaying-secondary-callback-data"></a><span id="displaying-secondary-callback-data"></span><span id="DISPLAYING-SECONDARY-CALLBACK-DATA"></span>显示辅助回调数据

有两种方法来显示辅助回调数据。 可以使用 **.enumtag**命令也可以编写自己的调试器扩展。

辅助回调数据的每个块由 GUID 标记标识。 指定此标记**Guid**字段 **(KBUGCHECK\_辅助\_转储\_数据) ReasonSpecificData**参数传递给[BugCheckSecondaryDumpDataCallback](https://go.microsoft.com/fwlink/p/?LinkID=254481)。

[ **.Enumtag （枚举辅助回调数据）** ](-enumtag--enumerate-secondary-callback-data-.md)命令不是非常精确的检测。 它将显示每个辅助数据块，显示标记，然后以十六进制和 ASCII 格式显示数据。 它是通常只可用于确定哪些标记实际上正在使用辅助数据块。

若要更实用的方式使用此数据，建议您编写自己的调试器扩展。 此扩展方法必须调用 dbgeng.h 标头文件中。 有关详细信息，请参阅[写入新的调试器扩展](writing-new-debugger-extensions.md)。

如果您知道辅助的数据块的 GUID 标记，你的扩展应使用的方法**IDebugDataSpaces3::ReadTagged**来访问数据。 其原型如下所示：

```cpp
STDMETHOD(ReadTagged)(
    THIS_
    IN LPGUID Tag,
    IN ULONG Offset,
    OUT OPTIONAL PVOID Buffer,
    IN ULONG BufferSize,
    OUT OPTIONAL PULONG TotalSize
    ) PURE; 
```

下面是如何使用此方法的示例：

```cpp
UCHAR RawData[MY_DATA_SIZE];
GUID MyGuid = .... ;

Success = DataSpaces->ReadTagged(  &MyGuid,  0,  RawData,
                                   sizeof(RawData),  NULL); 
```

如果你提供*BufferSize*太小，这就是**ReadTagged**将成功，但将编写仅请求的字节数*缓冲区*。 如果指定*BufferSize*太大**ReadTagged**将会成功，但将写入到实际的块大小*缓冲区*。 如果提供的指针*TotalSize*， **ReadTagged**将使用它返回实际的块的大小。 如果不能访问块， **ReadTagged**将返回了失败状态代码。

如果两个块具有相同 GUID 标记，将返回第一个匹配块，并且第二个块将不可访问。

如果您不能确定你的块的 GUID 标记，则可以使用**IDebugDataSpaces3::StartEnumTagged**， **IDebugDataSpaces3::GetNextTagged**，和**IDebugDataSpaces3::EndEnumTagged**方法来枚举标记的块。 其原型如下所示：

```cpp
STDMETHOD(StartEnumTagged)(
    THIS_
    OUT PULONG64 Handle
    ) PURE;

STDMETHOD(GetNextTagged)(
    THIS_
    IN ULONG64 Handle,
    OUT LPGUID Tag,
    OUT PULONG Size
    ) PURE;

STDMETHOD(EndEnumTagged)(
    THIS_
    IN ULONG64 Handle
    ) PURE; 
```

### <a name="span-iddebugging-callback-routinesspanspan-iddebugging-callback-routinesspandebugging-callback-routines"></a><span id="debugging-callback-routines"></span><span id="DEBUGGING-CALLBACK-ROUTINES"></span>调试回调例程

还有可能要调试的回调例程本身。 就像任何其他断点一样工作回调例程中的断点。

如果回调例程导致第二个错误检查，将首先处理此新的 bug 检查。 但是，Windows 将不会重复停止进程的某些部分 — 例如，它不会写入的第二个崩溃转储文件。 蓝色屏幕上显示的停止代码将第二个错误检查代码。 如果附加内核调试程序，通常会显示有关这两个错误检查的消息。

 

 





