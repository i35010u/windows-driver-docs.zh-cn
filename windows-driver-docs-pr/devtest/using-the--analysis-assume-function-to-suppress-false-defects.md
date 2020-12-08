---
title: 使用 _analysis_assume 函数抑制误判缺陷
description: 使用 _analysis_assume 函数抑制误判缺陷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 580de0b62195cabb3f40114fcc2716eac26e01aa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822521"
---
# <a name="using-the-_analysis_assume-function-to-suppress-false-defects"></a>使用 \_ 分析 \_ 假设函数禁止显示错误


可以向静态驱动程序验证程序 (SDV) 提供有关驱动程序源代码的其他信息，以便在验证期间可以禁止显示错误错误的报告。 当 SDV 报告明显的规则冲突，但在驱动程序正常工作的情况下，会出现错误。

若要为 SDV 提供此附加信息，请使用 **\_ \_ 分析 \_ 假定** 函数。 函数具有以下语法：

```
__analysis_assume( expression ) 
```

其中 *expression* 可以是计算结果为 **true** 的任何表达式。

使用此函数时，SDV 假定 *表达式* 表示的条件在 **\_ \_ 分析 \_ 假设** 函数显示的点处为 **true** 。 **\_ \_ 分析 \_ 假定** 函数仅由静态分析工具使用。 编译器将忽略该函数。

如果你使用 **\_ \_ 分析 \_ 假设**，则一定要确定你所做的假设有效性，这一点至关重要。 如果事实证明您假设是 **假** 的，无论是现在还是将来，您都可能会禁止真正的缺陷。 建议你始终向代码添加注释，说明使用 **\_ \_ 分析 \_ 假定** 函数的原因。 如果无法编写假设的原因，请不要取消该缺陷。

你应根据需要添加 **\_ \_ 分析 \_ 假设** 函数，只要你发现可以安全取消的错误。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

在下面的代码示例中，KMDF 规则 [RequestCompletedLocal](./kmdf-requestcompletedlocal.md) 报告了一个缺陷。 这是错误的缺陷，因为 SDV 无法正确解释 **switch** 语句，因此不会进入请求完成的分支。

此 **switch** 语句中有六种可能的情况。 驱动程序定义了六条 IOCTL 代码，因此驱动程序将绝对采用其中一个分支。 如果执行了其中一个分支，则请求会成功完成。

```
VOID
PortIOEvtIoDeviceControl(
      __in WDFQUEUE     Queue,
      __in WDFREQUEST   Request,
      __in size_t       OutputBufferLength,
  __in size_t       InputBufferLength,
  __in ULONG        IoControlCode
     )
 
     PDEVICE_CONTEXT devContext = NULL;
     WDFDEVICE device;

     PAGED_CODE();
 
     device = WdfIoQueueGetDevice(Queue);
 
     devContext = PortIOGetDeviceContext(device);
 
     switch(IoControlCode)
         case IOCTL_GPD_READ_PORT_UCHAR:
         case IOCTL_GPD_READ_PORT_USHORT:
         case IOCTL_GPD_READ_PORT_ULONG:
             PortIOIoctlReadPort(devContext,
                                 Request,
                                 OutputBufferLength,
                                 InputBufferLength,
                                 IoControlCode);
             break;

 
         case IOCTL_GPD_WRITE_PORT_UCHAR:
         case IOCTL_GPD_WRITE_PORT_USHORT:
         case IOCTL_GPD_WRITE_PORT_ULONG:    
             PortIOIoctlWritePort(devContext,
                                  Request,
                                  OutputBufferLength,
                                  InputBufferLength,
                                  IoControlCode);
             break;
 
     }
 
}
```

若要安全地取消误报，请使用 **\_ \_ analysis \_ 假设** 函数指定 *IoControlCode* 保证为驱动程序定义的 IOCTLs 之一。

```
VOID
PortIOEvtIoDeviceControl(
      __in WDFQUEUE     Queue,
      __in WDFREQUEST   Request,
      __in size_t       OutputBufferLength,
      __in size_t       InputBufferLength,
      __in ULONG        IoControlCode
     )
 
     PDEVICE_CONTEXT devContext = NULL;
     WDFDEVICE device;

     PAGED_CODE();
 
     device = WdfIoQueueGetDevice(Queue);
 
     devContext = PortIOGetDeviceContext(device);

/* Use __analysis_assume to suppress a false defect for the SDV RequestCompletedLocal rule. 
There are only 6 possible IOCTLs for IoControlCode; each case is covered in the switch statement.
*/

 __analysis_assume( IoControlCode == IOCTL_GPD_READ_PORT_UCHAR || \
                       IoControlCode == IOCTL_GPD_READ_PORT_USHORT|| \
                       IoControlCode == IOCTL_GPD_READ_PORT_ULONG || \
                       IoControlCode == IOCTL_GPD_WRITE_PORT_UCHAR|| \
                       IoControlCode == IOCTL_GPD_WRITE_PORT_USHORT|| \
                       IoControlCode == IOCTL_GPD_WRITE_PORT_ULONG);

     switch(IoControlCode)
         case IOCTL_GPD_READ_PORT_UCHAR:
         case IOCTL_GPD_READ_PORT_USHORT:
         case IOCTL_GPD_READ_PORT_ULONG:
             PortIOIoctlReadPort(devContext,
                                 Request,
                                 OutputBufferLength,
                                 InputBufferLength,
                                 IoControlCode);
             break;

 
         case IOCTL_GPD_WRITE_PORT_UCHAR:
         case IOCTL_GPD_WRITE_PORT_USHORT:
         case IOCTL_GPD_WRITE_PORT_ULONG:    
             PortIOIoctlWritePort(devContext,
                                  Request,
                                  OutputBufferLength,
                                  InputBufferLength,
                                  IoControlCode);
             break;
 
     }
 
}
```

有关如何使用 **\_ \_ 分析 \_ 假设** 的另一个示例，请参阅 [使用 \_ \_ sdv \_ save \_ 请求和 \_ \_ sdv \_ 检索 \_ 延迟过程调用的请求](using---sdv-save-request-and---sdv-retrieve-request-for-deferred-proce.md)中使用的代码示例。 该示例演示了如何使用 **\_ \_ sdv \_ save \_ request** 和 **\_ \_ sdv \_ 检索 \_** () 上的 dpc 的请求。 **\_ \_ 分析 \_ 假设** 函数用于禁止显示可能导致的错误缺陷。

 

