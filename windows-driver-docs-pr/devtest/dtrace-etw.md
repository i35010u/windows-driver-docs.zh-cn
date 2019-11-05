---
title: DTrace ETW
description: DTrace 使用 D 编程语言支持 Windows 事件跟踪（ETW）。
ms.assetid: abf23d76-423d-4d1e-afde-83739015bbf1
keywords:
- DTrace WDK
- 软件跟踪 WDK，DTrace
- 显示跟踪消息
- 格式化跟踪消息 WDK DTrace
- 跟踪消息格式 WDK DTrace
- 软件跟踪 WDK，设置消息格式
- 跟踪 WDK，DTrace
- 跟踪消息格式化文件 WDK
ms.date: 11/04/2019
ms.localizationpriority: medium
ms.openlocfilehash: 5e9fbbac12d49e2ee4657689398ef67d938973d9
ms.sourcegitcommit: 5081de283b09b4fe847912fc1dc0e7f057e0a0cd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2019
ms.locfileid: "73592432"
---
# <a name="dtrace-etw"></a>DTrace ETW

使用适用于 Windows 的 DTrace 处理现有的 ETW 事件并添加新的 ETW 事件。

Windows 事件跟踪（ETW）是一个内核级别的跟踪功能，可让你将内核或应用程序定义的事件记录到日志文件中。 你可以实时使用事件或从日志文件中使用事件，并使用它们来调试应用程序，或确定应用程序中出现性能问题的位置。 有关 ETW 的一般信息，请参阅[关于事件跟踪](https://docs.microsoft.com/windows/win32/etw/about-event-tracing)。

> [!NOTE]
> 版本18980和 Windows Server 有问必答 Preview 版本18975后，Windows 内部版本支持 DTrace。

有关在 Windows 上使用 DTrace 的常规信息，请参阅[dtrace](dtrace.md)。

## <a name="etw-windows-dtrace-provider"></a>ETW Windows DTrace 提供程序

您可以使用 DTrace 来捕获和报告跟踪日志记录和基于清单的 ETW 事件。 若要探测特定关键字/级别/应对警报，如果不使用通配符，ETW 探测将更可靠地工作。 请根据以下规则完全指定探测：  

Probename = etw

Modname = 以 xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx 形式使用所有小写字符的提供程序 guid。

Funcname = Level_Keyword 形式的0x00_0x0000000000000000。 若要匹配所有内容，请将其设置为0xff_0xffffffffffffffff。

Probename = 整数事件 ID 或 "generic_event"，以匹配所有事件 Id。

基于 Probename 的筛选仅适用于所提供的事件。 对 tracelogged 事件使用通配符（*）。

ETW 有效负载通过 arg0 访问。 这由 nt\`\_事件\_标头后跟事件特定日期。

### <a name="determining-available-etw-providers"></a>确定可用的 ETW 提供程序

使用 logman 命令可显示活动 ETW 提供程序及其提供程序 Guid。

```dtrace
C:\>logman query providers
...
Microsoft-Windows-Kernel-Memory {D1D93EF7-E1F2-4F45-9943-03D245FE6C00}
Microsoft-Windows-Kernel-Network {7DD42A49-5329-4832-8DFD-43D979153A88}
Microsoft-Windows-Kernel-PnP {9C205A39-1250-487D-ABD7-E831C6290539}
Microsoft-Windows-Kernel-Power {331C3B3A-2005-44C2-AC5E-77220C37D6B4}
Microsoft-Windows-Kernel-Prefetch {5322D61A-9EFA-4BC3-A3F9-14BE95C144F8}
Microsoft-Windows-Kernel-Process {22FB2CD6-0E7B-422B-A0C7-2FAD1FD0E716}
...
```

## <a name="displaying-existing-etw-provider-information"></a>显示现有 ETW 提供程序信息

DTrace 能够输出 ETW 事件。 这对于现有 ETW 管道要报告、收集和分析的情况非常有用。

使用此示例 DTrace 命令报告 Microsoft Windows 内核内存提供程序事件。

```dtrace
C:\>dtrace -n "etw:d1d93ef7-e1f2-4f45-9943-03d245fe6c00:0xff_0xffffffffffffffff:12"
dtrace: description 'etw:d1d93ef7-e1f2-4f45-9943-03d245fe6c00:0xff_0xffffffffffffffff:12' matched 1 probe
CPU     ID                    FUNCTION:NAME
  0   3271       0xff_0xffffffffffffffff:12
  0   3271       0xff_0xffffffffffffffff:12
  0   3271       0xff_0xffffffffffffffff:12
  0   3271       0xff_0xffffffffffffffff:12
  0   3271       0xff_0xffffffffffffffff:12
  0   3271       0xff_0xffffffffffffffff:12
  0   3271       0xff_0xffffffffffffffff:12
  0   3271       0xff_0xffffffffffffffff:12
  0   3271       0xff_0xffffffffffffffff:12
  0   3271       0xff_0xffffffffffffffff:12
  0   3271       0xff_0xffffffffffffffff:12
```

## <a name="adding-new-etw-events"></a>添加新的 ETW 事件

可以通过调用 etw\_跟踪宏来创建 etw 跟踪事件。 仅当存在指定跟踪提供程序的活动侦听器时才记录事件，否则将跳过这些事件。

Etw\_trace 宏支持基本数据类型，如 int8、uint8、int16、uint16、int32、uint32、int64、uint64、hexint32、hexint64 和 string。 有关更多详细信息，请参阅下*支持的 ETW 数据类型*表格。

**示例 ETW\_跟踪宏：**

当 syscall 例程返回 0xc0000001-STATUS_UNSUCCESSFUL 时，此脚本会生成一个自定义 ETW 事件。

您可以更改 `this->status` 值，以使用不同的[NTSTATUS 值](https://docs.microsoft.com/openspecs/windows_protocols/ms-erref/596a1078-e883-4972-9bbc-49e60bebca55)记录不同的 syscall 返回值。

```dtrace
syscall:::return 
{ 
    this->status = (uint32_t) arg0;

    if (this->status == 0xc0000001UL) 
    { 
        etw_trace
        (
            "Tools.DTrace.Platform", /* Provider Name */
            "AAD330CC-4BB9-588A-B252-08276853AF02", /* Provider GUID */
            "My custom event from DTrace", /* Event Name */
            1, /* Event Level (0 - 5) */
            0x0000000000000020, /* Flag */
            "etw_int32", /* Field_1 Name */
            "PID",/* Field_1 Type */
            (int32_t)pid, /* Field_1 Value  */
            "etw_string", /* Field_2 Name */
            "Execname", /* Field_2 type */
            execname, /* Field_2 Value */
            "etw_string", /* Field_3 Name */
            "Probefunc", /* Field_3 type */
            probefunc /* Field_3 Value */   
            );
    }
}
```

```dtrace
C:\> dtrace -s addnewetwevent.d
dtrace: script 'addnewetwevent.d' matched 1881 probes
CPU     ID                    FUNCTION:NAME
  0     93 NtAlpcSendWaitReceivePort:return
  0     93 NtAlpcSendWaitReceivePort:return
  0     93 NtAlpcSendWaitReceivePort:return
```

## <a name="etw-numa-mem-stats-example-code"></a>ETW NUMA 内存统计示例代码

此示例脚本使用 Microsoft Windows 内核内存 ETW 提供程序来转储 NUMA 节点内存。 页面大小可转换为大小（KB），乘以4。 有关 NUMA 的一般信息，请参阅[Numa 支持](https://docs.microsoft.com/windows/win32/procthread/numa-support)。

此代码也位于 <https://github.com/microsoft/DTrace-on-Windows/blob/master/samples/windows/etw/numamemstats.d>

```dtrace
typedef struct KernelMemInfoEvent
{
        struct nt`_EVENT_HEADER _EH;
    uint32_t PartitionId;
    uint32_t Count;
    uint32_t NodeNumber;
}kmi;

typedef struct MemoryNodeInfo
{
    uint64_t TotalPageCount;
    uint64_t SmallFreePageCount;
    uint64_t SmallZeroPageCount;
    uint64_t MediumFreePageCount;
    uint64_t MediumZeroPageCount;
    uint64_t LargeFreePageCount;
    uint64_t LargeZeroPageCount;
    uint64_t HugeFreePageCount;
    uint64_t HugeZeroPageCount;
}m_nodeinfo;

int printcounter;

BEGIN
{
    printcounter = 0;
}

/* MemNodeInfo */
etw:d1d93ef7-e1f2-4f45-9943-03d245fe6c00:0xff_0xffffffffffffffff:12
{
    if (printcounter%10 == 0)
    {
        printf ("\n \n");
        printf("Partition ID: %d \n",((kmi *)arg0)->PartitionId);
        printf("Count: %d \n", ((kmi *)arg0)->Count);
        
        printf("Node number: %d\n", ((kmi *)arg0)->NodeNumber);
        counters = (m_nodeinfo*)(arg0 + sizeof(struct nt`_EVENT_HEADER) + 12);
        print(*counters);

        /* Dump rest of the NUMA node info */

        if (((kmi *)arg0)->Count > 1)
        {
            nodenumber = (uint32_t *) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(1)) + (sizeof(uint32_t)*(1)) );
            printf ("Node Number: %d \n", *nodenumber);
            counters = (m_nodeinfo*) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(1)) + (sizeof(uint32_t)*(1)) + sizeof(uint32_t));
            print(*counters);
        }
        if (((kmi *)arg0)->Count > 2)
        {
            nodenumber = (uint32_t *) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(2)) + (sizeof(uint32_t)*(2)) );
            printf ("Node Number: %d \n", *nodenumber);
            counters = (m_nodeinfo*) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(2)) + (sizeof(uint32_t)*(2)) + sizeof(uint32_t));
            print(*counters);
        }
        if (((kmi *)arg0)->Count > 3)
        {
            nodenumber = (uint32_t *) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(3)) + (sizeof(uint32_t)*(3)) );
            printf ("Node Number: %d \n", *nodenumber);
            counters = (m_nodeinfo*) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(3)) + (sizeof(uint32_t)*(3)) + sizeof(uint32_t));
            print(*counters);
        }
        if (((kmi *)arg0)->Count > 4)
        {
            nodenumber = (uint32_t *) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(4)) + (sizeof(uint32_t)*(4)) );
            printf ("Node Number: %d \n", *nodenumber);
            counters = (m_nodeinfo*) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(4)) + (sizeof(uint32_t)*(4)) + sizeof(uint32_t));
            print(*counters);
        }
        if (((kmi *)arg0)->Count > 5)
        {
            nodenumber = (uint32_t *) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(5)) + (sizeof(uint32_t)*(5)) );
            printf ("Node Number: %d \n", *nodenumber);
            counters = (m_nodeinfo*) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(5)) + (sizeof(uint32_t)*(5)) + sizeof(uint32_t));
            print(*counters);
        }
        if (((kmi *)arg0)->Count > 6)
        {
            nodenumber = (uint32_t *) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(6)) + (sizeof(uint32_t)*(6)) );
            printf ("Node Number: %d \n", *nodenumber);
            counters = (m_nodeinfo*) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(6)) + (sizeof(uint32_t)*(6)) + sizeof(uint32_t));
            print(*counters);
        }
        if (((kmi *)arg0)->Count > 7)
        {
            nodenumber = (uint32_t *) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(7)) + (sizeof(uint32_t)*(7)) );
            printf ("Node Number: %d \n", *nodenumber);
            counters = (m_nodeinfo*) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(7)) + (sizeof(uint32_t)*(7)) + sizeof(uint32_t));
            print(*counters);
        }
        if (((kmi *)arg0)->Count > 8)
        {
            nodenumber = (uint32_t *) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(8)) + (sizeof(uint32_t)*(8)) );
            printf ("Node Number: %d \n", *nodenumber);
            counters = (m_nodeinfo*) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(8)) + (sizeof(uint32_t)*(8)) + sizeof(uint32_t));
            print(*counters);
        }
        if (((kmi *)arg0)->Count > 9)
        {
            nodenumber = (uint32_t *) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(9)) + (sizeof(uint32_t)*(9)) );
            printf ("Node Number: %d \n", *nodenumber);
            counters = (m_nodeinfo*) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(9)) + (sizeof(uint32_t)*(9)) + sizeof(uint32_t));
            print(*counters);
        }
        if (((kmi *)arg0)->Count > 10)
        {
            nodenumber = (uint32_t *) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(10)) + (sizeof(uint32_t)*(10)) );
            printf ("Node Number: %d \n", *nodenumber);
            counters = (m_nodeinfo*) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(10)) + (sizeof(uint32_t)*(10)) + sizeof(uint32_t));
            print(*counters);
        }
        if (((kmi *)arg0)->Count > 11)
        {
            nodenumber = (uint32_t *) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(11)) + (sizeof(uint32_t)*(11)) );
            printf ("Node Number: %d \n", *nodenumber);
            counters = (m_nodeinfo*) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(11)) + (sizeof(uint32_t)*(11)) + sizeof(uint32_t));
            print(*counters);
        }
        if (((kmi *)arg0)->Count > 12)
        {
            nodenumber = (uint32_t *) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(12)) + (sizeof(uint32_t)*(12)) );
            printf ("Node Number: %d \n", *nodenumber);
            counters = (m_nodeinfo*) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(12)) + (sizeof(uint32_t)*(12)) + sizeof(uint32_t));
            print(*counters);
        }
        if (((kmi *)arg0)->Count > 13)
        {
            nodenumber = (uint32_t *) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(13)) + (sizeof(uint32_t)*(13)) );
            printf ("Node Number: %d \n", *nodenumber);
            counters = (m_nodeinfo*) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(13)) + (sizeof(uint32_t)*(13)) + sizeof(uint32_t));
            print(*counters);
        }
        if (((kmi *)arg0)->Count > 14)
        {
            nodenumber = (uint32_t *) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(14)) + (sizeof(uint32_t)*(14)) );
            printf ("Node Number: %d \n", *nodenumber);
            counters = (m_nodeinfo*) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(14)) + (sizeof(uint32_t)*(14)) + sizeof(uint32_t));
            print(*counters);
        }
        if (((kmi *)arg0)->Count > 15)
        {
            nodenumber = (uint32_t *) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(15)) + (sizeof(uint32_t)*(15)) );
            printf ("Node Number: %d \n", *nodenumber);
            counters = (m_nodeinfo*) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(15)) + (sizeof(uint32_t)*(15)) + sizeof(uint32_t));
            print(*counters);
        }

    }
    exit(1);
    printcounter++;
}
```

将该文件另存为 etwnumamemstats。 d

以管理员身份打开命令提示符，并使用-s 选项运行脚本。 

在客户端 Windows 电脑上运行时，将显示单个 NUMA 节点。

```dtrace
C:\> dtrace -s etwnumamemstats.d 
trace: script 'etwnumamemstats.d' matched 36 probes
CPU     ID                    FUNCTION:NAME
  0  42735       0xff_0xffffffffffffffff:12

