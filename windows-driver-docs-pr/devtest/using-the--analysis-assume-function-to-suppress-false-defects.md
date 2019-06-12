---
title: 使用 _analysis_assume 函数抑制误判缺陷
description: 使用 _analysis_assume 函数抑制误判缺陷
ms.assetid: eb71a664-ada5-44e3-b75d-b1a7348b115f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 215121b46c1fb8f49f24bb8eece471e62f20f7fa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325420"
---
# <a name="using-the-analysisassume-function-to-suppress-false-defects"></a>使用\_分析\_假定禁止显示 False 缺陷函数


您可以向 Static Driver Verifier (SDV) 提供的其他信息有关您的驱动程序源代码，以便在验证期间，可取消的 false 缺陷报告。 SDV 报告了明显的规则冲突，但该驱动程序正确操作的情况下，会出现 false 缺陷。

若要为 SDV 提供此附加信息，请使用 **\_ \_analysis\_假定**函数。 该函数具有以下语法：

```
__analysis_assume( expression ) 
```

其中*表达式*可以是任何表达式的计算结果为假定**true**。

SDV 时使用此函数，假设条件表示由*表达式*是**true**点位置 **\_ \_analysis\_假定**函数显示。 **\_ \_Analysis\_假定**函数只能使用由静态分析工具。 编译器将忽略该函数。

如果您使用 **\_ \_analysis\_假定**，这一点至关重要，您确信可以在进行的假设的有效性。 如果事实证明，您的假设**false**，现在或在将来，你无法将禁止显示，则返回 true 的缺陷。 我们建议你始终向您说明为什么要使用的代码添加注释 **\_ \_analysis\_假定**函数。 如果您不能编写假设的原因，不要禁止显示缺陷。

应将添加 **\_ \_analysis\_假定**函数根据需要您找到可以安全地的 false 缺陷时禁止显示。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

在下面的代码示例，KMDF 规则[RequestCompletedLocal](https://msdn.microsoft.com/library/windows/hardware/ff551609)报告缺陷。 这是误报缺陷，因为无法正确解释 SDV**切换**语句，因此不会进入分支完成请求。

在此**切换**语句中，有六个可能的情况。 该驱动程序已经定义了六个 IOCTL 代码，因此，该驱动程序将绝对需要的一个分支。 如果采用的一个分支，该请求是成功完成。

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

若要安全地禁止显示误报缺陷，请使用 **\_ \_analysis\_假定**函数指定的*IoControlCode*保证是一个 Ioctl定义了该驱动程序。

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

有关如何使用的另一个示例 **\_ \_analysis\_假定**，请参阅示例代码中使用[Using \_ \_sdv\_保存\_请求和\_ \_sdv\_检索\_延迟过程调用的请求](using---sdv-save-request-and---sdv-retrieve-request-for-deferred-proce.md)。 该示例演示如何使用 **\_ \_sdv\_保存\_请求**并 **\_ \_sdv\_检索\_请求**的 Dpc （工作项、 计时器等）。 **\_ \_Analysis\_假定**函数用于禁止显示 false，否则可能会导致的缺陷。

 

 





