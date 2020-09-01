---
title: 读取 Bug 检查回调数据
description: 读取 Bug 检查回调数据
ms.assetid: 638074bb-5133-4edc-86c5-33aafa837a0c
keywords:
- bug 检查的回调数据
- bug 检查的回调数据，显示回调数据
- bug 检查的回调数据，显示辅助数据
- 辅助 bug 检查回调数据
- bug 检查，回调例程
- dbgeng 头文件，IDebugDataSpaces3
- dbgeng 头文件，ReadTagged
- dbgeng 头文件，StartEnumTagged
- dbgeng 头文件，GetNextTagged
ms.date: 06/05/2020
ms.localizationpriority: medium
ms.openlocfilehash: a03eb8ca32e0ff306548094642151878225d41cf
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206803"
---
# <a name="reading-bug-check-callback-data"></a>读取 Bug 检查回调数据

许多驱动程序提供 *bug 检查回调例程*。 当 Windows 发出 bug 检查时，它将在关闭系统之前调用这些例程。 这些例程可以指定并写入到称为 *回调数据* 和 *辅助回调数据*的内存区域。

**BugCheckCallback** 使用 [KBUGCHECK_CALLBACK_ROUTINE](/windows-hardware/drivers/ddi/wdm/nc-wdm-kbugcheck_callback_routine)  
此例程写入的数据会成为 *回调数据*的一部分。 数据不包括在故障转储文件中。

**BugCheckSecondaryDumpDataCallback** 使用 [KBUGCHECK_REASON_CALLBACK_ROUTINE](/windows-hardware/drivers/ddi/wdm/nc-wdm-kbugcheck_reason_callback_routine)  
此例程写入的数据会成为 *辅助回调数据*的一部分。 数据包含在故障转储文件中。

**BugCheckAddPagesCallback** 使用 [KBUGCHECK_REASON_CALLBACK_ROUTINE](/windows-hardware/drivers/ddi/wdm/nc-wdm-kbugcheck_reason_callback_routine)  
此例程指定的页面将成为 *回调数据*的一部分。 这些页面中的数据包含在故障转储文件中。

调试器可用的回叫和辅助回叫数据量取决于多个因素：

- 如果要对崩溃的系统执行实时调试，则已由 [BugCheckCallback](/windows-hardware/drivers/ddi/wdm/nc-wdm-kbugcheck_callback_routine) 写入或由 [BugCheckAddPagesCallback](/windows-hardware/drivers/ddi/wdm/nc-wdm-kbugcheck_reason_callback_routine) 指定的回调数据将可用。 辅助回叫数据将不可用，因为它不存储在任何固定的内存位置。

- 如果调试的是完整内存转储或内核内存转储，则由 [BugCheckAddPagesCallback](/windows-hardware/drivers/ddi/wdm/nc-wdm-kbugcheck_reason_callback_routine) 指定的回叫 [数据将可用](/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kbugcheck_reason_callback_routine) 。 [BugCheckCallback](/windows-hardware/drivers/ddi/wdm/nc-wdm-kbugcheck_callback_routine)写入的回叫数据将不可用。

- 如果调试的是小内存转储，则回调数据将不可用。 辅助回调数据将可用。

有关这些不同转储文件大小的详细信息，请参阅 [内核模式转储文件的种类](varieties-of-kernel-mode-dump-files.md) 。

## <a name="displaying-callback-data"></a>显示回调数据

若要显示 bug 检查回调数据，可以使用 [**！ bugdump**](-bugdump.md) 扩展名。

如果没有任何参数， [**！ bugdump**](-bugdump.md) 将显示所有回调的数据。

若要查看某个特定回调例程的数据，请使用 [**！ bugdump**](-bugdump.md)*Component*，其中 *组件* 是在注册该例程时传递到 **KeRegisterBugCheckCallback** 的相同参数。

### <a name="displaying-secondary-callback-data"></a>显示辅助回调数据

可以通过两种方法来显示辅助回叫数据。 可以使用 **enumtag** 命令，也可以编写自己的调试器扩展。

每个辅助回调数据块由 GUID 标记标识。 此标记由传递给[BugCheckSecondaryDumpDataCallback](/windows-hardware/drivers/ddi/wdm/nc-wdm-kbugcheck_reason_callback_routine) **) REASONSPECIFICDATA 参数 (KBUGCHECK \_ 辅助 \_ 转储 \_ 数据**的**Guid**字段指定。

[**Enumtag (枚举辅助回调数据) **](-enumtag--enumerate-secondary-callback-data-.md)命令不是非常精确的检测。 它显示每个辅助数据块，显示标记，然后以十六进制和 ASCII 格式显示数据。 通常，它仅用于确定哪些标记实际上用于辅助数据块。

若要以更实用的方式使用此数据，建议编写自己的调试器扩展。 此扩展必须调用 dbgeng 标头文件中的方法。 有关详细信息，请参阅 [编写新调试器扩展](writing-new-debugger-extensions.md)。

如果知道辅助数据块的 GUID 标记，扩展应使用方法 **IDebugDataSpaces3：： ReadTagged** 来访问数据。 其原型如下所示：

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

如果提供的 *BufferSize* 太小， **ReadTagged** 将会成功，但只会将请求的字节数写入 *缓冲区*。 如果指定的 *BufferSize* 太大， **ReadTagged** 将会成功，但只会将实际块大小写入 *缓冲区*。 如果为 *TotalSize*提供指针，则 **ReadTagged** 将使用它来返回实际块的大小。 如果块无法访问， **ReadTagged** 将返回失败状态代码。

如果两个块具有相同的 GUID 标记，则将返回第一个匹配块，并将无法访问第二个块。

如果不确定块的 GUID 标记，可以使用 **IDebugDataSpaces3：： StartEnumTagged**、 **IDebugDataSpaces3：： GetNextTagged**和 **IDebugDataSpaces3：： EndEnumTagged** 方法来枚举标记的块。 它们的原型如下所示：

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

### <a name="debugging-callback-routines"></a>调试回调例程

还可以调试回调例程本身。 回调例程内的断点的工作方式与任何其他断点相同。

如果回调例程导致第二个 bug 检查，则将首先处理此新的 bug 检查。 但是，Windows 不会重复停止进程的某些部分，例如，它不会写入第二个故障转储文件。 蓝屏上显示的停止代码将是第二个 bug 检查代码。 如果附加了内核调试程序，则通常会出现有关这两个 bug 检查的消息。