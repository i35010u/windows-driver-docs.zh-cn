---
title: Hyper-V 可扩展交换机策略概述
description: Hyper-V 可扩展交换机策略概述
ms.assetid: 1D0AC55B-60F7-400E-A376-F3E2F7373A92
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dce3c0ff8072655d8922171319c9494084863e4a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564606"
---
# <a name="overview-of-hyper-v-extensible-switch-policies"></a>Hyper-V 可扩展交换机策略概述


HYPER-V 平台和可扩展交换机接口提供了一个基础结构来管理交换机和端口的可扩展交换机的策略。 通过 PowerShell cmdlet 和基于 WMI 的应用程序，这些策略进行管理。 此基础结构还提供对存储和迁移策略的支持。

独立软件供应商 (Isv) 可以使用此基础结构注册其自己的自定义策略。 它们要注册后，可以发现这些策略，并通过内置的 HYPER-V 策略接口进行管理。 每个端口级别或每个交换机级别上，可以配置策略的属性。

除了自定义策略属性中，HYPER-V 可扩展交换机接口提供用于获取每个端口或在每个交换机的基础上自定义策略属性的状态信息的基础结构。 此状态信息被称为*功能状态*信息。

可扩展交换机的自定义策略数据已注册 WMI 管理层使用的托管的对象格式 (MOF) 类定义。 下面演示自定义端口策略属性的 MOF 类的示例。

```C++
#pragma namespace("\\\\.\\root\\virtualization\\v2")

[ Dynamic, 
 UUID("F2F73F23-2B8E-457a-96C4-F541201C9150"),
 ExtensionId("5CBF81BE-5055-47CD-9055-A76B2B4E369E"), 
 Provider("VmmsWmiInstanceAndMethodProvider"), 
 Locale(0x409),
 InterfaceVersion("1"),
 InterfaceRevision("0"),
DisplayName("VendorName Port Settings Friendly Name") : Amended,
Description("VendorName Port Settings detailed description.") : Amended]
class Vendor_SampleFeatureSettingData: Msvm_EthernetSwitchPortFeatureSettingDataMsvm
{
  [WmiDataId(1),
   InterfaceVersion("1"),
   InterfaceRevision("0")]
  uint8  IntValue8 = 0;

  [WmiDataId(2),
   InterfaceVersion("1"),
   InterfaceRevision("0")]
  uint16 IntValue16 = 0;

  [WmiDataId(3),
   InterfaceVersion("1"),
   InterfaceRevision("0")]
  uint32 IntValue32 = 0;

  [WmiDataId(4),
   InterfaceVersion("1"),
   InterfaceRevision("0")]
  uint64 IntValue64 = 0;

  [WmiDataId(5),
   InterfaceVersion("1"),
   InterfaceRevision("0"), 
   MaxLen(255)]
  string FixedLengthString = "";

  [WmiDataId(6),
   InterfaceVersion("1"),
   InterfaceRevision("0")]
  string VariableLengthString = "";

  [WmiDataId(7),
   InterfaceVersion("1"),
   InterfaceRevision("0"),
   Max(8)]
  uint32 FixedLengthArray[] = {};

  [WmiDataId(8),
   InterfaceVersion("1"),
   InterfaceRevision("0")]
  uint32 VariableLengthArray[] = {};

};
```

WMI 管理层将 MOF 数据序列化，传输到底层的可扩展交换机扩展的时间。 MOF 类是序列化到 HYPER-V 可扩展交换机扩展可以处理的相应 C 结构。 下面显示了上一示例中的 MOF 类进行序列化的 C 结构的示例。

```C++
#pragma pack(8)

typedef struct _VARIABLE_LENGTH_ARRAY
{
    UINT32 Buffer[1];
} VARIABLE_LENGTH_ARRAY;

typedef struct _SAMPLE_FEATURE_SETTINGS
{
    UINT8  IntValue8;
    UINT32 IntValue16;
    UINT32 IntValue32;
    UINT64 IntValue64;
    UINT16 FixedLengthStringByteCount;
    WCHAR  FixedLengthString[256]; 
    UINT32 VariableLengthStringOffset;    // offset to VARIABLE_LENGTH_STRING structure
    UINT32 FixedLengthArrayElementCount;
    UINT32 FixedLengthArray[8];
    UINT32 VariableLengthArrayElementCount;
    UINT32 VariableLengthArrayOffset;   // offset to VARIABLE_LENGTH_ARRAY
} SAMPLE_FEATURE_SETTINGS;
 
typedef struct _VARIABLE_LENGTH_STRING
{
    USHORT StringLength;
    WCHAR  StringBuffer[1];
} VARIABLE_LENGTH_STRING;
```

此示例重点介绍 MOF 类序列化为可扩展交换机策略属性的相应 C 结构时出现的以下几点：

-   在 MOF 文件中的版本定义转换为 USHORT 值，其中高顺序位包含的主要版本和低顺序位包含次要版本。 通过使用下面的代码序列化版本：

    `  (((MajorVersion) << 8) + (MinorVersion))`

    例如，上述 Version("1") 会序列化为 0x0100 通过值`(((1) << 8) + (0))`。 版本 ("1.1") 将为 0x0101 通过值进行序列化`(((1) << 8) + (1))`。

    当向扩展名为基础，发出自定义策略属性**PropertyVersion**定义策略的属性的结构的成员包含序列化的版本值。

    例如，当可扩展交换机接口发出的对象标识符 (OID) 请求[OID\_切换\_端口\_属性\_添加](https://msdn.microsoft.com/library/windows/hardware/hh598275)，OID 是与相关联[**NDIS\_交换机\_端口\_属性\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598238)结构。 **PropertyVersion**该结构的成员包含的序列化的版本值。

-   所有可变长度字符串会被都序列化为包含序列都化的 C 结构的缓冲区内的偏移量。 每个可变长度字符串的格式设置为**变量\_长度\_字符串**此缓冲区偏移量中的结构。

 

 





