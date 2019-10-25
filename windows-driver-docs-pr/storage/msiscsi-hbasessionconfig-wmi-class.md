---
title: MSiSCSI\_HBASessionConfig WMI 类
description: MSiSCSI\_HBASessionConfig WMI 类
ms.assetid: ef3ac7d0-be4a-457e-b837-a6434776dfc1
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 92774af8522de98193052e12d5ef73f593dbf22b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845362"
---
# <a name="msiscsi_hbasessionconfig-wmi-class"></a>MSiSCSI\_HBASessionConfig WMI 类


## <span id="ddk_msiscsi_hbasessionconfig_wmi_class_kr"></span><span id="DDK_MSISCSI_HBASESSIONCONFIG_WMI_CLASS_KR"></span>


管理应用程序可以使用 MSiSCSI\_HBASessionConfig WMI 类检索和设置存储微型端口驱动程序的特定实例用来与目标设备建立登录会话的默认配置选项。

由于此类与存储微型端口驱动程序的特定实例相关联，因此微型端口驱动程序必须使用微型端口驱动程序管理的特定物理设备对象（PDO）的名称来注册该类。

MSiSCSI\_HBASessionConfig 类在*管理 mof*中定义为如下。

```cpp
class MSiSCSI_HBASessionConfig {
  [key] string  InstanceName;
  boolean  Active;
  [WmiDataId(1), read, write, Description(" The InitialR2T
    key is used to turn off the default use of R2T, thus
    allowing an initiator to start sending data to a target
    as if it has received an initial R2T with Buffer
    Offset=0 and Desired Data Transfer Length=min
    (FirstBurstSize, Expected Data Transfer Length).") :
    amended] 
    boolean  InitialR2T;
  [WmiDataId(2), read, write, Description("The initiator and
    target negotiate support for immediate data. To turn
    immediate data off, the initiator or target must state
    its desire to do so.  ImmediateData can be turned on if
    both the initiator and target have ImmediateData=Yes.")
    : amended]
    boolean  ImmediateData;
  [WmiDataId(3), read, write, Description("Maximum data
    segment length in bytes they can receive in an iSCSI
    PDU.") : amended] 
    uint32  MaxRecvDataSegmentLength;
  [WmiDataId(4), read, write, Description("Maximum SCSI data
    payload in bytes in an Data-In or a solicited Data-Out
    iSCSI sequence.") : amended]
    uint32  MaxBurstLength;
  [WmiDataId(5), read, write, Description("maximum amount in
    bytes of unsolicited data an iSCSI initiator may send to
    the target, during the execution of a single SCSI
    command. This covers the immediate data (if any) and the
    sequence of unsolicited Data-Out PDUs (if any) that
    follow the command.") : amended]
    uint32  FirstBurstLength;
  [WmiDataId(6), read, write, Description("Initiator and
    target negotiate the maximum number of outstanding R2Ts
    per task, excluding any implied initial R2T that might
    be part of that task.  An R2T is considered outstanding
    until the last data PDU (with the F bit set to 1) is
    transferred, or a sequence reception timeout (section
    6.12.1) is encountered for that data sequence.") :
    amended]
    uint32  MaxOutstandingR2T;
};
```

当 WMI 工具套件编译上述类定义时，它会生成[**MSiSCSI\_HBASessionConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsimgt/ns-iscsimgt-_msiscsi_hbasessionconfig)数据结构。

 

 





