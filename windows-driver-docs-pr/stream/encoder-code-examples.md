---
title: 编码器代码示例
description: 编码器代码示例
ms.assetid: cbe773ad-2222-4d62-8e1e-6d47418a3e7c
keywords:
- 可变的位速率 WDK 编码器
- 编码器设备 WDK AVStream
- AVStream WDK，编码器设备
- 未压缩数据流 WDK AVStream
- 编码的流 WDK AVStream
- 音频编码器设备 WDK AVStream
- 视频编码器设备 WDK AVStream
- ENCAPIPARAM_BITRATE_MODE
- ENCAPIPARAM_BITRATE
- 位速率 WDK 编码器
- 注册表 WDK 编码器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 632aa4aafecbb1c2d64cb6819a7536edc3085151
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363562"
---
# <a name="encoder-code-examples"></a>编码器代码示例


下面的代码示例基于[AVStream 模拟硬件示例驱动程序 (AVSHwS)](https://go.microsoft.com/fwlink/p/?linkid=256083)。 它们演示了：

-   如何指定编码器的受支持的比特率

-   如何指定编码模式支持的编码器的比特率

-   如何在运行时，编码器设备下指定元数据值*设备参数\\功能*注册表项

### <a name="implementing-supported-bit-rates"></a>**实现支持的比特率**

下面的代码段演示如何实现对支持[ENCAPIPARAM\_比特率](https://msdn.microsoft.com/library/windows/hardware/ff559520)属性。 使用[ **KSPROPERTY\_单步执行\_长**](https://msdn.microsoft.com/library/windows/hardware/ff565631)结构，以指定具有 400 bps 下界和 4,000,000 bps 上限 400 位 / 秒 (bps) 以单步执行粒度。

```cpp
const KSPROPERTY_STEPPING_LONG BitRateRanges [] = {
    {
        400,
        0,
        400,
        4000000
    }
};
```

如果通过右键单击 GraphEdit 之类的工具中的筛选器访问编码器筛选器的属性页，你将看到**比特率**滚动条将使用这些值。

接下来，指定的默认编码比特率的编码器筛选器时创建它的一个实例。 请注意，使用的数据类型是对应于 ENCAPIPARAM 所需的属性值类型的 ULONG\_比特率属性。 此值是默认编码"比特率"的编码器的属性页中显示：

```cpp
const ULONG BitRateValues [] = {
    1000000
};
```

合法范围和默认值的列表指定为 ENCAPIPARAM\_比特率属性：

```cpp
 const KSPROPERTY_MEMBERSLIST BitRateMembersList [] = {
    {
        {
            KSPROPERTY_MEMBER_STEPPEDRANGES,
            sizeof (BitRateRanges),
            SIZEOF_ARRAY (BitRateRanges),
            0
        },
        BitRateRanges
    },
    {
        {
            KSPROPERTY_MEMBER_VALUES,
            sizeof (BitRateValues),
            SIZEOF_ARRAY (BitRateValues),
            KSPROPERTY_MEMBER_FLAG_DEFAULT
        },
        BitRateValues
    }
};
```

```cpp
 const KSPROPERTY_VALUES BitRateValuesSet = {
    {
        STATICGUIDOF (KSPROPTYPESETID_General),
        VT_UI4,
        0
    },
    SIZEOF_ARRAY (BitRateMembersList),
    BitRateMembersList
};
```

指定为 ENCAPIPARAM 定义的单个属性\_比特率属性集：

```cpp
DEFINE_KSPROPERTY_TABLE(ENCAPI_BitRate) {
    DEFINE_KSPROPERTY_ITEM (
        0,
        GetBitRateHandler, //Get-property handler supported
        sizeof (KSPROPERTY),
        sizeof (ULONG),
        SetBitRateHandler, //Set-property handler supported
        &BitRateValuesSet,
        0,
        NULL,
        NULL,
        sizeof (ULONG)
        )
};
```

**请注意**   *获取*的属性处理程序返回的编码比特率，并且*设置*-属性处理程序必须测试然后再使用它传入传入的值是否有效。

 

### <a name="implementing-supported-encoding-bit-rate-modes"></a>**实现支持编码的位速率模式**

下面的代码段演示如何实现对支持[ENCAPIPARAM\_比特率\_模式](https://msdn.microsoft.com/library/windows/hardware/ff559524)属性。

定义编码器所支持的编码模式：

```cpp
 const VIDEOENCODER_BITRATE_MODE BitRateModeValues [] = {
    ConstantBitRate,
    VariableBitRateAverage
};
```

指定的默认编码为平均可变比特率的位速率模式：

```cpp
const VIDEOENCODER_BITRATE_MODE BitRateModeDefaultValues [] = {
    VariableBitRateAverage
};
```

指定的合法范围列表和默认值为 ENCAPIPARAM\_比特率\_模式属性：

```cpp
const KSPROPERTY_MEMBERSLIST BitRateModeMembersList [] = {
    {
        {
            KSPROPERTY_MEMBER_VALUES,
            sizeof (BitRateModeValues),
            SIZEOF_ARRAY (BitRateModeValues),
            0
        },
        BitRateModeValues
    },
    {
        {
            KSPROPERTY_MEMBER_VALUES,
            sizeof (BitRateModeDefaultValues),
            SIZEOF_ARRAY (BitRateModeDefaultValues),
            KSPROPERTY_MEMBER_FLAG_DEFAULT
        },
        BitRateModeDefaultValues
    }
};

const KSPROPERTY_VALUES BitRateModeValuesSet = {
    {
        STATICGUIDOF (KSPROPTYPESETID_General),
        VT_I4,
        0
    },
    SIZEOF_ARRAY (BitRateModeMembersList),
    BitRateModeMembersList
};
```

指定为 ENCAPIPARAM 定义的单个属性\_比特率\_模式属性设置：

```cpp
DEFINE_KSPROPERTY_TABLE(ENCAPI_BitRateMode) {
    DEFINE_KSPROPERTY_ITEM (
        0,
        GetBitRateModeHandler, //Get-property handler supported
        sizeof (KSPROPERTY),
        sizeof (VIDEOENCODER_BITRATE_MODE),
        SetBitRateModeHandler, //Set-property handler supported
        &BitRateModeValuesSet,
        0,
        NULL,
        NULL,
        sizeof (VIDEOENCODER_BITRATE_MODE)
        )
};
```

**请注意**   *获取*-属性处理程序应返回的编码的位速率模式，并且*设置*-属性处理程序必须测试传入传入的值是否有效之前使用它。

 

然后将该属性设置指定为[ **KSFILTER\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff562553)结构的自动化表。

```cpp
DEFINE_KSPROPERTY_SET_TABLE(PropertyTable) {
    DEFINE_KSPROPERTY_SET(
        &ENCAPIPARAM_BITRATE_MODE,
        SIZEOF_ARRAY (ENCAPI_BitRateMode),
        ENCAPI_BitRateMode,
        0,
        NULL
        ),
    DEFINE_KSPROPERTY_SET(
        &ENCAPIPARAM_BITRATE,
        SIZEOF_ARRAY (ENCAPI_BitRate),
        ENCAPI_BitRate,
        0,
        NULL
        )
};

DEFINE_KSAUTOMATION_TABLE(FilterTestTable) {
    DEFINE_KSAUTOMATION_PROPERTIES(PropertyTable),
    DEFINE_KSAUTOMATION_METHODS_NULL,
    DEFINE_KSAUTOMATION_EVENTS_NULL
};

const 
KSFILTER_DESCRIPTOR 
FilterDescriptor = {
    ...,
    &FilterTestTable, // Automation Table
    ...,
    ...
};
```

### <a href="" id="specifying-the-encoder-s-capabilities-in-the-registry"></a>**在注册表中指定编码器的功能**

下面的代码示例演示如何创建*功能*注册表项下的*设备参数*注册表项，以及如何创建和指定子键和值下的*功能*密钥。 该驱动程序初始化时，请执行此代码。

**注意：** 以下代码假定每个物理设备的单个硬件编码器存在。 如果您的硬件包含多个编码器，则必须循环访问对的调用中返回的列表**IoGetDeviceInterfaces**函数，并为每个编码器注册功能。

```cpp
/**************************************************************************
CreateDwordValueInCapabilityRegistry()

IN Pdo: PhysicalDeviceObject
IN categoryGUID: Category GUID eg KSCATEGORY_CAPTURE

1. Get Symbolic name for interface
2. Open registry key for storing information about a 
   particular device interface instance
3. Create Capabilities key under "Device Parameters" key
4. Create a DWORD value "TestCapValueDWORD" under Capabilities

Must be running at IRQL = PASSIVE_LEVEL in the context of a system thread
**************************************************************************/
NTSTATUS CreateDwordValueInCapabilityRegistry(IN PDEVICE_OBJECT pdo, IN GUID categoryGUID)

{

    // 1. Get Symbolic name for interface
    // pSymbolicNameList can contain multiple strings if pdo is NULL. 
    // Driver should parse this list of string to get 
    // the one corresponding to current device interface instance. 
    PWSTR  pSymbolicNameList = NULL;

    NTSTATUS ntStatus = IoGetDeviceInterfaces(
        &categoryGUID,
        pdo,
        DEVICE_INTERFACE_INCLUDE_NONACTIVE,
        &pSymbolicNameList);
    if (NT_SUCCESS(ntStatus) && (NULL != pSymbolicNameList))
    {
        HANDLE hDeviceParametersKey = NULL;
        UNICODE_STRING symbolicName;

        // 2. Open registry key for storing information about a 
        // particular device interface instance
        RtlInitUnicodeString(&symbolicName, pSymbolicNameList);
        ntStatus = IoOpenDeviceInterfaceRegistryKey(
            &symbolicName,
            KEY_READ|KEY_WRITE,
            &hDeviceParametersKey);
        if (NT_SUCCESS(ntStatus))
        {
            OBJECT_ATTRIBUTES objAttribSubKey;
            UNICODE_STRING subKey;
 
            // 3. Create Capabilities key under "Device Parameters" key
            RtlInitUnicodeString(&subKey,L"Capabilities");
            InitializeObjectAttributes(&objAttribSubKey,
                &subKey,
                OBJ_KERNEL_HANDLE,
                hDeviceParametersKey,
                NULL);
 
            HANDLE hCapabilityKeyHandle = NULL;
 
            ntStatus = ZwCreateKey(&hCapabilityKeyHandle,
                    KEY_READ|KEY_WRITE|KEY_SET_VALUE,
                    &objAttribSubKey,
                    0,
                    NULL,
                    REG_OPTION_NON_VOLATILE,
                    NULL);
            if (NT_SUCCESS(ntStatus))
            {
                OBJECT_ATTRIBUTES objAttribDwordKeyVal;
                UNICODE_STRING subValDword;
 
                // 4. Create a DWORD value "TestCapValueDWORD" under Capabilities 
                RtlInitUnicodeString(&subValDword,L"TestCapValueDWORD");
 
                ULONG data = 0xaaaaaaaa;
 
                ntStatus = ZwSetValueKey(hCapabilityKeyHandle,&subValDword,0,REG_DWORD,&data,sizeof(ULONG));
                ZwClose(hCapabilityKeyHandle);
            }
        }
        ZwClose(hDeviceParametersKey);
        ExFreePool(pSymbolicNameList);
    }
 
    return ntStatus;
}
```

 

 