Partition ID: 0
Count: 1
Node number: 1
m_nodeinfo {
    uint64_t TotalPageCount = 0xab98d
    uint64_t SmallFreePageCount = 0
    uint64_t SmallZeroPageCount = 0x1bec
    uint64_t MediumFreePageCount = 0
    uint64_t MediumZeroPageCount = 0x5a
    uint64_t LargeFreePageCount = 0
    uint64_t LargeZeroPageCount = 0
    uint64_t HugeFreePageCount = 0
    uint64_t HugeZeroPageCount = 0
}
  0  42735       0xff_0xffffffffffffffff:12
```

## <a name="supported-etw-data-types"></a>支持的 ETW 数据类型

| **ETW 类型**           | **D 语言数据类型** | **注意**                                                                                 |
| ---------------------- | ------------------------ | ----------------------------------------------------------------------------------------- |
| etw\_结构            | 整型                  | 此类型的负载值表示新结构将具有的成员的计数。  |
| etw\_字符串            | 字符串                   | N/A                                                                                       |
| etw\_mbcsstring        | 字符串                   | N/A                                                                                       |
| etw\_int8              | 整型                  | 建议键入大小，并强制转换为 D 脚本中 \`int8\_t\`             |
| etw\_uint8             | 整型                  | 建议将类型大小匹配，并强制转换为 D 脚本中 \`uint8\_t\`            |
| etw\_int16             | 整型                  | 建议键入大小，并强制转换为 D 脚本中 \`int16\_t\`            |
| etw\_uint16            | 整型                  | 建议将类型大小匹配，并强制转换为 D 脚本中的 \`uint16\_t\`           |
| etw\_int32             | 整型                  | N/A                                                                                       |
| etw\_uint32            | 整型                  | N/A                                                                                       |
| etw\_int64             | 整型                  | 类型必须显式 \`int64\_t\`，因为 D 默认为 \`int32\_t\`                  |
| etw\_uint64            | 整型                  | 类型必须显式 \`int64\_t\`，因为 D 默认为 \`int32\_t\`                  |
| etw\_float             | Scalar                   | D 脚本中不允许使用浮点常量，但在加载的符号上允许它 |
| etw\_双精度            | Scalar                   | D 脚本中不允许使用浮点常量，但在加载的符号上允许它 |
| etw\_bool32            | 整型                  | N/A                                                                                       |
| etw\_hexint32          | 整型                  | N/A                                                                                       |
| etw\_hexint64          | 整型                  | 类型必须显式 \`int64\_t\`，因为 D 默认为 \`int32\_t\`                  |
| etw\_countedmbcsstring | 整型                  | N/A                                                                                       |
| etw\_intptr            | 整型                  | 数据类型大小根据体系结构而变化（\`int32\_t\` 与 \`int64\_t\`）   |
| etw\_uintptr           | 整型                  | 数据类型大小根据体系结构而变化（\`int32\_t\` 与 \`int64\_t\`）   |
| etw\_指针           | 整型                  | 数据类型大小根据体系结构而变化（\`int32\_t\` 与 \`int64\_t\`）   |
| etw\_char16            | 整型                  | 建议键入大小，并强制转换为 D 脚本中 \`int16\_t\`            |
| etw\_char8             | 整型                  | 建议键入大小，并强制转换为 D 脚本中 \`int8\_t\`             |
| etw\_bool8             | 整型                  | 建议键入大小，并强制转换为 D 脚本中 \`int8\_t\`             |
| etw\_hexint8           | 整型                  | 建议键入大小，并强制转换为 D 脚本中 \`int8\_t\`             |
| etw\_hexint16          | 整型                  | 建议键入大小，并强制转换为 D 脚本中 \`int16\_t\`            |
| etw\_pid               | 整型                  | N/A                                                                                       |
| etw\_tid               | 整型                  | N/A                                                                                       |
| etw\_mbcsxml           | 整型                  | N/A                                                                                       |
| etw\_mbcsjson          | 整型                  | N/A                                                                                       |
| etw\_countedmbcsxml    | 整型                  | N/A                                                                                       |
| etw\_countedmbcsjson   | 整型                  | N/A                                                                                       |
| etw\_win32error        | 整型                  | N/A                                                                                       |
| etw\_ntstatus          | 整型                  | N/A                                                                                       |
| etw\_hresult           | 整型                  | N/A                                                                                       |

## <a name="see-also"></a>另请参阅

[Windows 上的 DTrace](dtrace.md)

[DTrace Windows 编程](dtrace-programming.md)

[DTrace Windows 代码示例](dtrace-code-samples.md)

[DTrace 实时转储](dtrace-live-dump.md)
