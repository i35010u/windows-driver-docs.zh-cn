---
title: wudfext.wudfrequest
description: Wudfext.wudfrequest 扩展显示有关的 I/O 请求的信息。
ms.assetid: 4812c7bb-0fce-43e1-8f07-e4da9dd0c3bb
keywords:
- wudfext.wudfrequest Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wudfext.wudfrequest
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 13d09e379a886a8e18d58860c6eb65fbf8dec3ca
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545882"
---
# <a name="wudfextwudfrequest"></a>!wudfext.wudfrequest

**！ Wudfext.wudfrequest**扩展显示有关的 I/O 请求的信息。

```dbgcmd
!wudfext.wudfrequest pWDFRequest
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数

<span id="_______pWDFRequest______"></span><span id="_______pwdfrequest______"></span><span id="_______PWDFREQUEST______"></span> *pWDFRequest*   
指定的地址**WDFIoRequest**接口来显示有关的信息。 [ **！ Wudfext.wudfqueue** ](-wudfext-wudfqueue.md)扩展命令确定地址**WDFIoRequest**。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wudfext.dll
 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[用户模式驱动程序框架调试](user-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

以下是一种 **！ wudfext.wudfrequest**显示：

```dbgcmd
kd> !wudfrequest 0x000fa530 
CWdfIoRequest  0x000fa4b8
Type: WdfRequestRead
  IWDFIoQueue: 0x000f3500
Completed: No
Canceled: No
UM IRP: 0x00429108  UniqueId: 0xf4  Kernel Irp: 0x0x936ef160
  Type: WudfMsg_READ
  ClientProcessId: 0x1248
  Device Stack: 0x003be4e0
  IoStatus
    hrStatus: 0x0
    Information: 0x0
  Driver/Framework created IRP: No
  Data Buffer: 0x00000000 / 0
  IsFrom32BitProcess: Yes
  CancelFlagSet: No
  Cancel callback: 0x000fa534
  Total number of stack locations: 2
  CurrentStackLocation: 2 (StackLocation[ 1 ])
    StackLocation[ 0 ]
      UNINITIALIZED
  > StackLocation[ 1 ]
      IWDFRequest:  ????
      IWDFDevice:   0x000f2f80
      IWDFFile:     0x00418cf0
      Completion:
        Callback:   0x00000000
        Context:    0x00000000
      Parameters: (RequestType: WdfRequestRead)
        Buffer length:        0x400
        Key:                  0x00000000
        Offset:               0x0
```

 

 





