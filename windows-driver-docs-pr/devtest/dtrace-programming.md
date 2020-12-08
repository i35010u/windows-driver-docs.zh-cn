---
title: DTrace 编程
description: DTrace 支持 D 编程语言。 本主题提供了 D 代码示例。
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
ms.openlocfilehash: 1e1887a12766f7bf2816d9c59f1c10ceda28fb47
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817797"
---
# <a name="dtrace-programming"></a>DTrace 编程

DTrace 支持 D 编程语言。 本主题介绍如何开始编写和使用 DTrace 脚本。

有关 Windows 上的 DTrace 的一般信息，请参阅 [dtrace](dtrace.md)。

有关 DTrace 的详细信息，请参阅剑桥大学的 [OpenDTrace 规范1.0 版](https://www.cl.cam.ac.uk/techreports/UCAM-CL-TR-924.pdf) 。

> [!NOTE]
> 版本18980和 Windows Server 有问必答 Preview 版本18975后，Windows 内部版本支持 DTrace。

## <a name="additional-sample-scripts"></a>其他示例脚本

DTrace 源代码的示例目录中提供了适用于 Windows 方案的其他 D 脚本。

[https://github.com/microsoft/DTrace-on-Windows/tree/master/samples/windows](https://github.com/microsoft/DTrace-on-Windows/tree/master/samples/windows)

中提供了一组 opentrace 工具包脚本 [https://github.com/opendtrace/toolkit](https://github.com/opendtrace/toolkit) 。


## <a name="hello-world"></a>Hello World

DTrace 脚本是包含命令和 D 编程脚本元素的简单文本文件。

```dtrace
dtrace:::BEGIN
{
  trace("Hello World from DTrace!");
  exit(0);
}
```

将该文件另存为 helloworld。

以管理员身份打开命令提示符窗口，并使用-s 选项运行脚本。

```dtrace
dtrace -s helloworld.d
dtrace: script '.\helloworld.d' matched 1 probe
CPU     ID                    FUNCTION:NAME
  0      1                           :BEGIN   Hello World from DTrace!
```

## <a name="ntcreateuserprocess-return-time"></a>NtCreateUserProcess 返回时间

可以编写 DTrace 脚本来跟踪跨多个函数/事件所花的时间。 下面是一个简单的示例，该示例跟踪创建进程的输入/返回之间的 NtCreateUserProcess 函数。

```dtrace

syscall::NtCreateUserProcess:entry
{
    self->ts = timestamp;
}

syscall::NtCreateUserProcess:return
{
    printf(" [Caller %s]: Time taken to return from create process is %d MicroSecond \n", execname, (timestamp - self->ts)/ 1000);
}

```

将该文件另存为 ntcreatetime，并使用-s 选项运行测试脚本。


```dtrace
C:\Windows\system32>dtrace -s ntcreatetime.d
dtrace: script 'ntcreatetime.d' matched 2 probes
CPU     ID                    FUNCTION:NAME
  0    183       NtCreateUserProcess:return  [Caller svchost.exe]: Time taken to return from create process is 51191 MicroSecond

  0    183       NtCreateUserProcess:return  [Caller SearchIndexer.]: Time taken to return from create process is 84418 MicroSecond

  0    183       NtCreateUserProcess:return  [Caller SearchIndexer.]: Time taken to return from create process is 137961 MicroSecond

```

## <a name="file-delete-tracker"></a>文件删除跟踪器

此示例脚本使用 syscall 提供程序来检测 NtOpenFile，并检查传递 (参数 #5) ，以跟踪整个系统中的删除。

将以下脚本复制到 filedeletetracker 中。

```dtrace
ERROR{exit(0);}

struct ustr{uint16_t buffer[256];};

syscall::NtOpenFile:entry
{
   this->deleted = arg5 & 0x00001000; /* & with FILE_DELETE_ON_CLOSE */

  if (this->deleted) {
        this->attr = (nt`_OBJECT_ATTRIBUTES*)
            copyin(arg2, sizeof(nt`_OBJECT_ATTRIBUTES));

        if (this->attr->ObjectName) {
            this->objectName = (nt`_UNICODE_STRING*)
                copyin((uintptr_t)this->attr->ObjectName,
                       sizeof(nt`_UNICODE_STRING));
          
            this->fname = (uint16_t*)
                copyin((uintptr_t)this->objectName->Buffer,
                       this->objectName->Length);

            printf("Process %s PID %d deleted file %*ws \n", execname,pid, 
            this->objectName->Length / 2, 
             ((struct ustr*)this->fname)->buffer);
        }
    }
}
```

使用-s 选项运行测试脚本。

创建或找到要删除的文件。 将该文件移动到 "回收站"，然后清空 "回收站"。 删除文件并触发事件时，将显示有关文件删除的信息。

```dtrace
C:\Windows\system32>dtrace -s filedeletetracker.d
dtrace: script 'filedeletetracker.d' matched 8 probes
CPU     ID                    FUNCTION:NAME
  0    512                 NtOpenFile:entry Process explorer.exe PID 4684 deleted file \??\C:\$Recycle.Bin\S-1-12-1-3310478672-1302480547-4207937687-2985363607\$ROSR3FA.txt
```

此程序旨在继续监视文件删除。 按 CTRL + C 退出。

有关更大的代码示例，请参阅下一主题 [DTrace Windows 代码示例](dtrace-code-samples.md)。

## <a name="see-also"></a>另请参阅

[Windows 上的 DTrace](dtrace.md)

[DTrace ETW](dtrace-etw.md)

[DTrace Windows 代码示例](dtrace-code-samples.md)

[DTrace 实时转储](dtrace-live-dump.md)
